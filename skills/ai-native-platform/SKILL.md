---
name: ai-native-platform
description: Platform engineering for AI-assisted and agentic software development — the four levels of agentic development, workspace-level governance for AI coding agents (including regulated industries), and the AI-native platform blueprint (model hubs, GPU templates, golden paths for AI workloads). Use when introducing coding agents to an org, designing agent governance/permissions/audit, planning AI/GPU infrastructure, or assessing readiness to increase agent autonomy.
---

# AI-Native Platform

The bottleneck has moved from developer capacity to **the quality and
deterministic fabric of the platform**. Models are commodity; the
differentiator is governing probabilistic intelligence with deterministic
systems — policy enforcement, reproducible CI/CD, ephemeral environments,
identity, audit. The paths you build today for human developers are the same
paths agents will execute tomorrow.

## The four levels of agentic development

| Level | Name | What changes | Constraint |
|---|---|---|---|
| 0 | Human is the loop | Functional IDP, no agents | Build this first |
| 1 | Human **in** the loop | Agents assist (codegen, search); human accepts every output | Human review bandwidth; gains ~linear |
| 2 | Human **on** the loop | Humans *dispatch* agents; parallel PRs; validation becomes an industrial feedback loop (agents retry until deterministic checks pass); humans verify behavior/evidence, not every line | CI capacity, validation breadth |
| 3 | Human as orchestrator | Agents respond to system signals (anomalies, dep updates) without initiation; rule-based promotion via a change-classification engine (low-risk auto-promoted, high-risk reviewed); humans review the rules | Architectural maturity, token economics |
| 4 | Autonomous (outlook) | Agents initiate from environmental signals (telemetry, CVEs, feedback); humans set constraints and escalation boundaries; self-improving validation | Production-system maturity — unreachable via better models alone |

Level 2 is the drastic transition. It adds a **Dispatch path**: work intake,
context packaging (repo + docs + known issues + environment hints — "a
context stack an agent can execute on, not just prose"), non-human identity
with scope enforcement, isolated workspace provisioning, output routing.
**The quality of your codified policy layer directly determines how much
autonomy you can safely grant.** Most orgs sit between L1 and L2. Layering
AI on an unchanged platform produces the self-confirmation loop: see the
downsides, conclude "not for us," fall behind.

## Governance is infrastructure, not vendor settings

Application-tier controls (Copilot/Cursor policies) aren't yours — one
vendor update re-enabled disabled policies and left a firm non-compliant
for two weeks. Govern at the **workspace level** (centrally managed CDEs,
self-hostable/air-gappable) where every process inherits policy, identity,
and network boundaries. Five governance planes:

1. **Provisioning** — environments as code; agents know who they are
2. **Policy** — RBAC over libraries, tools, repos, network domains;
   versioned policy-as-code; tell agents their boundaries up front
3. **Audit** — every prompt, tool call, and resource access logged and
   attributed; cost tracked per model/team
4. **Proxy** — one gateway for models/agents, IdP-authenticated,
   multi-provider
5. **Boundary** — per-agent firewalling, process-level network isolation

**Privilege separation is non-negotiable**: agents never inherit human
privileges. Default: least privilege, no internet, read-only + PR-only
writes; approval workflows for high-stakes actions; ephemeral
workspace-per-task (persistent workspaces breed context pollution and
permission drift). Failures are **controlled**: blocked, logged,
attributed, surfaced — the agent is told and adjusts. Regulated mappings:
SOX = full attribution prompt→model→approval; GDPR = workspace-enforced
geography; FedRAMP/ITAR = classification-tiered separation, air-gapped
self-hosted models.

## Sequencing: visibility → context → ephemeral scale

1. **Observe before restricting** — deploy AI observability first (models
   used, tool interactions, tokens, cost, shadow AI)
2. **Solve cold start** — template workspaces via IaC + lightweight context
   engineering (markdown: standards, anti-patterns, terminology);
   context-less agents produce poor output and waste tokens
3. **Then scale** — ephemeral workspace-per-PR, parallel agents, widened
   validation (scenario execution, performance, dependency/license,
   environment integrity), rule-based promotion per risk class

## The AI-native blueprint (platforms *for* AI)

AI-enabled = tools bolted into workflows. **AI-native** = models, datasets,
and inference endpoints as versioned, governed platform services. Three
layers: **governed data foundation** (versioned, compliance-tagged datasets
with lineage — compliance won't approve deployments without it) →
**accelerated compute** (composable GPU templates with cost thresholds and
scale-to-zero; never the "mainframe anti-pattern" of one centralized GPU
cluster with weeks-long queues) → **production orchestration** (models
through CI/CD as artifacts; certified templates embedding observability,
security, failover, rollback). Provide golden paths for AI use cases — a
customer-service agent path pre-wires GPU inference + vector DB + data
pipelines + endpoints; teams customize business logic only.

## Metrics

Productivity: time-to-first-commit, agent utilization. Compliance:
audit-trail completeness %, policy violation rate, shadow-AI detection.
Cost: tokens per team, cost per agent-hour, cost per inference, GPU
utilization. Targets seen: AI stack stand-up in 48h; onboarding 15–30 days
→ day one; +100% per-dev output with humans signing off.

## Anti-patterns

Governance as a security-team-only problem; bolting controls onto vendor
tools; locking agents down before observing behavior; ignoring cold start;
persistent workspaces; one-size-fits-all agent policies; siloed per-BU GPU
clusters bypassing governance; and the critical one — **skipping
production-system readiness**, entering the chaos zone where agent change
volume exceeds your capacity to validate, govern, and audit.

## As an agent

When asked to introduce or scale coding agents: first locate the org on the
four levels and check the level's constraint (L1→L2 needs dispatch +
industrial validation; L2→L3 needs the policy layer). Recommend the
visibility-first sequence, insist on workspace-level governance and
privilege separation, and score any proposal against the anti-pattern list
— especially readiness before autonomy.
