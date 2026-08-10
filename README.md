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

## Skills

| Skill | Audience | What it covers |
|---|---|---|
| `platform-blueprint` | Architects | Five-plane IDP reference architecture, personas & what they consume/create, golden paths, sovereignty axis |
| `cluster-lifecycle` | Engineers | Day 0/1/2 cluster management, blueprints, fleet control plane, drift, upgrades |
| `platform-observability` | Engineers | OTel standardization, cross-signal correlation, SLOs/error budgets, dashboards-as-code |
| `platform-security` | Engineers | Shift-down vulnerability management, hardened images, policy-as-code, SBOMs |
| `cloud-dev-environments` | Both | CDEs as inner-loop platform capability, security, AI-agent sandboxes, rollout |
| `ai-native-platform` | Both | Four levels of agentic development, workspace-level agent governance, AI-native blueprint |
| `platform-state-of-play` | Architects | 2025 benchmarks: budgets, metrics, maturity, AI reality — for business cases |

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
