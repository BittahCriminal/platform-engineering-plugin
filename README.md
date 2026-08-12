# Platform Engineering

Claude Code plugin for platform engineering work — helping architects
scaffold platforms that personas consume and create resources through, and
engineers implement them with reliability, observability, and security
built in.

Skills are distilled from current platform engineering research: the IDP
reference architectures (AWS, Azure, GCP AI/ML, sovereign), cluster
lifecycle and observability reports, vulnerability management and CDE
whitepapers, the agentic-development and AI-native-enterprise papers, and
the 2025 State-of reports.

## Skills — Reference tier

Static knowledge, distilled from research, the same for every consumer.

| Skill | Audience | What it covers |
|---|---|---|
| `platform-blueprint` | Architects | Five-plane IDP reference architecture, personas & what they consume/create, golden paths, sovereignty axis |
| `cluster-lifecycle` | Engineers | Day 0/1/2 cluster management, blueprints, fleet control plane, drift, upgrades |
| `platform-observability` | Engineers | OTel standardization, cross-signal correlation, SLOs/error budgets, dashboards-as-code |
| `platform-security` | Engineers | Shift-down vulnerability management, hardened images, policy-as-code, SBOMs |
| `cloud-dev-environments` | Both | CDEs as inner-loop platform capability, security, AI-agent sandboxes, rollout |
| `ai-native-platform` | Both | Four levels of agentic development, workspace-level agent governance, AI-native blueprint |
| `platform-state-of-play` | Architects | 2025 benchmarks: budgets, metrics, maturity, AI reality — for business cases |

## Skills — Architect tier (planned)

Reads a specific organization's real infrastructure and produces org-specific
artifacts, using the Reference tier as its knowledge base. See
[docs/idp-adp-architect/PLAN.md](docs/idp-adp-architect/PLAN.md) for the full domain
model and delivery plan. Not yet implemented — skill directories are scaffolded stubs.

| Skill | What it covers |
|---|---|
| `architect-infra-discovery` | Discovers resources across Azure, AWS, GCP, and on-prem/local Kubernetes |
| `architect-permissions-mapper` | Normalizes Azure RBAC/Entra, AWS IAM, K8s RBAC into one model; flags permission-boundary issues |
| `architect-persona-generator` | Generates real org personas from identity bindings, mapped onto the five-plane model |
| `architect-workload-catalog` | Classifies resources into Score-style workload definitions |
| `architect-product-catalog` | Packages workloads/golden paths into a self-service product catalog |
| `architect-work-sync` | Links platform entities to whichever work tracker (Linear/Jira/GitHub/Azure DevOps) is authorized |
| `architect-blueprint` | Capstone — orchestrates all of the above into one org-specific IDP/ADP blueprint |

## Install

```
/plugin marketplace add BittahCriminal/plugin-hub
/plugin install platform-engineering
```

## Layout

```
.claude-plugin/plugin.json   # manifest
skills/<name>/SKILL.md       # one directory per skill
```
