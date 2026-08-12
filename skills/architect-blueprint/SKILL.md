---
name: architect-blueprint
description: Capstone skill — reads every .platform/** artifact plus platform-blueprint's reference model and renders one organization-specific IDP/ADP blueprint document (Markdown or Notion), scored against an agentic-DevOps maturity rubric. Use when synthesizing discovery, persona, workload, product, permissions, and work-tracking findings into a single reviewable deliverable for platform leadership.
status: planned
---

# Architect: Blueprint

**Status:** Planned, not yet implemented. See [../../docs/idp-adp-architect/PLAN.md](../../docs/idp-adp-architect/PLAN.md) for the full domain plan.

## Role in the Architect tier

This is the only Architect-tier skill with no upstream consumer — it exists purely
to synthesize. Every other `architect-*` skill produces a normalized artifact for
the *next* skill to consume; this one produces the artifact a *human* consumes: a
rendered blueprint document that reads like a specific organization's answer to
`platform-blueprint`'s generic reference model, backed by the agentic-DevOps
maturity findings from this session's research.

## Reads

All of `.platform/**` — `inventory/resources.json`, `identity/bindings.json`,
`personas/personas.yaml`, `workloads/*.yaml`, `catalog/products.yaml`,
`worktracking/links.json` — plus `platform-blueprint`'s five-plane model as the
document's organizing skeleton.

## Writes

A rendered Markdown (or Notion, if the org's work-tracking adapter target is
Notion-shaped) blueprint document — not a `.platform/**` schema object, since
nothing downstream consumes it. The document's own structure is defined below.

## Document skeleton

Render one section per plane from `platform-blueprint`, each populated with this
organization's actual data, followed by the three synthesis sections below:

1. **Developer Control, Integration & Delivery, Resource, Security, Observability**
   (and Data & Model Management, if AI/ML workloads were discovered) — for each
   plane: which discovered personas own it, which products/golden paths live on
   it, and which flagged findings (over-privileged bindings, unowned resources)
   sit on it unresolved.
2. **Maturity assessment** (below).
3. **Findings register** — every open flag from `architect-permissions-mapper`
   and every unresolved `WorkItem` from `architect-work-sync`, joined by
   `linked_entity` so a reader sees "this resource is over-privileged *and* has an
   open ticket" or "over-privileged *and no ticket exists yet*" as one row, not two
   unrelated lists.
4. **Sovereignty read** — `platform-blueprint`'s sovereignty axis, evaluated
   against what was actually discovered (self-hosted vs. managed control-plane
   dependencies, open-core vs. foundation-governed IaC tooling in use).

## The three-act framing for how this document should read

The research behind this domain plan describes agentic platform engineering as a
progression through three acts, and the blueprint document's narrative arc should
mirror it rather than presenting a flat feature list:

- **Act One — Platform-aware assistance.** The agent (Copilot or equivalent) has
  context about the platform's patterns but only *assists* a human who is still
  driving. In blueprint terms: personas and products exist, but `architect-work-sync`
  is only ever human-initiated.
- **Act Two — Agentic enforcement.** Guardrails encoded as policy are enforced
  automatically at generation/plan/runtime — see
  [Diagram 3](../../docs/idp-adp-architect/diagrams.md#3-three-layers-of-enforcement).
  In blueprint terms: `architect-permissions-mapper`'s flags are consistently
  resolved before merge, not discovered after the fact.
- **Act Three — Agent-assisted operations.** Agents like the Cluster Doctor
  ([Diagram 8](../../docs/idp-adp-architect/diagrams.md#8-cluster-doctor--event-driven-remediation-workflow))
  operate the platform directly — monitoring, diagnosing, and drafting fixes —
  with humans reviewing rather than initiating. In blueprint terms:
  `architect-work-sync`'s adapters are wired to monitoring events, not just to
  discovery runs.

([Agentic Platform Engineering with GitHub Copilot](https://devblogs.microsoft.com/all-things-azure/agentic-platform-engineering-with-github-copilot/))
The blueprint document should state, per plane, which act the organization is
actually operating in today — not which act its tooling is *capable* of, which is
the gap most self-assessments get wrong.

## GitHub (or equivalent) as the control plane

A repeated finding across the research: in a maturing agentic platform, the
source-control system itself becomes the control plane, with compliance enforced
across five layers — **Context** (curated docs/policies the agent can read),
**Instruction** (repo/org-level custom instructions encoding guardrails in natural
language, versioned alongside code), **Agent** (custom agents bundling
instructions + skills + context into one coherent unit), **Validation** (CI +
org rulesets, e.g. Defender for DevOps scanning IaC before merge), and **Cloud
enforcement** (runtime policy — Azure Policy or equivalent — as the final
backstop). This five-layer model is a *finer-grained* decomposition of
[Diagram 3](../../docs/idp-adp-architect/diagrams.md#3-three-layers-of-enforcement)'s
three enforcement layers, splitting "Generation Time" into Context+Instruction+Agent
and leaving Plan Time / Runtime as Validation / Cloud enforcement. The blueprint
document should use whichever granularity matches what was actually discovered —
five layers if the org has repo-level custom instructions and agents, three if it
only has plan-time/runtime policy so far.

## The Cluster Doctor pattern as the capstone's worked example

Rather than describing `architect-infra-discovery`, `architect-permissions-mapper`,
and `architect-work-sync` as three independent skills in the rendered document, use
the Cluster Doctor pattern as one connected narrative thread that shows how their
outputs actually compose: Argo CD (discovered by `architect-infra-discovery` as a
control-plane resource) detects a degraded app → the event reaches GitHub via
`repository_dispatch` → an issue is opened (this *is* `architect-work-sync`'s
adapter output) → an agent diagnoses using the in-cluster MCP server (querying data
`architect-infra-discovery` and `architect-permissions-mapper` produced) → a human
approves the fix. See
[Diagrams 7–9](../../docs/idp-adp-architect/diagrams.md#7-app-of-apps-gitops-promotion-flow)
for the full three-part flow (GitOps promotion → remediation event flow →
`repository_dispatch` sequence detail).

## Framework-assessment loop as the blueprint's self-check

Before presenting the blueprint as finished, run it through the same
assess-remediate-reassess loop the Git-Ape framework-enforcement pattern describes:
review the discovered IaC/config against a named framework (Azure Well-Architected
Framework, NIST SP 800-53 Rev. 5 via policy, or CAF naming/tagging), get a
prioritized findings list scored per pillar, update code/policy, then reassess to
confirm measurable improvement — rather than treating the blueprint as a one-time
snapshot
([Frameworks Only Matter When They Force Decisions](https://devblogs.microsoft.com/all-things-azure/frameworks-only-matter-when-they-force-decisions/)).
A blueprint that scores an organization's WAF Security pillar at 2.5/10 (the "SSH
open to `0.0.0.0/0`" tier of finding from that research's worked example) should
say so plainly in the findings register, not soften it into a generic
recommendation. **Available-but-not-assigned** policy initiatives — the Example C
gap in the same research — are exactly what
`architect-infra-discovery`'s policy-assignment addendum now discovers, so the
blueprint should be able to name this exact failure mode from real data, not just
in the abstract.

## Maturity assessment (four-level rubric)

Score the organization against the Agentic DevOps Maturity Model across four
dimensions — **Foundations, Agent Adoption, Pipeline Maturity, Governance** — each
scored **Reactive → Foundation → Structured → Optimized**:

| Level | Foundations | Agent Adoption | Pipeline Maturity | Governance |
|---|---|---|---|---|
| Reactive | Ad hoc standards, tribal knowledge | No agents, or unmanaged/ungoverned experimentation | Manual gatekeeping, pipelines as afterthought | No consistency/auditability requirements |
| Foundation | Checklisted foundations exist but aren't enforced | Agents used ad hoc by individuals | Pipelines exist but verify structure only | Scope of agent action undefined |
| Structured | Foundations checklist enforced org-wide | Org-level + repo-level agents with defined skill profiles | Layered verification (structural + semantic + provenance) | Consistency and scope control enforced; auditability designed in |
| Optimized | Foundations continuously re-validated | Agents operate with human-review gates, not human-initiation | Pipeline is an active verifier, not a passive gate | Full auditability; productivity metrics reframed around outcomes, not activity |

([Agentic DevOps: Practices, Principles, and Strategic Direction](https://devblogs.microsoft.com/all-things-azure/agentic-devops-practices-principles-strategic-direction/))
This table should be filled in per-dimension from real discovered signal wherever
possible — e.g. "Agent Adoption: Structured" is only justifiable if
`architect-persona-generator` actually found org-level *and* repo-level agent
personas with distinct scopes, not merely because the org has a Copilot license.

## The lifecycle loop the blueprint should close

The rendered document's closing section should map back onto the six-stage
agentic operations loop —
[Diagram 5](../../docs/idp-adp-architect/diagrams.md#5-agentic-operations-loop-define--generate--validate--deploy--operate--learn)
(Define → Generate → Validate → Deploy → Operate → Learn) — naming, for each
stage, whether it is currently human-driven or AI-assisted at this organization,
and what would need to change to move it one step further along. The recurring
split in that diagram — "Humans control POLICY, AI handles EXECUTION" — is the same
split every other `architect-*` skill's approval gates already encode; the
blueprint's job is to say it out loud as an explicit organizational maturity
statement rather than leaving it implicit in five different skills' flag rules.

## Addendum — Radius as a blueprint validation/emission target

[Radius](https://docs.radapp.io/) contributes a grammar this capstone can validate
discovered/generated topology against, or optionally emit into, when an organization
has Radius available as its application platform. Its core abstractions — **Environment**
(landing zone: compute/providers/credentials/Recipes; targets a K8s namespace, an AWS
account/region, or an Azure subscription/resource group), **Application** (the parent
Bicep resource, e.g. `Applications.Core/applications@2023-10-01-preview`), and **Resource
Type** (a versioned infra-agnostic API such as `Applications.Datastores/redisCaches` or
`Applications.Core/containers`) — together form a typed application-topology grammar
richer than this plugin's own `Workload`/`Product` pair
([Application concepts](https://docs.radapp.io/concepts/applications/);
[Environment concepts](https://docs.radapp.io/concepts/environments/);
[Resource Type concepts](https://docs.radapp.io/concepts/resource-types/)).

**Recipe / Recipe Pack as the resource-fulfillment check.** A **Recipe** is a versioned
Bicep or Terraform template that implements a Resource Type for a specific Environment;
a newer **Recipe Pack** (`Radius.Core/recipePacks@2025-08-01-preview`) groups Recipe
definitions for reuse across Environments — note that `rad env update --recipe-packs` is
still **preview** as of this research, so a blueprint should flag Recipe Pack usage as an
experimental-tooling finding, not treat it as a stable baseline. Before this capstone
reports a workload/product as deployable, it should validate that a Recipe actually
exists for every logical resource type the workload declares, in every target
Environment — a Radius Application with no matching Recipe in a given Environment is a
finding this document should surface in the Findings register, the same way an unowned
resource or an over-privileged binding is
([Recipes concepts](https://docs.radapp.io/concepts/recipes/);
[Recipe Pack schema](https://docs.radapp.io/reference/resources/radius/radius.core/2025-08-01-preview/recipepacks/)).

**Positioning relative to this plugin's own schema.** Radius's typed graph is a stronger
validation/emission target than a general replacement for `.platform/**` — it should be
consumed where an org already runs Radius, not proposed as a new mandatory dependency for
orgs that don't. See
[../../docs/idp-adp-architect/workload-spec-components.md](../../docs/idp-adp-architect/workload-spec-components.md)
for the full plane-by-plane split across Score, Radius, Kratix, and Dapr.

## Depends on

`architect-infra-discovery`, `architect-permissions-mapper`,
`architect-persona-generator`, `architect-workload-catalog`,
`architect-product-catalog`, `architect-work-sync`
