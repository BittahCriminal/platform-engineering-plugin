---
name: cluster-lifecycle
description: Kubernetes cluster lifecycle management as a platform product — Day 0 blueprints, Day 1 provisioning, Day 2 operations, and fleet management at scale. Use when designing cluster architecture, planning upgrades or patching, managing multiple clusters, defining cluster templates/blueprints, setting up GitOps drift control, or fixing snowflake-cluster operations.
---

# Cluster Lifecycle

Clusters are products with a creation-to-retirement journey, not pets to
nurse. The average org runs 20+ production clusters across 5+ locations, yet
51% admit to snowflake clusters with manual ops. Three survival principles:

1. **Automation is survival** — if a cluster activity isn't automated,
   consider it unreal.
2. **Cattle, not pets** — clusters built from reusable declarative
   templates, entirely replaceable. Recreate, don't endlessly patch.
3. **Guard against drift** — start declarative, stay declarative; GitOps
   reconciliation continuously detects and remediates back to approved state.

## Day 0 — the blueprint

Define a complete production-ready cluster blueprint, not just a distro:

- **OS** (Ubuntu, RHEL, micro-OS for edge — determines kernel patching)
- **Distribution** per use case (K3s for lightweight/edge, RKE2 for FIPS)
- **CNI** (policy enforcement, performance) and **CSI** (durability,
  multi-zone guarantees)
- **Core services baked in**: observability stack, ingress + TLS, secrets
  management (Vault), policy agents (OPA Gatekeeper / Kyverno)

Define **cluster classes** (web, data, GPU/AI, edge) — blueprints must
support diversity while holding standards.

## Day 1 — provisioning and placement

Instantiate from the blueprint with **Cluster API**, uniformly across
placements: public cloud, on-prem, sovereign, air-gapped, edge. Watch the
consistency traps — cloud assumes elastic resources; edge is
memory-constrained with unique hardware (form factors, specific GPUs).

## Day 2 — the relentless operation

This is where platforms die of firefighting. Automate:

- **Upgrades**: three upstream K8s releases a year means every cluster
  upgrades multiple times annually. Policies and desired versions in Git;
  progressive rollouts with canaries, automated checks, safe rollback.
- **Patching**: OS + dozens of stack components; 15% of orgs need
  weeks-to-months to patch their fleet — that's the failure mode.
- **Rotations**: certificates for services, ingress, node comms. Missed
  expiries inevitably cause outages.
- **Scaling**: tune HPA / VPA / KEDA / Karpenter; handle event-driven change
  (CVE hotfixes, model rollouts to inference services).
- **Resilience**: continuous policy enforcement; DR tested regularly across
  regions, backups validated by actual restores.

## Fleet management

At fleet scale you govern an ecosystem, you don't administer clusters. Put a
**fleet-level control plane** above the clusters and practice five
disciplines:

1. Fleet-wide observability (unified telemetry, cost, health)
2. Progressive rollouts (canary, automated checks, rollback)
3. Standardized blueprints per cluster class
4. Policy propagation — security/config as versioned, auto-enforced code
5. Exception workflows — temporary deviations with owner, expiry, and
   automatic reconciliation back to standard

Steer by fleet metrics, not instinct: **% of clusters at N-1 version, mean
drift-remediation time, CVE time-to-patch, fleet error budgets**. A CVE
drops → the control plane must instantly show which clusters are affected
and reconcile them to the hardened state.

## Governance

Policy-as-code as guardrails, not gates: mandatory TLS, least privilege,
privileged-workload restrictions enforced by admission controllers and
pipelines. Paved paths make infrastructure an API with clear contracts —
don't centralize all ownership. Four security domains: centralized RBAC via
trusted IdPs; automated secret rotation (never plaintext in ConfigMaps or
Git); continuous CVE scanning with image provenance and CIS benchmarks;
tested multi-region DR.

## Adoption checklist

1. Assess lifecycle gaps — is everything declarative, are upgrade policies
   in Git?
2. Define standardized blueprints per cluster class, OS upward
3. Institute fleet visibility and central policy application
4. Tighten governance and ownership boundaries
5. Harden Day-2 runbooks: automate upgrades, patching, cert rotation
6. Pilot with one high-value team; optimize on measurable outcomes

## Anti-patterns

Snowflake clusters (drifted from desired state via manual fixes); ad-hoc
manual ops — every one-off fix is a future liability; single-cluster mindset
on a fleet; shadow ops dependent on expert heroes; missed cert expiries;
secrets in Git; centralizing all ownership instead of paved paths;
automation without human oversight.

## As an agent

When reviewing cluster infrastructure: check for a declarative blueprint per
cluster class, Git-defined upgrade policy, drift reconciliation, cert
rotation automation, and fleet metrics. Any manually-applied change you find
is a finding — the fix is a template/policy change, not a hotfix.
