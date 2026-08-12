---
name: architect-workload-catalog
description: Groups discovered resources into Score-style workload definitions with a closed type taxonomy (web-service, batch-job, ml-training, data-pipeline). Use when normalizing raw infrastructure into meaningful application-level units, defining what "a workload" means for a specific platform, or scoping autoscaling/resource-request defaults per workload type.
status: planned
---

# Architect: Workload Catalog

**Status:** Planned, not yet implemented. See [../../docs/idp-adp-architect/PLAN.md](../../docs/idp-adp-architect/PLAN.md) for the full domain plan.

## Role in the Architect tier

`architect-infra-discovery` produces a flat bag of `Resource` objects — a
Deployment here, a LoadBalancer there, no notion that they belong together. This
skill's job is the grouping step: turn N related resources into 1 `Workload`, in
the same spirit as a [Score](https://score.dev) spec — declarative, workload-centric,
resource-agnostic underneath.

## Reads

`.platform/inventory/resources.json` (from `architect-infra-discovery`) and
`.platform/identity/bindings.json` (from `architect-permissions-mapper`, for
`owner_persona` resolution).

## Writes

`.platform/workloads/*.yaml` — one file per `Workload` object per
`.platform/schema/workload.schema.json` (`id`, `type`, `spec`, `resources`,
`owner_persona`), where `spec` is a Score-style body.

## Grouping heuristic

A `Workload` is the smallest set of `Resource.id` references that must be
deployed, scaled, and rolled back together to keep one running application
healthy. Practically: start from a compute resource (`k8s.deployment`,
`k8s.statefulset`, `compute.vm`), then pull in everything that resource's
discovered tags/owner reference — its Service, its PersistentVolumeClaim, its
attached load balancer — into the same `resources` array. A `k8s.cronjob` or
`k8s.job` with no attached Service is its own workload (a batch job doesn't need
one). Resources with no clear compute anchor (an orphaned storage bucket, a
dangling DNS zone) should not be force-fit into a workload — leave them
unassigned and let `architect-permissions-mapper`'s `unowned` flag surface them
instead of hiding them inside a workload that doesn't actually use them.

## Type taxonomy (the schema's `type` field)

The schema names four types as the v1 minimum: `web-service`, `batch-job`,
`ml-training`, `data-pipeline`. Each has a distinct resource-request and
autoscaling shape worth encoding as a default `spec` template rather than leaving
every workload to define its own from scratch:

| Type | Typical resource shape | Autoscaling default |
|---|---|---|
| `web-service` | Deployment + Service + (optional) Ingress/LoadBalancer | HPA on CPU/request-rate; Karpenter/cluster-autoscaler for node capacity |
| `batch-job` | Job or CronJob, no Service | No HPA — scale by parallelism/completions, not live traffic |
| `ml-training` | Job with GPU resource requests, often a PVC for checkpoints | No HPA; scale via job parallelism or a queue-depth-driven KEDA ScaledObject |
| `data-pipeline` | StatefulSet or Job chain, PVC, often a message broker dependency | KEDA ScaledObject on queue depth, not CPU |

The `web-service` autoscaling default above is a direct reuse of a worked example —
deploy a Karpenter NodePool, deploy the application, then a KEDA ScaledObject —
rather than a generic HPA-only setup
([*Practical Use Cases for Autoscaling in Kubernetes*](https://app.notion.com/3b8059b703e1813da74cea3e6e569718)).
This list is expected to grow (mirroring `architect-infra-discovery`'s resource
`type` taxonomy); additions should stay additive so `architect-product-catalog`'s
`workload_types` references don't break.

## Why resource requests/limits are catalog-relevant, not just runtime tuning

A `Workload.spec` that omits resource requests/limits isn't a neutral default —
the Kubernetes scheduler treats an unset request as "assume the smallest possible
footprint," which routinely causes noisy-neighbor and OOM problems the moment the
workload's real usage diverges from that assumption
([*Workload Autoscaling Overview*](https://app.notion.com/3b8059b703e1818d81e2d0c7fc95e4a5)).
The catalog generator should therefore populate `spec` with requests/limits
inferred from live usage where discovery can observe it (metrics-server data, if
reachable), and flag — not silently default — any workload where no observed usage
exists yet to base an inference on.

## Troubleshooting posture the catalog should carry forward

Workloads that already have HPA/VPA objects attached should have their
autoscaler's *health*, not just its target spec, reflected somewhere reachable
from the catalog entry — a `Workload` pointing at an HPA that's stuck because its
underlying Metrics Server is failing is a materially different situation from one
that's healthy but simply hasn't scaled recently, and `architect-blueprint`'s
capstone narrative should be able to tell the two apart
([*Workload Autoscaling Operations*](https://app.notion.com/3b8059b703e1814baa80c1e3c5dece78)).

## Addendum — Score as the portable workload contract

[Score](https://docs.score.dev/docs/) is the closest existing implementation of what this
skill's `Workload.spec` field is already modeled on, and should be treated as the
direct reference (or literal ingestion format) for that field rather than a loose
inspiration. Score is a CNCF Sandbox project (accepted 2024-08-08) originated at
Humanitec; the spec itself is at release `0.4.1` (2026-05-25), `apiVersion:
score.dev/v1b1`, validated against a canonical JSON Schema (Draft 2020-12) that
requires `apiVersion`, `metadata`, and `containers` and rejects unknown top-level keys
([Score spec reference](https://docs.score.dev/docs/score-specification/score-spec-reference/);
[CNCF Sandbox acceptance](https://www.cncf.io/blog/2024/08/08/score-accepted-as-a-cncf-sandbox-project/);
[canonical JSON Schema](https://github.com/score-spec/spec/blob/main/score-v1b1.json)).

**Resource model — directly reusable for the `resources` array.** Score's
`resources.<name>` block is `type` (required — an abstract kind like `postgres`,
`redis`, `dns`, `route`, `volume`; not a concrete chart or instance), `class`
(optional, default `"default"`), `id` (optional — identical `type`+`class`+`id`
across workloads means one shared resource, provisioned once, not duplicated), and
`params` (an open object that may reference placeholders like
`${resources.db.host}` or `${metadata.name}`). Resource evaluation forms an acyclic
dependency graph. There is no portable `secret:true` marker in the spec itself —
secrecy is translator-specific, so a discovered `${resources.*}` reference should not
be assumed safe to log verbatim just because the spec doesn't flag it
([Score spec reference](https://docs.score.dev/docs/score-specification/score-spec-reference/)).

**Translator matrix — what actually turns `score.yaml` into a running workload.**
Score itself is not a deployment platform; a separate translator does the binding:

| Translator | Target | Status |
|---|---|---|
| `score-compose` | Docker Compose | Reference/active; broadest default resource catalog (postgres, redis, mysql, mongodb, amqp, kafka-topic, s3, dns, route, volume, service-port) |
| `score-k8s` | Kubernetes | Reference/active; narrower default catalog, cleanup not fully implemented |
| `score-helm` | Helm | **Explicitly deprecated upstream — do not use as a translator baseline for new work** |
| Humanitec / `humctl` | Humanitec managed platform | Native binding to Resource Definitions via `humctl score deploy` |

([score-compose README](https://github.com/score-spec/score-compose/blob/main/README.md);
[score-k8s README](https://github.com/score-spec/score-k8s/blob/main/README.md);
[score-helm README](https://github.com/score-spec/score-helm/blob/main/README.md);
[Humanitec Score overview](https://developer.humanitec.com/app-humanitec-io/docs/score/overview/))

**Explicit non-scope — why this skill still owns grouping/typing.** Score's own
documentation disclaims policy/compliance, observability, CI/CD/GitOps, secrets
standardization, full application/product topology, and infra lifecycle/cleanup as
out of scope. In this plugin's terms: Score is the portable *deployable-workload
contract* feeding this skill's `Workload.spec`, not a replacement for
`architect-product-catalog`'s product-level concerns or `architect-permissions-mapper`'s
security findings. See
[../../docs/idp-adp-architect/workload-spec-components.md](../../docs/idp-adp-architect/workload-spec-components.md)
for how Score, Radius, Kratix, and Dapr divide up this plugin's five planes.

## Depends on

`architect-infra-discovery`
