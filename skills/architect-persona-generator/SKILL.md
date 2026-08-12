---
name: architect-persona-generator
description: Clusters discovered identity bindings and org group data into discrete platform personas mapped onto the five-plane model, including emerging agent personas (Cluster Doctor, coding agents). Use when defining who a platform serves, building a persona-aware onboarding flow, or scoping which stakeholders a golden path must satisfy.
status: planned
---

# Architect: Persona Generator

**Status:** Planned, not yet implemented. See [../../docs/idp-adp-architect/PLAN.md](../../docs/idp-adp-architect/PLAN.md) for the full domain plan.

## Role in the Architect tier

Turns a flat list of identity bindings into the small set of *roles* a platform
actually needs to design for. `platform-blueprint` already names the plane-owner
personas in the abstract (DevEx platform engineer, infrastructure platform engineer,
security platform engineer, observability platform engineer) — this skill is what
makes that table concrete for one specific organization: real group names, real
consumption/creation patterns, and — per the agentic-era research below — the
non-human personas that now sit inside the same access model as humans.

## Reads

`.platform/identity/bindings.json` (from `architect-permissions-mapper`) plus org
group data (Entra ID groups, GitHub teams, or equivalent) reachable via the same
authenticated CLIs already used for discovery.

## Writes

`.platform/personas/personas.yaml` — array of `Persona` objects per
`.platform/schema/persona.schema.json` (`name`, `plane`, `consumes`, `creates`,
`org_mapping`).

## Generation heuristic: cluster bindings, don't enumerate humans

A naive approach — one `Persona` per human principal — produces hundreds of
near-duplicate personas and misses the point. The generator should instead cluster
`IdentityBinding` records by **(role pattern, scope pattern, org_mapping)** and treat
each resulting cluster as a candidate persona, then let a human platform engineer
name/merge/split clusters before they're finalized. A cluster of 40 principals all
holding the same `Contributor`-equivalent role at namespace scope, sourced from one
Entra ID group, is one persona ("backend developer"), not 40. This mirrors how
`platform-blueprint` itself only names a handful of personas despite real
organizations having hundreds of engineers.

`org_mapping` is the join key back to the source group (an Entra ID group ID or
GitHub team slug) — keep it literal (not a display name) so
`architect-work-sync`'s adapters can resolve the same group when routing a drafted
ticket to the right team.

## Plane assignment

Map each persona cluster onto one of the five (or six, for AI/ML platforms) planes
from `platform-blueprint` using what the cluster **consumes** and **creates**, not
its job title — a "platform engineer" persona that only ever touches CI/CD config
and golden-path templates belongs on Integration & Delivery, not a generic
"Infrastructure" bucket:

| Plane | `consumes` (typical) | `creates` (typical) |
|---|---|---|
| Developer Control | golden paths, portal/CLI, provisioned resources with injected credentials | workload specs (Score-file PRs) |
| Integration & Delivery | IaC modules, CI templates | golden-path templates, pipeline definitions |
| Resource | — (usually consumed only by the platform, not a human persona) | — |
| Security | policy-as-code frameworks | RBAC bindings, policy assignments |
| Observability | dashboards, alert routing | SLOs, runbooks |
| Data & Model Management (AI/ML only) | feature store, model registry | model cards, experiment lineage |

## Non-engineer personas

Platform personas are not only engineers. Stakeholder-management material
consistently separates a **status-reporting cadence** persona set from the
hands-on-keyboard set — stand-up, status update, leadership review, and senior
leadership review are four distinct communication touchpoints with four different
personas on the receiving end, each needing a different level of detail
([*Driving Toward Clarity*](https://app.notion.com/3b8059b703e181a5b750d0fb86c76aa2)).
A platform's stakeholder list should itself be treated as generator input, not an
afterthought — projects that skip building an explicit stakeholder list are the ones
that discover a missing approver mid-rollout
([*Stakeholder Management*](https://app.notion.com/3b8059b703e1812fbd1ae84a45059da4)).

Two roles worth generating as first-class personas even when they hold no
`IdentityBinding` at all (their influence is organizational, not access-based):

- **Platform product manager / head of platform** — owns the Business Value pillar
  (developer experience, cost, risk, speed) and reconciles competing team asks
  against a shared roadmap
  ([*Understanding the Business Value of Platform Engineering*](https://app.notion.com/3b8059b703e18191bfa6c37e998128be)).
- **Executive sponsor** — the senior-leadership-review audience; without this
  persona named explicitly, the classic **minimum stakeholder commitment**
  anti-pattern recurs at every migration or platform re-architecture
  ([*Migrating from Legacy Systems to Cloud Native Solutions*](https://app.notion.com/3b8059b703e181109403cd16080c5370)).

A **Technical Program Manager** persona is worth generating explicitly whenever the
org has one: TPMs sit across project planning, resource management, risk management,
and communication — a horizontal role that most persona-clustering heuristics (which
key off *access*) will otherwise miss entirely, since a TPM often holds minimal
platform RBAC
([*Pillars of a Technical Program Manager*](https://app.notion.com/3b8059b703e181979b4ecbf60f3c5436)).
Cloud-native transformation work specifically calls out stakeholder alignment as its
own workstream, distinct from the technical migration plan
([*Transitioning to Cloud Native Good Habits*](https://app.notion.com/3b8059b703e181de8f8ded91cc3ff87e)).

## Agent personas — the newest persona class

The agentic-platform-engineering research (this plugin's newest source set) makes a
case that **AI agents are personas now, not tools**, and should be generated with
the same rigor as human ones:

- **Org-level agent** — holds enterprise-wide standards (security baselines, naming
  conventions, network topology, compliance rules); every repo-level agent persona
  inherits from it by default. This is a direct visual analogue of `org_mapping`:
  see [Diagram 4](../../docs/idp-adp-architect/diagrams.md#4-org-level--repo-level-agent-inheritance)
  ([Platform Engineering for the Agentic AI Era](https://devblogs.microsoft.com/all-things-azure/platform-engineering-for-the-agentic-ai-era/)).
- **Repo-level agent** (e.g. `@payments-infra-agent`, `@data-infra-agent`) — a
  narrower persona scoped to one codebase's patterns and deployment targets,
  generated the same way a human team's persona is generated: cluster its bindings,
  inherit from the org-level agent, name it after the repo/team it serves.
- **Cluster Doctor / remediation agent** — a persona triggered by monitoring events
  (Argo CD notification → GitHub Issue → label or human-assignment → agent diagnosis
  → PR), not by a human logging in. Its `creates` field should include draft PRs and
  issue comments, never merged changes — the human-review step is structural, not
  optional (step 7 in
  [Diagram 8](../../docs/idp-adp-architect/diagrams.md#8-cluster-doctor--event-driven-remediation-workflow))
  ([Agentic Platform Engineering with GitHub Copilot](https://devblogs.microsoft.com/all-things-azure/agentic-platform-engineering-with-github-copilot/)).

The Agentic DevOps research names three **emerging human responsibilities** that
should be generated as personas alongside the agent personas above, since they
exist specifically to govern agent personas:

- **System Designer** — defines the specifications and skill profiles agents work
  from (the `.github/copilot-instructions.md` layer).
- **Agent Operator** — manages the fleet of active agents, their scope, and their
  kickoff triggers (label-based, human-assignment, or scheduled).
- **Quality Steward** — owns the verification layer (structural, semantic, and
  provenance checks) that gates an agent's output before merge.

([Agentic DevOps: Practices, Principles, and Strategic Direction](https://devblogs.microsoft.com/all-things-azure/agentic-devops-practices-principles-strategic-direction/))

## Depends on

`architect-permissions-mapper`
