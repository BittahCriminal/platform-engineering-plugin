---
name: architect-blueprint
description: Capstone skill — orchestrates infra discovery, permissions mapping, persona generation, workload/product cataloging, and work-tracking sync into one org-specific IDP/ADP blueprint document, using platform-blueprint's five-plane model as its frame. Use when you want the full end-to-end platform blueprint for a specific organization, not an individual piece of it.
status: planned
---

# Architect: Blueprint (capstone)

**Status:** Planned, not yet implemented. See [../../docs/idp-adp-architect/PLAN.md](../../docs/idp-adp-architect/PLAN.md) for the full domain plan.

## Role in the Architect tier

The deliverable skill. Runs (or reads the output of) every other `architect-*` skill
and renders a single org-specific blueprint: infrastructure inventory, permissions
posture, persona map (against the five-plane model), workload/product catalog, and
linked work-tracking backlog.

## Reads

All of `.platform/**` plus `platform-blueprint` (Reference tier) for the frame it
renders results into.

## Writes

A rendered blueprint document (Markdown, or Notion page if that connector is
available) — not part of the `.platform/` machine-readable state.

## Depends on

`architect-infra-discovery`, `architect-permissions-mapper`,
`architect-persona-generator`, `architect-workload-catalog`,
`architect-product-catalog`, `architect-work-sync`
