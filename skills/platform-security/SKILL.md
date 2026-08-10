---
name: platform-security
description: Vulnerability management as a platform capability — shift down (not left), hardened base images, policy-as-code guardrails, SBOMs, and self-service remediation. Use when designing platform security, handling CVE scanning and prioritization, choosing security tooling (Trivy, Grype, Syft, OPA, Kyverno), setting patch SLAs and metrics, or breaking a team out of CVE triage toil.
---

# Platform Security

**Shift down, not left.** Shift left means developers run security tools;
shift down means *the platform* runs them and developers never see findings
unless action is required. Shift left has hit its limits: developers spend
19% of their week on security tasks — a lost workday — much of it in the
"CVE doom cycle": pull a public base image, get 287 findings, spend hours
documenting false-positive exceptions, repeat tomorrow. That's a systemic
problem, not a diligence problem.

Ownership split: the platform team owns the security posture of shared
infrastructure and golden paths; app teams keep business-logic vulns and
data handling.

## Four capabilities of a secure-by-design platform

1. **Automated image hardening** — centrally managed, signed, hardened base
   images; automatic rebuilds when an upstream CVE drops. Kills entire
   classes of risk at once.
2. **Policy-as-code enforcement** — OPA / Kyverno / Conftest at the
   deployment boundary. Risk-based thresholds ("block ≥7 CVSS, warn on
   medium"), never "block any CVE" — that just creates deployment
   bottlenecks. Always provide controlled escape hatches with audit trails.
3. **Pre-approved service templates** — secure Terraform/Helm golden paths
   developers consume without needing to understand the mechanisms.
4. **Continuous secret rotation** — Vault / cloud secret managers,
   short-lived tokens, secret scanning in pipelines.

## Where scanning lives

- **CI**: SBOM generation (Syft) + scanning (Grype/Trivy), findings
  surfaced as PR comments — where developers already work, never a separate
  reporting silo
- **Registry**: continuous rescanning of stored images; auto-rebuild
  triggers
- **Deployment boundary**: admission policies
- **Runtime**: continuous monitoring with automated response
- **Prioritization** (standard practice beyond the basics): rank by
  exploitability, not raw CVSS — EPSS scores and CISA KEV listing beat
  severity alone; reachability analysis kills most false positives

## Metrics (directional targets)

Mean time to patch ↓ · % vulns auto-remediated → 80%+ for routine CVEs ·
CVE backlog trend ↓ · developer time on security ↓ from the 19% baseline ·
platform adoption ↑ (fewer than 30% of teams achieve voluntary adoption —
DX is the lever) · compliance evidence generated from pipeline data, near
zero manual effort.

## Maturity roadmap (7 steps)

1. **Baseline** — SBOM your commit-to-runtime flow (Syft/Grype), classify
   risk ownership
2. **Guardrails** — first policies in warn-only, then block ≥7; monthly
   policy review
3. **Supply chain** — central registry, rescanning, hardened signed images,
   auto-rebuild
4. **IDP integration** — secure templates, scanning hooks, PR-comment
   feedback
5. **Secrets** — vaulting, short-lived tokens, pipeline secret scanning
6. **Culture** — platform as enabler, not enforcer; security metrics in
   platform KPIs
7. **Continuous trust** — audits generated from pipeline data; track
   reduction in manual approvals

Start-now list: SBOMs for your 3 highest-traffic services; one warn-only
policy rule; PR-comment findings for one team; one shared hardened base
image; baseline the six metrics; agree ownership boundaries with security.

Prerequisites: CI/CD, containerized workloads, an IDP (or intent), and at
least one dedicated platform engineer. Without those, fix pipelines first.

## Tool selection criteria

Integration depth (embeds in CI/CD + IDP vs context switching) · automation
completeness (remediation, not just detection) · developer experience impact
(reduces load vs adds gates) · compliance evidence generation. OSS
(Syft/Grype/Trivy) is flexible but costs integration effort; commercial is
faster but vendor-dependent. No universal answer — decide by maturity, risk
tolerance, platform capacity.

## Anti-patterns

Shift-left as toil-shifting; blocking on any CVE; absolute blocks without
escape hatches; mandated platforms with poor DX; more dashboards as a fix
for scale; isolated reporting silos; manual compliance documentation.

## As an agent

When reviewing platform or service security: check the base image is the
platform's hardened one (not a public pull), policies exist as code with
thresholds and escape hatches, SBOMs are generated in CI, findings land in
PRs, and secrets are vaulted with rotation. Prioritize findings by
exploitability (KEV/EPSS) before severity, and always propose the
platform-level fix (template/base-image change) over per-service patching.
