---
name: platform-blueprint
description: Reference architecture for scaffolding an Internal Developer Platform — the five-plane model, platform personas and what each consumes/creates, golden paths, design principles, and the sovereignty decision axis. Use when designing or reviewing an IDP, choosing platform tooling (portal, orchestrator, IaC, CD), defining golden paths and self-service workflows, planning an AI/ML platform, or evaluating cloud vs sovereign architecture.
---

# Platform Blueprint

The community IDP reference architecture (v2.0, derived from 480 real IDPs).
It is a framework, not a prescription — planes are swappable capabilities
behind APIs, which is also what makes exit strategies real.

## The five planes

| Plane | Contains | Owner persona |
|---|---|---|
| **Developer Control** | IDE/CDE, copilots/agents, portal — every action also represented as code in Git | DevEx platform engineer |
| **Integration & Delivery** | VCS, workload spec (e.g. Score), IaC, CI, registry, **platform orchestrator**, CD | Infrastructure platform engineer |
| **Resource** | Compute, data, networking, storage, messaging | Infrastructure platform engineer |
| **Security** (spans all) | Code analysis, secrets, IAM, policy control, network security | Security platform engineer |
| **Observability** (spans all) | Monitoring/logging, infra health, FinOps, incident management | Observability platform engineer |

AI/ML platforms add a sixth: **Data & Model Management** (feature store,
model registry with model cards, experiment/lineage metadata) — a generic
SDLC IDP will not cut it for ML workloads.

The **platform orchestrator** is the central control point: a graph of
app↔resource↔environment relationships, central RBAC, sign-off
orchestration, deployment triggering. Exemplars per slot: portal
Backstage/Port/Cortex; orchestrator Humanitec/Kratix/Cycloid; spec Score;
IaC Terraform/OpenTofu/Crossplane; CD Argo/Flux; policy OPA/Kyverno.

## Personas: who consumes, who creates

**Platform users** (consume): backend/frontend developers, product managers,
executives — plus, on ML platforms, data scientists, ML engineers, data
engineers. A developer consumes golden paths, portal/CLI/chat interfaces,
Score files, and provisioned resources with credentials injected (secret
*retrieval*, never distribution).

**Platform owners** (create): infrastructure, DevEx, security, and
observability platform engineers, a platform product manager, and a head of
platform. They create templates, IaC modules, policies, golden paths, and
fleet operations. Run it as **Platform as a Product**: internal customers,
feedback loops, adoption metrics.

## Design principles

1. **GitOps first** — every change is a PR; Git is the audit log and the
   disaster-recovery/exit mechanism (point CD at a new cluster and rebuild).
2. **Backend first** — a graph-based, API-first, versioned backend is the
   platform's brain. Linear one-off pipelines accumulate tech debt fast.
3. **Secure by default** — least privilege, encryption everywhere, policy-
   as-code validated pre-provisioning; the safest way must be the easiest.
4. **Observability by default** — every component emits telemetry; SLOs
   with error budgets per platform capability.
5. **AI-augmented, governed** — copilots and agents act only through
   trusted interfaces (CLI or orchestrator API) so every AI-triggered infra
   change has RBAC and an audit trail. Never let an LLM mutate infra
   outside them.

## Golden paths

Standardized, opinionated workflows — paved roads that turn tribal knowledge
into self-service while preserving break-out flexibility (guardrails, not
cages). The canonical shape, end to end:

> Developer states intent (chat/CLI) → PR against the workload spec
> (`score.yaml` gains a `resources:` entry) → merge triggers CI (build,
> scan, push) → orchestrator matches resource type to an approved IaC
> template, checks permissions, runs sign-offs → provisions via cloud API →
> secrets injected into the container env → resource joins the graph,
> auto-wired into observability, surfaced in the portal.

Platform-side changes get the same treatment: policy checks in the IDE,
impact simulation in the portal, progressive fleet rollout (small subset →
percentage → staging) with live observability and fast rollback.

## The sovereignty axis

Cloud-opinionated and sovereign are two ends of one decision axis:
**managed velocity vs exit-by-design**. The sovereignty test isn't "is it
open source?" but *"can we self-host, operate, and migrate away without
depending on a single commercial entity?"* Data residency alone is not
sovereignty — a control plane under foreign jurisdiction is partial
sovereignty (CLOUD Act vs GDPR). When NIS2/DORA apply: segment sensitive
workloads to certified providers, keep golden paths identical across
targets via the orchestrator, prefer foundation-governed tools (OpenTofu
over Terraform), watch open-core license drift, and treat air-gapped
operation as the ultimate stress test. AI sovereignty: open-weight models
on controlled infra; proprietary copilots leak IP.

## Sequencing

Backend/orchestrator first; Git as source of truth from day one; security
and observability foundational, never retrofitted (retrofit ≈ rework);
interfaces (portal, CLI, chat) layered over the backend; AI last, through
governed interfaces. For AI/ML: automate the highest-impact workflow first
(secure notebooks, then training pipelines, then serving), mirroring the ML
lifecycle; align early on workload definitions (training job, inference
endpoint, data pipeline) for consistent policy and cost attribution.
Enterprises really run up to 4 IDPs (services, data/AI, mobile...) — scope
which one you're building.

## Anti-patterns

Platform as a "collection of tools" without a backend brain; linear
pipelines as architecture; security/observability bolted on later; secret
distribution instead of retrieval; LLMs mutating infra outside governed
interfaces; residency mistaken for sovereignty; paper exit strategies that
were never executed; golden paths as cages (no break-out); every team
re-litigating identical tool decisions.

## As an agent

When designing: interview for personas and their top-3 workflows first,
then map each workflow to a golden path across the planes — the plane model
is the checklist for what the path must touch. When reviewing an existing
platform: locate the backend/orchestrator (if the answer is "the CI
pipeline", flag it), verify secret retrieval, policy-as-code pre-provision,
telemetry defaults, and that every AI integration goes through a governed
interface.
