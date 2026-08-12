---
name: architect-infra-discovery
description: Discovers real infrastructure across cloud and on-prem/local providers (Azure, AWS, GCP, Kubernetes) and normalizes it into the shared Resource schema. Use when starting a platform blueprint for a specific organization and no inventory exists yet, or when the inventory needs to be refreshed against current state.
status: planned
---

# Architect: Infra Discovery

**Status:** Planned, not yet implemented. See [../../docs/idp-adp-architect/PLAN.md](../../docs/idp-adp-architect/PLAN.md) for the full domain plan.

## Role in the Architect tier

First skill in the pipeline. Every other `architect-*` skill depends on the
`.platform/inventory/resources.json` this one produces.

## Reads

Provider APIs via already-authenticated CLIs — `az`, `aws`, `gcloud`, `kubectl`
(current context). No new credentials are provisioned by this skill; it uses whatever
the operator is already logged into.

## Writes

`.platform/inventory/resources.json` — array of `Resource` objects per
`.platform/schema/resource.schema.json`.

## Provider adapters (build order)

1. Azure (subscriptions, resource groups)
2. On-prem/local Kubernetes (current `kubeconfig` context)
3. AWS
4. GCP

Each adapter implements one function: `discover(provider) -> Resource[]`. Downstream
skills never branch on provider — they only read the normalized schema.

## Open questions

- Which Azure tenant/subscription and which Kubernetes context(s) to run against first
  (recommend a non-production one for the pilot).
