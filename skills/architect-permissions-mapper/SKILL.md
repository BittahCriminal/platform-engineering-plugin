---
name: architect-permissions-mapper
description: Normalizes Azure RBAC/Entra ID, AWS IAM, and Kubernetes RBAC into one IdentityBinding model, then flags over-privileged, cross-boundary, orphaned, and unowned access. Use when mapping permissions boundaries or auditing IAM/RBAC posture for a discovered environment.
status: planned
---

# Architect: Permissions Mapper

**Status:** Planned, not yet implemented. See [../../docs/idp-adp-architect/PLAN.md](../../docs/idp-adp-architect/PLAN.md) for the full domain plan.

## Role in the Architect tier

Turns three different native permission models into one comparable shape, and is the
connective tissue between "permissions boundaries" and "IAM and RBAC" — one mapper,
two views of its output.

## Reads

`.platform/inventory/resources.json` (from `architect-infra-discovery`) plus
Entra ID / IAM / K8s RBAC APIs via the same authenticated CLIs.

## Writes

`.platform/identity/bindings.json` — array of `IdentityBinding` objects per
`.platform/schema/identity_binding.schema.json` (`principal`, `role`, `scope`,
`resource_id`, `source_system`, `flags`).

## Three native models, one comparable shape

Azure RBAC/Entra, AWS IAM, and Kubernetes RBAC solve the same problem (who can do
what, at what scope) with structurally different primitives. The mapper's job is to
project all three onto `IdentityBinding`'s four required fields without losing the
distinctions that matter for the flag rules below:

| Dimension | Azure RBAC / Entra ID | AWS IAM | Kubernetes RBAC |
|---|---|---|---|
| Principal types | User, group, service principal, managed identity | IAM user, role, federated identity | User (via auth method), group, ServiceAccount |
| Scope granularity | Management group → subscription → resource group → resource | Account → (no native sub-scoping without SCPs/permission boundaries) | Cluster → namespace |
| Grant mechanism | Role assignment (built-in or custom role → principal → scope) | Policy attached to principal (identity-based) or resource (resource-based) | RoleBinding/ClusterRoleBinding → Role/ClusterRole → subject |
| "God mode" equivalent | `Owner` at subscription/management-group scope | `AdministratorAccess` or `*:*` policy | `cluster-admin` ClusterRoleBinding |
| `source_system` value | `azure-rbac` / `entra-id` | `aws-iam` | `k8s-rbac` |

## Kubernetes RBAC primitives (the model with the most moving parts)

Kubernetes RBAC needs the most care because "Role" alone is ambiguous — the mapper
must resolve four distinct object kinds into one `IdentityBinding.role`+`scope` pair
([*RBAC Policies and Auditing*](https://app.notion.com/3b8059b703e18166af51d6ada4ea7b2e)):

- **Role** — namespace-scoped permission set. Maps to `scope = namespace`.
- **ClusterRole** — cluster-scoped (or reusable across namespaces via
  ClusterRoleBinding + namespace-scoped RoleBinding). Maps to `scope = cluster` when
  bound via ClusterRoleBinding, `scope = namespace` when bound via RoleBinding.
- **RoleBinding** — grants a Role or ClusterRole to subjects *within one namespace*.
- **ClusterRoleBinding** — grants a ClusterRole to subjects *cluster-wide* — this is
  the binding kind the `over-privileged` flag should treat as highest-severity by
  default, since it collapses namespace boundaries entirely.
- **Aggregated ClusterRoles** (label-selector-composed from other ClusterRoles) and
  **negative roles** (a Role that grants nothing, used to occupy a name/prevent
  wildcard matches) are edge cases the mapper should resolve to their *effective*
  permission set, not their literal rule list — an aggregated ClusterRole with broad
  label selectors can be effectively cluster-admin without ever saying so.

Authentication feeds into this from a separate layer: Kubernetes doesn't authenticate
users itself, it defers to external identity via certs, tokens, or OIDC, then RBAC
authorizes based on the resulting user/group claims
([*Integrating Authentication into Your Cluster*](https://app.notion.com/3b8059b703e18185b617d491884ff674)).
Practically, this means the mapper needs the OIDC group-claim mapping (or equivalent)
to resolve a Kubernetes "group" subject back to a real Entra ID/IAM group — without
that join, K8s bindings and cloud bindings for the same human stay unlinked, and
`cross-boundary` detection (below) can't fire.

## Multi-tenancy boundary strength (informs `cross-boundary`)

Not all "namespace boundaries" are equally hard, which matters when deciding whether
a principal holding bindings in two namespaces is actually cross-boundary in a
meaningful sense:

| Isolation mechanism | Boundary strength | Notes |
|---|---|---|
| Namespace + ResourceQuota/LimitRange only | Soft — logical separation, shared control plane, shared node pool by default | Default assumption unless a NetworkPolicy or dedicated node pool is also present |
| Namespace + NetworkPolicy + quotas | Medium — network-isolated, still shared API server/etcd | |
| vCluster (virtual control plane per tenant) | Hard — each tenant gets its own API server/etcd, syncing down to a shared host cluster | ([*Building Multitenant Clusters with vClusters*](https://app.notion.com/3b8059b703e181c78561f9718697460d)) Treat vCluster boundaries as equivalent to separate clusters for `cross-boundary` purposes |

`Namespaces, Quotas, and Limits for Multi-Tenancy in Kubernetes` establishes that
namespaces alone were never designed as a hard security boundary — they're a resource
and naming boundary first. The mapper should not suppress `cross-boundary` just
because two grants sit in "different namespaces" if there's no NetworkPolicy/vCluster
backing that separation.

## Flag rules (v1) — detection heuristics

- **`over-privileged`** — wildcard scope (`resource_id: "*"`), a built-in
  `Owner`/`AdministratorAccess`-equivalent role, or a ClusterRoleBinding to
  `cluster-admin`. Treat ClusterRoleBinding-scoped grants as higher severity than
  namespace-scoped RoleBindings with the same nominal role name.
- **`cross-boundary`** — principal holds bindings across boundaries with *insufficient
  isolation strength* per the table above (soft/medium), not merely "more than one
  namespace" — a platform-team service account legitimately spanning namespaces
  behind a vCluster boundary should not trip this.
- **`orphaned`** — principal no longer exists (deleted user/deprovisioned service
  principal) or has no active `Persona` once `architect-persona-generator` has run —
  this flag can be set on a second pass after personas exist.
- **`unowned`** — binding's `resource_id` resolves to a `Resource` with no
  `owner_tag`, or has no corresponding `Workload`/`Product` owner once those catalogs
  exist — same second-pass pattern as `orphaned`.

## Security posture this mapper should surface, not just log

Two adjacent concerns from the source material belong in the blueprint's narrative
around a flagged binding, even though they're not `IdentityBinding` fields
themselves: **secrets exposure** — RBAC that's technically scoped correctly but sits
next to secrets committed to Git or unmanaged Kubernetes `Secret` objects is a
related finding worth cross-referencing
([*Security with GitOps*](https://app.notion.com/3b8059b703e1813cb9eac75c806a7bf1) —
Sealed Secrets/External Secrets as the remediation pattern), and **known-vulnerable
workloads holding broad bindings** — a principal with `over-privileged` access
*and* an unpatched CVE on the workload it runs as is a compounding risk
([*Vulnerability Management for Platform Engineers*](https://app.notion.com/3b8059b703e18143b1b6f5e8b0c48f39)).
The capstone (`architect-blueprint`) should be able to join these two flagged sets
rather than reporting them as unrelated findings.

## Addendum — agentic-era findings (verify identity before write)

The agentic-platform-engineering research pulled into this plugin surfaces a pattern
worth encoding as a mapper rule, not just narrative: **Workload Identity Federation**
(federated OIDC credentials bound to a Kubernetes ServiceAccount via the
`azure.workload.identity/use` pod label, rather than a long-lived secret) is the shape
a `Resource`↔`IdentityBinding` pair should have whenever an in-cluster workload calls a
cloud API — e.g. an AKS pod reading Azure Blob Storage via a federated credential
scoped to `Storage Blob Data Contributor`
([AKS + RunAI Model Streamer walkthrough](https://blog.aks.azure.com/2026/07/13/runai-streamer-vllm)).
A binding with `source_system: k8s-rbac` whose subject is a ServiceAccount *without* a
corresponding federated-credential/managed-identity binding is a candidate for a new
flag — **`legacy-credential`** — since it implies a static secret sits where a
workload identity should. This is additive to the v1 flag set above, not a
replacement.

The broader principle from the same research — every agentic write path must "verify
identity before write" and route destructive changes through human approval — is the
justification for why `over-privileged` should weight *agent-held* bindings (a
ServiceAccount or service principal used by a coding agent / cluster-remediation bot)
at least as strictly as human-held ones. Diagram 4 in
[../../docs/idp-adp-architect/diagrams.md](../../docs/idp-adp-architect/diagrams.md)
(org-level vs. repo-level agent inheritance) is the visual for this: an org-level
policy binding is the parent every repo-scoped agent identity should inherit from,
so a repo-level agent identity holding broader-than-inherited access is itself an
`over-privileged` finding, symmetric with the human case.

## Depends on

`architect-infra-discovery`
