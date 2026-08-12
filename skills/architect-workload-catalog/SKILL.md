---
name: architect-workload-catalog
description: Classifies discovered resources into workload types (web service, batch job, ML training, data pipeline) and emits Score-style workload specs. Use when you need a real workload inventory for a discovered environment, not just raw resources.
status: planned
---

# Architect: Workload Catalog

**Status:** Planned, not yet implemented. See [../../docs/idp-adp-architect/PLAN.md](../../docs/idp-adp-architect/PLAN.md) for the full domain plan.

## Reads

`.platform/inventory/resources.json` and `.platform/identity/bindings.json`.

## Writes

`.platform/workloads/*.yaml` — one `Workload` object per file, per
`.platform/schema/workload.schema.json`.

## Depends on

`architect-infra-discovery`
