---
name: architect-infra-discovery
description: Discovers real infrastructure across cloud and on-prem/local providers (Azure, AWS, GCP, Kubernetes) and normalizes it into the shared Resource schema. Use when starting a platform blueprint for a specific organization and no inventory exists yet, or when the inventory needs to be refreshed against current state.
status: planned
---

# Architect: Infra Discovery

**Status:** Planned, not yet implemented. See [../../docs/idp-adp-architect/PLAN.md](../../docs/idp-adp-architect/PLAN.md) for the full domain plan.

## Role in the Architect tier

First skill in the pipeline. Every other `architect-*` skill depends on the
`.platform/inventory/resources.json` this one produces. It is also the skill that
decides *what counts as ground truth* when live state and declared state disagree —
a decision every downstream skill inherits.

## Reads

Provider APIs via already-authenticated CLIs — `az`, `aws`, `gcloud`, `kubectl`
(current context) — plus, where present, Terraform/OpenTofu state files
(`terraform.tfstate` or a remote backend) as a second, declared-intent source.
No new credentials are provisioned by this skill; it uses whatever the operator is
already logged into.

## Writes

`.platform/inventory/resources.json` — array of `Resource` objects per
`.platform/schema/resource.schema.json` (`id`, `provider`, `type`, `region`, `tags`,
`owner_tag`, `discovered_at`).

## Two sources of truth, and how they reconcile

Discovery has to reconcile two different pictures of "what exists," and getting this
wrong is the single biggest source of a stale inventory ([*Understanding Terraform
Architecture*](https://app.notion.com/3b8059b703e181a5b337f54ec0f75cd0)):

| Source | What it captures | Failure mode if used alone |
|---|---|---|
| **Declared state** (Terraform/OpenTofu state file — the plan's record of what it created) | Everything the platform team intentionally provisioned, with module/resource lineage | Blind to anything created out-of-band (console click-ops, `kubectl apply` outside Git, a resource another team owns) |
| **Live state** (provider API / `kubectl get` against current context) | Everything that actually exists right now | No lineage — can't tell "team-owned platform resource" from "someone's forgotten test VM" |

The adapter runs both and tags each `Resource` with `in_state: true/false`. A resource
present live but absent from state is exactly the **partial resource management**
problem the Terraform state model warns about — it will get flagged, not silently
adopted into `owner_tag` inference below.

## Provider adapter matrix (build order)

| Provider | Native surface discovered | Auth already assumed | Key normalization work |
|---|---|---|---|
| **1. Azure** | Subscriptions → resource groups → resources (`az resource list`) | `az login` context / current subscription | ARM resource ID → `Resource.id`; resource type string → normalized `type` (e.g. `Microsoft.Compute/virtualMachines` → `compute.vm`) |
| **2. On-prem / local Kubernetes** | Current `kubeconfig` context: nodes, namespaces, workloads, PVs | Whatever `kubectl` context is active | See on-prem specifics below — no cloud API to lean on, so discovery is entirely `kubectl`-native |
| **3. AWS** | Account → region → resources (EC2, EKS, Lambda, S3, …) | `aws sts get-caller-identity` context | ARN → `Resource.id`; service+resource-type → normalized `type` |
| **4. GCP** | Project → resources (GCE, GKE, Cloud Functions, …) | `gcloud config` active project | Resource name path → `Resource.id`; GCP resource kind → normalized `type` |

Each adapter implements one function: `discover(provider) -> Resource[]`. Downstream
skills never branch on provider — they only read the normalized schema. The three
cloud reference architectures ([Azure](https://app.notion.com/3b8059b703e181f79bbdf17bb5880809),
[AWS](https://app.notion.com/3b8059b703e1811bade9e7fc8dc10c6d),
[GCP AI/ML](https://app.notion.com/3b8059b703e181b09afffa0f5f3b6e6b)) agree on the
same two-tier shape underneath the provider-specific services — a **control plane**
(orchestration, policy, golden paths) sitting over a **resource plane** (the actual
compute/data/network) — which is exactly the split `resource.schema.json` encodes:
control-plane objects (e.g. the IDP orchestrator itself, CI/CD) are `Resource.type`
values just like any VM, so the inventory can represent the platform's own control
surface, not only tenant workloads.

## On-prem/local Kubernetes: why it needs its own adapter, not a Kubernetes-generic one

On-prem clusters have no cloud API to enumerate "the account's resources" — the
cluster *is* the account, and its physical/operational context matters for
discovery in ways managed Kubernetes hides ([*The On-Prem Kubernetes Reality
Check*](https://app.notion.com/3b8059b703e181bca58ad42fd63e63f9)):

- **System size** — node count and capacity aren't elastic; discovery should record
  static capacity, not assume autoscaling exists.
- **System location** — data-center/rack locality matters for latency and sovereignty
  reasoning downstream (feeds `platform-blueprint`'s sovereignty axis).
- **Operating system** — `kubeadm`-deployed clusters vary OS/kernel per node in ways
  managed offerings normalize away; record it, since it affects what security/patch
  posture `architect-permissions-mapper` can assume.
- Troubleshooting on-prem discovery gaps (nodes that don't report, `NotReady` nodes,
  stale kubeconfig contexts) should degrade to a partial inventory with a warning,
  not fail the whole run — on-prem is the provider most likely to be flaky mid-scan.

## Resource type taxonomy (normalization targets)

Every adapter must resolve into a small, closed set of `type` values so downstream
skills can pattern-match without provider branching. Minimum v1 set, informed by
what actually recurs across the cloud reference architectures and the Kubernetes
material: `compute.vm`, `compute.container-host` (node), `k8s.cluster`,
`k8s.namespace`, `k8s.deployment`, `k8s.statefulset`, `k8s.job`, `k8s.cronjob`,
`storage.bucket`, `storage.persistent-volume`, `network.load-balancer`,
`network.dns-zone`, `identity.service-account`, `platform.control-plane` (the IDP
orchestrator/portal itself, if discovered as infra-as-code). This list is expected
to grow; `architect-workload-catalog` consumes it, so changes should be additive.

## Ownership inference (feeds `owner_tag`)

Cloud resources rarely arrive with a clean owner field — this is the same gap FinOps
tagging strategy chapters treat as a first-class problem, not an afterthought
([*Cost Management and Best Practices*](https://app.notion.com/3b8059b703e18127a44bc503e014d619),
[*FinOps – How to Avoid a Bill Shock*](https://app.notion.com/3b8059b703e181d79e43c17079940cca)).
Discovery should populate `owner_tag` from, in priority order: (1) an explicit
`owner`/`team`/`cost-center` tag if present, (2) the IaC module path that created it
(from Terraform state, if reconciled above), (3) leave unset — never guess from
naming convention alone. Untagged resources are exactly what
`architect-permissions-mapper`'s `unowned` flag and `architect-work-sync`'s backlog
drafting will surface as gaps, so under-populating here (rather than fabricating an
owner) is the safer default.

## Discovery cadence and drift

Discovery is not a one-time import. Because declared state (Terraform) and live
state (API/`kubectl`) can diverge continuously, `discovered_at` timestamps should be
treated as a freshness signal the blueprint capstone (`architect-blueprint`) surfaces
explicitly — "inventory last refreshed N days ago" — rather than assuming a single
run stays valid.

## Addendum — agentic-era findings (policy as a discoverable resource)

The "[Three Layers of Enforcement](../../docs/idp-adp-architect/diagrams.md#3-three-layers-of-enforcement)"
pattern from the agentic-platform-engineering research (generation-time pattern
application → plan-time static analysis (tflint/Sentinel/OPA/Checkov) → runtime cloud
enforcement (Azure Policy assignments)) implies discovery shouldn't stop at compute/
storage/network resources: **policy assignments and initiatives themselves are
discoverable resources** the mapper needs to know about, normalized under a new
`type` value — `governance.policy-assignment` — so `architect-permissions-mapper` can
join "this resource has broad IAM access" with "and no runtime policy is actually
enforcing guardrails on it," which is a materially worse finding than either alone.
A concrete instance of this exact gap, worth using as the canonical example: an Azure
Policy *initiative* that is available in the tenant but not assigned to the relevant
scope — present in the tooling, not actually protecting anything
([Frameworks Only Matter When They Force Decisions — Example C](https://devblogs.microsoft.com/all-things-azure/frameworks-only-matter-when-they-force-decisions/)).
Add `discover_policy_assignments(provider) -> Resource[]` as a fifth adapter function
alongside the four in the provider matrix above; it is lower build priority than the
compute/network adapters but should land before `architect-permissions-mapper`'s
second pass (`orphaned`/`unowned` flags) needs it.

## Open questions

- Which Azure tenant/subscription and which Kubernetes context(s) to run against
  first (recommend a non-production one for the pilot).
- Whether to treat a missing Terraform state file as "no declared state" (skip
  reconciliation) or as a discovery error worth surfacing — leaning toward the
  former since not every org manages 100% of infra as code.
