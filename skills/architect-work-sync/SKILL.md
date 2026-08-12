---
name: architect-work-sync
description: Adapter-based bridge from discovered platform entities (personas, workloads, permission gaps) to whatever work-tracking system the org already uses — Linear, Jira, GitHub, or Azure DevOps — detected at runtime. Never files a ticket silently; always drafts for human approval. Use when a discovered gap (unowned resource, over-privileged binding, missing workload owner) needs to become a tracked, assignable piece of work.
status: planned
---

# Architect: Work Sync

**Status:** Planned, not yet implemented. See [../../docs/idp-adp-architect/PLAN.md](../../docs/idp-adp-architect/PLAN.md) for the full domain plan.

## Role in the Architect tier

Every upstream `architect-*` skill produces findings, not actions: an unowned
resource, an over-privileged binding, a workload with no `owner_persona`. This
skill is the only one that writes *outward*, into whatever system the org's humans
actually work from — and it is deliberately the most conservative skill in the
tier: it drafts, it never silently files.

## Reads

`.platform/personas/personas.yaml`, `.platform/workloads/*.yaml`, and the flagged
subset of `.platform/identity/bindings.json` (from `architect-permissions-mapper`).

## Writes

`.platform/worktracking/links.json` — array of `WorkItem` objects per
`.platform/schema/work_item.schema.json` (`external_ref`, `system`, `linked_entity`,
`status`). The `WorkItem` itself is a *link record*, not the drafted ticket content —
drafted-but-not-yet-approved tickets should live in a separate `pending/` staging
area until a human approves them, at which point `external_ref` gets populated with
the real ticket ID/URL and `status` flips from `draft` to whatever the target
system reports.

## The non-negotiable rule

**Never file a ticket silently. Always draft for human approval first.** This
mirrors the human-review gate that appears as a structural, numbered step in every
agentic-remediation flow this plugin's research covers — it is not this skill's own
invention, it's the pattern the whole agentic-platform-engineering research set
converges on. Concretely: step 7 in
[Diagram 8](../../docs/idp-adp-architect/diagrams.md#8-cluster-doctor--event-driven-remediation-workflow)
("Human Developer/Platform Engineer reviews and approves the PR — or asks the agent
to modify") is the same gate this skill's `draft → approve → sync` lifecycle
implements, just for tickets instead of pull requests.

## Adapter matrix — detected at runtime, not hardcoded

| System | `WorkItem.system` value | Native concept `linked_entity` maps to | Detection signal |
|---|---|---|---|
| Linear | `linear` | Issue, in a Team's backlog | Linear API key/workspace present |
| Jira | `jira` | Issue, in a Project | Jira Cloud/Server API token present |
| GitHub | `github` | Issue (optionally with labels driving automation) | GitHub App/PAT with repo access |
| Azure DevOps | `azure-devops` | **Work item**, on a **Board**, inside a **Sprint** — Azure DevOps's own vocabulary is more granular than the schema's flat `WorkItem`, so the adapter should record the board/sprint context inside `status` or a system-specific extension field rather than dropping it | `az devops` CLI context or PAT present |

Azure DevOps is worth calling out specifically because its object model (Boards →
sprints → queries → process templates) is richer than the other three systems' flat
issue model — Azure Boards organizes work items through backlogs and boards with
configurable process templates, and treats sprints as a first-class scheduling unit
in a way Linear/Jira/GitHub only approximate
([*Managing Projects with Azure DevOps Boards*](https://app.notion.com/3b8059b703e1811ba90dd0010245d1a4);
overview: [*Azure DevOps Overview*](https://app.notion.com/3b8059b703e181128661e5b97a927bf3)).
Adapters should map *down* to the lowest common denominator (`WorkItem`'s four
fields) rather than forcing every other system to grow Azure DevOps's full
vocabulary.

## The concrete reference pattern: Argo CD → repository_dispatch → GitHub Issues → label-triggered agent → PR

This is the adapter example named in the domain plan, and it is not hypothetical —
it is a real, documented pattern from the research this plugin incorporates, and
the GitHub adapter above should implement it close to verbatim:

1. Argo CD detects a deployment failure or degraded app health.
2. Argo CD Notifications builds a custom payload (app name, cluster, resource
   group, region, failure reason, links, labels) and sends a `repository_dispatch`
   event to the GitHub repository.
3. A GitHub Actions workflow (`argocd-deployment-failure.yml`) starts, parses the
   payload, and checks for an existing open issue for the same failure before
   creating a new one — this idempotency check is the one step every other
   system's adapter must replicate: **never open a duplicate issue for the same
   underlying finding.**
4. The created/updated GitHub Issue becomes the shared incident record.
5. Either a `Cluster-Doctor` label auto-triggers a custom agent via the GitHub
   Copilot CLI, or a human explicitly assigns the Copilot Coding Agent to the
   issue — both are valid kickoff paths, and this skill's own draft-then-approve
   lifecycle should support both: an automated trigger drafting a ticket is fine,
   an automated trigger *merging or closing* one is not.
6. The agent uses an in-cluster MCP server to diagnose the issue, then pushes
   issue updates and a PR with a proposed solution back onto the same issue.
7. A human developer or platform engineer reviews and approves the PR — or sends
   the agent back to revise it. This is the gate this skill must never bypass.

Full sequence-diagram detail (the exact `repository_dispatch` payload shape and
the five-participant message flow) is captured in
[Diagram 9](../../docs/idp-adp-architect/diagrams.md#9-the-wiring--repositorydispatch-sequence-diagram);
the box/arrow version of the same flow, including the namespace/cluster grouping,
is [Diagram 8](../../docs/idp-adp-architect/diagrams.md#8-cluster-doctor--event-driven-remediation-workflow).
The App of Apps GitOps promotion flow that produces the deployments Argo CD is
watching in the first place is [Diagram 7](../../docs/idp-adp-architect/diagrams.md#7-app-of-apps-gitops-promotion-flow)
([Agentic Platform Engineering with GitHub Copilot](https://devblogs.microsoft.com/all-things-azure/agentic-platform-engineering-with-github-copilot/)).

Non-GitHub adapters substitute their own inbound mechanism for the
`repository_dispatch` hop (a Linear webhook, a Jira REST call, an Azure DevOps
work-item API call) but should converge on the same idempotency-then-approval
shape: **check for an existing item → draft/update, never silently finalize →
require human approval before status leaves `draft`.**

## GitOps-as-portal-interface (why this skill sits downstream of GitOps, not beside it)

GitOps is not just the deployment mechanism this skill observes — in a maturing
IDP, GitOps repos themselves become the developer-facing interface, alongside a
Backstage-style portal and CI pipeline capabilities layered on top
([*Expanding the IDP with CI/CD, Observability, Data Services, and Developer
Portals*](https://app.notion.com/3b8059b703e181f498f4f8638c2332ef)). At scale, the
**App of Apps** pattern is how that GitOps layer stays manageable across many
teams/environments without hand-maintaining N separate Argo CD Application objects
per team
([*GitOps at Scale and Multitenancy*](https://app.notion.com/3b8059b703e181138ef3ee4c86b4570e)).
This skill should assume App-of-Apps-shaped GitOps is the norm it's observing, not
the exception — `linked_entity` values will often resolve to an Argo CD
Application/ApplicationSet name, not a raw resource ID.

## Addendum — the Kratix GitOps delivery lifecycle (a second, complementary pattern)

[Kratix](https://docs.kratix.io/) implements a full request-to-delivery lifecycle that
this skill should recognize and observe alongside the Argo CD → `repository_dispatch`
→ GitHub Issues pattern above — the two are complementary, not competing: the Argo CD
pattern is triggered by *deployment failure*, while Kratix's pipeline is triggered by a
*new resource request*. Where an org runs Kratix, this is the lifecycle `architect-work-sync`
should map its `WorkItem` records against:

1. A developer creates an instance of a Promise's CRD (the *request*) — this is the
   moment analogous to opening a ticket, and is where a `WorkItem` link record should
   first be created.
2. Kratix's Promise controller reconciles the request and runs the Resource Configure
   Pipeline: a `reader` init container writes the request object to
   `/kratix/input/object.yaml`, the author-supplied pipeline container(s) run against
   it, and a `work-creator` sidecar turns whatever lands in `/kratix/output` into a
   `Work` object; a `status-writer` can report status back onto the request.
3. The scheduler matches the `Work`'s target requirements against registered
   `Destination` objects via `destinationSelectors`, creating one `WorkPlacement` per
   matched Destination.
4. Each `WorkPlacement` is written to the State Store (`GitStateStore` or
   `BucketStateStore`) that its Destination references — this is the actual handoff
   point to GitOps, not a Kratix-internal deployment step.
5. An external GitOps agent (Flux or Argo CD) observes the State Store and converges
   the target cluster — which means a Kratix-fulfilled request eventually produces the
   same kind of Argo CD Application/ApplicationSet this skill already expects to see
   from the App-of-Apps pattern; a `linked_entity` may legitimately resolve through
   *both* a Kratix request and an Argo CD Application for the same underlying resource.

Deleting a request triggers the symmetric Resource Delete Pipeline. Reconciliation is
continuous (a default ~10-hour resync cadence), so pipelines must be idempotent — running
Configure again on an unchanged request must not create duplicate downstream resources,
the same idempotency requirement this skill already enforces for its own adapters
([Promise workflows](https://docs.kratix.io/main/reference/promises/workflows);
[Resource workflows](https://docs.kratix.io/main/reference/resources/workflows);
[GitStateStore reference](https://docs.kratix.io/main/reference/statestore/gitstatestore);
[multi-destination management](https://docs.kratix.io/main/reference/destinations/multidestination-management)).

**The one rule this skill must carry over unchanged: never edit Kratix-generated output
in place.** A `Work`, `WorkPlacement`, or the files it writes into a State Store are
generated artifacts of the pipeline run, not a place to hand-patch a fix — exactly like
this skill's own rule against silently finalizing a ticket. If a generated result is
wrong, the fix is to change the *request*, the *Promise*, or the *pipeline* that produced
it, and let reconciliation regenerate the output; a `WorkItem` observing a Kratix-sourced
`linked_entity` should treat any drift between the State Store and a manually-edited copy
as a finding for this skill to surface, not something to reconcile silently
([Kratix internal objects](https://docs.kratix.io/main/platform-concepts/kratix-resources)).
See [../../docs/idp-adp-architect/workload-spec-components.md](../../docs/idp-adp-architect/workload-spec-components.md)
for how this lifecycle fits alongside Score, Radius, and Dapr.

## Depends on

`architect-persona-generator`, `architect-workload-catalog`
