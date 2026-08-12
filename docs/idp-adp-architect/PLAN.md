# IDP/ADP Architect — Domain & Delivery Plan

**Repo:** `BittahCriminal/platform-engineering-plugin`
**Status:** Proposed — new "Architect" tier alongside the existing "Reference" tier
**Author context:** L. Richard, Cloud Byte Consulting

## 1. Why this is a new tier, not just another skill

The plugin today (`platform-blueprint`, `cluster-lifecycle`, `platform-observability`,
`platform-security`, `cloud-dev-environments`, `ai-native-platform`,
`platform-state-of-play`) is a **Reference tier**: static knowledge distilled from
research, the same for every consumer, every time.

What you're describing — discovery, persona generation, workload/product definition,
permissions/IAM/RBAC mapping, work-tracking sync — is fundamentally different. It has to
read a *specific* organization's real cloud accounts, clusters, identity systems, and
tickets, and produce artifacts unique to that org. Call this the **Architect tier**: it
consumes the Reference tier's frameworks (five-plane model, personas, golden paths) as
its knowledge base, and applies them against live infrastructure.

Per the plugin-packaging decision tree, this is a **plugin with multiple skills plus
light integrations** — not a new MCP server. Every discovery/mapping skill shells out to
CLIs you already have authenticated (`az`, `aws`, `gcloud`, `kubectl`, `gh`) rather than
embedding cloud SDKs or standing up new infrastructure. Zero new credentials to manage.

## 2. Domain definition

- **Domain name:** IDP/ADP Architect (`idp-adp-architect`) — the "architect" half of
  `platform-engineering-plugin`.
- **Mission:** turn the plugin from "teaches platform engineering principles" into
  "helps you build and document *your* platform using those principles, against your
  actual environment."
- **Bounded context:** one organization's platform surface at a time — its cloud/local
  infrastructure, identities and permissions, workloads, product catalog, and the
  work-tracking system(s) it has authorized. Does not attempt cross-org benchmarking
  (that's `platform-state-of-play`'s job in the Reference tier).
- **Out of scope (v1):** actually provisioning or mutating infrastructure. This is a
  read/discover/document/recommend tool, matching the plugin's existing "AI-augmented,
  governed" design principle — no LLM mutates infra outside a trusted orchestrator.

## 3. Core domain model

A shared schema all Architect skills read/write, stored in the consumer's repo under
`.platform/` so it's git-tracked and diffable:

| Entity | Fields (core) | Produced by |
|---|---|---|
| `Resource` | id, provider, type, region/zone, tags, owner_tag | `architect-infra-discovery` |
| `IdentityBinding` | principal, role/scope, resource_id, source_system | `architect-permissions-mapper` |
| `Persona` | name, plane (five-plane model), consumes[], creates[], org_mapping | `architect-persona-generator` |
| `Workload` | id, type, spec (Score-style), resources[], owner_persona | `architect-workload-catalog` |
| `Product` | name, golden_path, workload_types[], SLA, owner_persona | `architect-product-catalog` |
| `WorkItem` | external_ref, system, linked_entity, status | `architect-work-sync` |

```
.platform/
  schema/            # JSON Schema defs for the 6 entities above
  inventory/resources.json
  identity/bindings.json
  personas/personas.yaml
  workloads/*.yaml
  catalog/products.yaml
  worktracking/links.json
```

`Persona.plane` maps directly onto `platform-blueprint`'s five-plane table, so
`architect-blueprint` (the capstone skill) can render an org-specific version of that
same table with real names instead of generic roles.

## 4. New skills (Architect tier)

| Skill | Reads | Writes | Depends on |
|---|---|---|---|
| `architect-infra-discovery` | cloud/K8s APIs via `az`/`aws`/`gcloud`/`kubectl` | `inventory/resources.json` | — |
| `architect-permissions-mapper` | AAD/Entra, IAM, K8s RBAC | `identity/bindings.json` | infra-discovery |
| `architect-persona-generator` | bindings + org data (AAD groups, GitHub teams) | `personas/personas.yaml` | permissions-mapper |
| `architect-workload-catalog` | resources + bindings | `workloads/*.yaml` | infra-discovery |
| `architect-product-catalog` | workloads + golden paths | `catalog/products.yaml` | workload-catalog |
| `architect-work-sync` | whichever of Linear/Jira/GitHub Projects/Azure DevOps is authorized | `worktracking/links.json` | personas, workloads |
| `architect-blueprint` (capstone) | all of the above + `platform-blueprint` reference | org blueprint doc (md/Notion) | all above |

## 5. Provider & integration strategy

**Infra discovery — multi-cloud architecture from day one, phased adapters:**
The `architect-infra-discovery` and `architect-permissions-mapper` skills define one
provider-adapter interface up front (`discover(provider) -> Resource[]`,
`bindings(provider) -> IdentityBinding[]`) so no downstream skill ever branches on
provider. Adapters are implemented in this order, matched to where you have live
access to validate against real data first:

1. Azure (subscriptions, Entra ID/AAD, resource groups) + on-prem/local Kubernetes
   (any cluster reachable via current `kubeconfig` context)
2. AWS (IAM, accounts/orgs)
3. GCP (IAM, projects)

Adding a provider later means writing one adapter file, not touching the other five
skills.

**Work tracking — adapter, not a fixed choice:**
`architect-work-sync` auto-detects which systems are actually connected/authorized at
run time (Linear, Jira, GitHub Issues/Projects, Azure DevOps Boards, etc.) and only
activates adapters for those. No system is hardcoded as "the" tracker — this matches
using whatever access a given consumer grants.

**Books/Research corpus:**
`research/SOURCES.md` is scaffolded now as an intake point. You'll attach your reading
list/files separately; once received, they get folded in the same way the existing
Reference skills cite their sources (IDP reference architectures, vulnerability/CDE
whitepapers, state-of reports) — each Architect skill's SKILL.md front matter will
credit the specific sources that shaped its logic (e.g., which RBAC/IAM standard, which
persona-modeling framework).

## 6. Permissions/IAM/RBAC mapping approach

`architect-permissions-mapper` normalizes three different native models (Azure
RBAC/Entra roles, AWS IAM policies, K8s RBAC ClusterRoles/RoleBindings) into one
`IdentityBinding` shape, then applies a small rule set flagged in the output:

- Over-privileged bindings (wildcard scopes, cluster-admin-equivalent grants)
- Cross-boundary access (a principal with bindings in more than one bounded context)
- Orphaned bindings (principal no longer exists / no longer has an active persona)
- Bindings with no corresponding `Workload` or `Product` owner (unowned access)

This is the connective tissue between "permissions boundaries" and "IAM and RBAC" in
your original ask — one mapper, two ways of looking at its output.

## 7. Delivery plan

| Phase | Scope | Depends on |
|---|---|---|
| 0 — Foundations | `.platform/schema/*`, 7 skill dirs scaffolded with SKILL.md stubs, this plan doc, `research/SOURCES.md` placeholder | — |
| 1 — Discovery core | `architect-infra-discovery`: Azure + on-prem K8s adapters, validated against one real subscription/cluster | Phase 0 |
| 2 — Identity & permissions | `architect-permissions-mapper`: Entra + K8s RBAC, flag rules | Phase 1 |
| 3 — Personas & workloads | `architect-persona-generator`, `architect-workload-catalog` | Phase 2 |
| 4 — Product catalog | `architect-product-catalog` | Phase 3 |
| 5 — Work tracking sync | `architect-work-sync`, adapters activated per what's authorized | Phase 3 |
| 6 — Multi-cloud expansion | AWS + GCP adapters added to discovery & permissions mapper | Phase 2 |
| 7 — Capstone | `architect-blueprint` orchestrates all of the above into one org blueprint doc | Phases 1–6 |

## 8. Open items before Phase 1 can start for real

- Attach the books/research list for `research/SOURCES.md`.
- Confirm which Azure tenant/subscription and which Kubernetes context(s) are safe to
  run discovery against first (a non-production one is recommended for the pilot run).
- When Phase 5 comes up, authorize whichever work-tracking connector(s) you want tested
  first (Linear/Jira/GitHub Projects/Azure DevOps) — no need to decide that now.
