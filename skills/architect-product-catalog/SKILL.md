---
name: architect-product-catalog
description: Packages discovered workload types and golden paths into a self-service product catalog (name, SLA, owner persona, provisioning path). Use when standing up a "Platform as a Product" catalog from real workload data.
status: planned
---

# Architect: Product Catalog

**Status:** Planned, not yet implemented. See [../../docs/idp-adp-architect/PLAN.md](../../docs/idp-adp-architect/PLAN.md) for the full domain plan.

## Reads

`.platform/workloads/*.yaml` and the golden-path patterns from `platform-blueprint`
(Reference tier).

## Writes

`.platform/catalog/products.yaml` — array of `Product` objects per
`.platform/schema/product.schema.json`.

## Depends on

`architect-workload-catalog`
