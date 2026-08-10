---
name: platform-state-of-play
description: Current platform engineering benchmarks and trends (2025 State of Platform Engineering Vol 4, n=518; State of AI in Platform Engineering, n=242) for justifying platform decisions with data. Use when building a business case for platform investment, benchmarking a platform team (budget, metrics, maturity, adoption), countering defunding risk, or grounding claims about AI's actual role in platform teams.
---

# Platform State of Play

Benchmarks from the 2025 State of Platform Engineering (Vol 4) and State of
AI in Platform Engineering surveys. Use these numbers to justify decisions
and set expectations — and refresh them when newer volumes ship.

## Adoption & shape of the field

- ~90% of orgs have adopted platform engineering (DORA 2025)
- **55.9% of companies run more than one platform** — plurality is normal,
  not immaturity (services, data/AI, mobile)
- Focus areas: CI/CD 73%, IaC 67%, Kubernetes 65%, GitOps 57%, platform
  orchestration 44% — AI/LLMs still only 18% of platform focus
- Budgets are small: 47% run on $0–1M/yr; only 9% exceed $20M —
  "underfunded relative to scope" is the norm, so scope accordingly
- Roles are specializing: DevEx, security, observability, and AI-focused
  platform engineers; 21.6% of teams have a dedicated Platform Product
  Manager, and another 15% combine PPMs with product-minded engineers

## The metrics that keep you funded

- 29.6% of teams don't measure success at all; 40.9% can't show value
  within 12 months — that is the defunding profile
- 35.2% deliver measurable value in under 6 months — the bar to aim for:
  **Minimum Viable Platform, golden paths covering ~80% of common needs,
  value in weeks**
- Metrics in use: DORA 41%, time-to-market 31%, SPACE 14% — pick DORA +
  one business metric and report from month one
- Top challenges are cultural, not technical: driving adoption 45%, shared
  vision/product mindset 44%, existing-system complexity 44%

## What high performers do differently

Treat the platform as a product with data-driven investment; achieve
intrinsic or participatory adoption rather than mandates (36.6% still rely
on extrinsic mandate — it underperforms); measure DORA/SPACE plus business
impact; ship an MVP in weeks; build foundations *before* AI — DORA lists a
quality internal platform among the capabilities that amplify AI's positive
effect. Benchmark maturity against the CNCF Platform Engineering Maturity
Model (five dimensions × four levels); the field sits mostly in the middle
bands — "operational, far from optimizing."

## AI in platform teams: reality vs hype

- 89% of platform engineers use AI daily — but for code generation (75%),
  docs (70%), messages (56%), error analysis (44%), IaC generation (42%);
  strategic platform integration is rare
- The "AI implementation plateau": tactical individual usage, shadow AI, no
  measured ROI; 47% call AI over-hyped, 45% appropriately hyped
- Real blockers: skill gaps 57%, hallucination 56%, integration 51%, data
  privacy 50%; AI-generated code raises review burden — 27% find it hard
  to keep stable
- Governance exists on paper (70% have AI policies) but the working fixes
  are: policy-as-code, AI observability (drift, audit trails), context
  isolation, and CDE sandboxes with pre-scoped credentials
- Platforms-for-AI is the growth mandate: 75% host or prepare to host AI
  workloads, yet 35% run GPU workloads with no orchestration and 41.5%
  haven't touched CI/CD for AI artifacts — data scientists are the new
  platform customers and mostly unserved

## Direction of travel

"Shifting down" replaces "shifting left" — the platform absorbs toil
instead of relocating it. The "portal trap" is understood: the platform is
its orchestration backend, not its UI. By ~2028 the reports predict AI as
fundamental as version control, self-evolving platforms, humans as
strategists auditing agentic subsystems — and a widening gap between early
adopters and laggards.

## As an agent

When making a platform case: lead with time-to-value (<6 months, MVP,
golden paths for the 80%), commit to DORA + one business metric from day
one, and name the cultural challenges as the plan's primary risks. When
benchmarking: score against the CNCF maturity model and the numbers above.
When asked about AI on the platform: separate AI-powered platform (mature
tooling exists) from platform-for-AI (underserved, highest leverage) and
insist on foundations first — AI amplifies existing chaos.
