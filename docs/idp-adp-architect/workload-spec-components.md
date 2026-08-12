# Workload-Spec Components — Score, Radius, Kratix, Dapr

**Status:** Research complete, findings woven into `architect-*`/`platform-*` skills (see cross-references below).
**Companion research artifacts (offline, not yet committed to this repo):** `/home/user/workspace/pe_plugin_research/{score,radius,kratix,dapr}_deepdive.md`, each with a full raw-source archive (`repos/`, `raw/`) captured at a pinned commit so the underlying evidence survives without network access.

## Why this doc exists

The original ask was to deep-dive four candidate "workload specification" projects — [Score](https://docs.score.dev/docs/), [Radius](https://docs.radapp.io/), [Kratix](https://docs.kratix.io/), and [Dapr](https://docs.dapr.io/) — with an explicit caveat: **none of the four is a complete platform, and no single one will be used wholesale.** Each is a *component* that can fulfill part of one or more of this plugin's five planes (Developer Control, Integration & Delivery, Resource, Security, Observability — per `platform-blueprint`) or part of the `.platform/**` schema (`Workload`, `Product`, `IdentityBinding`, `WorkItem`) defined in [PLAN.md](./PLAN.md). This doc is the cross-cutting map; the actual adoption guidance lives inline in each affected SKILL.md, addenda-style, matching the pattern already used for the agentic-era research in `architect-permissions-mapper`.

## One-line positioning per project

| Project | One-line role | NOT this |
|---|---|---|
| [Score](https://docs.score.dev/docs/) | Portable developer-facing workload contract (`score.yaml`) — declares what a workload needs | Not a deployment platform, not a provisioner, no built-in policy/observability/CI |
| [Radius](https://docs.radapp.io/) | Kubernetes-hosted application platform with a typed application graph (Bicep) + environment-scoped Recipes | Not a workload-spec *language* in Score's narrow sense; heavier, opinionated about topology |
| [Kratix](https://docs.kratix.io/) | Platform-capability API builder + GitOps delivery plane (Promise → Work → WorkPlacement → Destination) | Not a workload spec at all — it's how a platform *fulfills* a request for a capability a workload needs |
| [Dapr](https://docs.dapr.io/) | Day-2 sidecar runtime for distributed-application concerns (state, pub/sub, secrets, workflow, actors) | Not a provisioner, catalog, or delivery controller — assumes the workload is already scheduled |

## Plane-by-plane mapping

### Developer Control plane

- **Score** is the most direct fit: `score.yaml` *is* the developer-control artifact — a workload author declares `containers`, `resources`, and dependency `params` without knowing which translator (score-compose/score-k8s/Humanitec) will realize it. Feeds `architect-workload-catalog`'s `Workload.spec` field directly as the Score-style body the schema already names. ([Score spec reference](https://docs.score.dev/docs/score-specification/score-spec-reference/))
- **Radius** gives developers a richer authoring surface (Bicep application graph) at the cost of being Kubernetes/Radius-specific rather than translator-agnostic; it is the developer-control layer to offer *if* the org has already committed to Radius as its application platform, not a default. ([Radius Application concepts](https://docs.radapp.io/concepts/applications/))
- **Kratix** sits one layer up from both: it is what a developer uses to request a *capability* (a database, a namespace, an environment) that a Score workload or Radius application then depends on — the CRD instance a developer submits (e.g. `Database`) is itself a developer-control-plane artifact, just not a workload-shape one. ([Promise reference](https://docs.kratix.io/main/reference/promises/intro))

### Resource plane

- **Score**'s `resources.<name>` block (`type`/`class`/`id`/`params`) is a portable *reference* to a resource, not the provisioner — the score-compose/score-k8s/Humanitec translator does the actual binding. This maps cleanly onto `architect-workload-catalog`'s existing `resources[]` array on the `Workload` entity.
- **Radius**'s Recipe/Recipe Pack mechanism is the resource plane's most complete answer among the four: a Recipe is a versioned Bicep/Terraform implementation bound per-Environment, and the Connection edge tracks consumer→dependency intent with an optional IAM role list (Azure-only today). This is a validation target for `architect-blueprint`, not a replacement for `architect-infra-discovery`'s live-discovery role. ([Recipes concepts](https://docs.radapp.io/concepts/recipes/))
- **Kratix** is the resource plane's *fulfillment engine* rather than a resource description format: a Promise's workflow Pipeline is free to call Terraform, a cloud CLI, or an internal system, and the declared output becomes a `Work` scheduled to a `Destination`'s GitOps agent. Treat Kratix output as generated, not hand-edited — this is the `architect-work-sync` linkage described below. ([Kratix internal objects](https://docs.kratix.io/main/platform-concepts/kratix-resources))
- **Dapr**'s Component resource is explicitly *not* proof of provisioning — it is a binding/configuration reference to a resource that must already exist. Dapr contributes the workload's runtime contract to an already-provisioned Redis/Kafka/Vault, nothing upstream of that. ([Dapr components concept](https://github.com/dapr/docs/blob/f5d0b6d/daprdocs/content/en/concepts/components-concept.md))

### Security plane

- **Radius**'s Connection `iam.kind: 'azure'` role automation is the clearest identity-intent signal among the four — but it is Azure-only, and must be modeled distinctly from the *control-plane's own* deployment identity (Azure Workload Identity / AWS IRSA), which is a separate principal. This is the primary addendum woven into `architect-permissions-mapper` below.
- **Dapr** contributes a workload-level permission graph that is additive to, not a replacement for, Kubernetes RBAC/cloud IAM: mTLS via Sentry, component/secret/pubsub `scopes`, service-invocation ACLs, and `WorkflowAccessPolicy`. Woven into `platform-security` below.
- **Kratix**'s security surface is mostly about *pipeline* trust (pinned/scanned/signed OCI images running as Kubernetes Jobs with a service account) rather than workload identity — a distinct concern from both Radius's and Dapr's, worth a future `architect-permissions-mapper` addendum once Kratix adoption is real (not written yet; flagged as a gap below).

### Integration & Delivery / CI/CD plane

- **Kratix** is the strongest fit: Promise → Work → WorkPlacement → Destination is a GitOps delivery pipeline by construction, and the marketplace ships pre-built Promises for ArgoCD, cert-manager, Vault, Dapr itself, and others. Woven into `architect-work-sync` below — this is a genuinely new delivery-state synchronization pattern, not a restatement of the existing Argo CD/`repository_dispatch` pattern already documented there.
- **Score**'s translators (score-compose, score-k8s) are themselves lightweight CI/CD-adjacent tools — they render a workload spec into a deployable form — but Score explicitly disclaims owning CI/CD/GitOps as a concern.
- **Radius**'s `rad deploy` / environment model is delivery-adjacent but assumes Radius as the runtime; less relevant to this plugin's system-agnostic CI/CD story than Kratix's GitOps-native design.

### Observability plane

- **Dapr** is the only one of the four with native telemetry emission relevant here: OpenTelemetry/Zipkin-compatible tracing (W3C Trace Context propagated at the sidecar) and Prometheus-formatted metrics, for every Dapr-mediated call and Workflow execution — without requiring per-service instrumentation code. This is a genuine addition to `platform-observability`'s existing OTel-standardization story, with one hard caveat: Dapr is a **native emitter, not a native backend** — Grafana/Jaeger/OTEL Collector still have to exist externally. Woven in below.
- Score, Radius, and Kratix have no comparable native telemetry story for this plugin's purposes (Radius's Dashboard is a topology UI, not an observability backend; Kratix has Promise/Work/WorkPlacement status/conditions, which is closer to delivery-state tracking than telemetry).

## Cross-references — where each finding actually landed

| Finding | Woven into |
|---|---|
| Score `score.yaml` as the portable workload contract; translator matrix | [`architect-workload-catalog/SKILL.md`](../../skills/architect-workload-catalog/SKILL.md) |
| Radius Connection as an intent edge; Azure-only IAM automation; control-plane vs. workload identity distinction | [`architect-permissions-mapper/SKILL.md`](../../skills/architect-permissions-mapper/SKILL.md) |
| Radius Bicep application-topology grammar + Recipe/Recipe Pack validation target | [`architect-blueprint/SKILL.md`](../../skills/architect-blueprint/SKILL.md) |
| Kratix Promise as a catalog product's fulfillment backend | [`architect-product-catalog/SKILL.md`](../../skills/architect-product-catalog/SKILL.md) |
| Kratix Promise → Work → WorkPlacement → Destination GitOps delivery lifecycle | [`architect-work-sync/SKILL.md`](../../skills/architect-work-sync/SKILL.md) |
| Dapr native OTel/Prometheus emission, external-backend caveat | [`platform-observability/SKILL.md`](../../skills/platform-observability/SKILL.md) |
| Dapr mTLS/Sentry, component/secret/pubsub scopes, WorkflowAccessPolicy | [`platform-security/SKILL.md`](../../skills/platform-security/SKILL.md) |
| Full citation index for all four projects | [`research/SOURCES.md`](../../research/SOURCES.md) |

## Known gap

Kratix's pipeline-image supply-chain security model (pinned/scanned/signed OCI images, least-privilege workflow service accounts) has no current home in `architect-permissions-mapper` — it doesn't fit the `IdentityBinding` schema cleanly (it's about *pipeline* execution trust, not principal-to-resource bindings). Revisit once real Kratix adoption surfaces a concrete need, rather than force-fitting it into the existing flag rules now.

## Maturity/versioning caveats worth remembering across all four

- **Score**: CNCF Sandbox since 2024-08-08; spec `0.4.1` (2026-05-25); score-helm is explicitly deprecated upstream — do not use it as a translator baseline. ([CNCF Sandbox acceptance](https://www.cncf.io/blog/2024/08/08/score-accepted-as-a-cncf-sandbox-project/), [score-helm README](https://github.com/score-spec/score-helm/blob/main/README.md))
- **Radius**: CNCF Sandbox (not Incubating/Graduated); latest stable `v0.59.0` (2026-06-18); two API generations coexist (`Applications.Core/*@2023-10-01-preview` vs. `Radius.Core/*@2025-08-01-preview`) and must be tracked as distinct `(type, apiVersion)` pairs, not normalized away. ([Radius README](https://github.com/radius-project/radius/blob/89f7c62e5048d25eee75414d977b0178330353f5/README.md))
- **Kratix**: **not verified as a CNCF project** — do not label it CNCF Sandbox; API surface is still `v1alpha1`; last numbered GitHub release is `v0.125.0` (2024-07-08). ([OpenUK Syntasso case study](https://openuk.uk/case-studies/case-study-syntasso/))
- **Dapr**: CNCF **Graduated** (2024-10-30); stable `v1.18.2` (2026-07-21) — the most mature project of the four by governance status. ([CNCF graduation announcement](https://www.cncf.io/announcements/2024/11/12/cloud-native-computing-foundation-announces-dapr-graduation/))
