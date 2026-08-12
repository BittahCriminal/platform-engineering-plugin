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

## Addendum — Dapr's workload-level permission graph (additional, not authoritative)

[Dapr](https://docs.dapr.io/) contributes a second, workload-native permission and
identity layer wherever it's already deployed as a service mesh/runtime sidecar — this
skill should treat it as an *additional* source of access-control findings layered on
top of K8s RBAC, cloud IAM, and network policy, never as the authoritative graph on its
own. An app ID is Dapr's atomic identity unit, and every sidecar-to-sidecar call is
mTLS-encrypted by default via **Sentry**, Dapr's built-in certificate authority —
default certificate validity is 24 hours with a 15-minute clock-skew allowance, which is
a materially shorter rotation window than most static cloud-IAM credentials this skill
already flags for rotation
([security concept](https://github.com/dapr/docs/blob/f5d0b6d/daprdocs/content/en/concepts/security-concept.md);
[mTLS operations](https://github.com/dapr/docs/blob/f5d0b6d/daprdocs/content/en/operations/security/mtls.md)).

**Where Dapr's own access controls live, and what to check for each.** A Component
(the pluggable backend behind a building-block API, e.g. `type: state.redis`) can carry
a `scopes` list restricting which app IDs may load it — an unscoped Component (no
`scopes` set) is reachable by every app ID in the namespace and should be flagged the
same way this skill already flags an over-broad IAM policy. Service-invocation **ACLs**
restrict which app IDs may call which operations on a given app. **`WorkflowAccessPolicy`**
governs which external app IDs may start, query, or terminate another app's Workflow
executions — a Workflow app with no access policy defined should be treated as
equivalent to an unauthenticated internal API. Two additional, easily-confused token
layers close the local sidecar boundary: an API token that the app must present *to* its
own sidecar, and a separate app API token the sidecar must present when calling back
*into* the app — both should be verified present, not assumed, since either being unset
leaves that local hop unauthenticated
([component scopes](https://github.com/dapr/docs/blob/f5d0b6d/daprdocs/content/en/operations/components/component-scopes.md)).

**Do not treat Dapr's graph as universal.** Dapr secures *Dapr-mediated* traffic only —
a workload can still reach a dependency directly (bypassing its own sidecar), and
Dapr's Sentry-issued identities say nothing about the cloud IAM role or K8s ServiceAccount
that same pod is also running under. This skill's over-privilege and unscoped-access
findings should merge Dapr's ACL/scope/`WorkflowAccessPolicy` data with the existing
K8s RBAC and cloud IAM findings, not substitute one for the other. See
[../../docs/idp-adp-architect/workload-spec-components.md](../../docs/idp-adp-architect/workload-spec-components.md)
for how this compares to Score, Radius, and Kratix's contributions to the security plane.

## As an agent

When reviewing platform or service security: check the base image is the
platform's hardened one (not a public pull), policies exist as code with
thresholds and escape hatches, SBOMs are generated in CI, findings land in
PRs, and secrets are vaulted with rotation. Prioritize findings by
exploitability (KEV/EPSS) before severity, and always propose the
platform-level fix (template/base-image change) over per-service patching.
