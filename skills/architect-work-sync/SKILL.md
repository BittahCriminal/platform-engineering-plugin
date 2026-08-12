---
name: architect-work-sync
description: Links discovered platform entities (resources, workloads, personas, permission gaps) to whichever work-tracking system is authorized at runtime — Linear, Jira, GitHub Issues/Projects, or Azure DevOps Boards — and drafts backlog items for platform gaps found during discovery. Use when tying platform architecture work to existing ticket tracking.
status: planned
---

# Architect: Work Sync

**Status:** Planned, not yet implemented. See [../../docs/idp-adp-architect/PLAN.md](../../docs/idp-adp-architect/PLAN.md) for the full domain plan.

## Role in the Architect tier

Adapter-based, not a fixed choice of tracker. Detects which systems are actually
connected/authorized at run time and only activates those adapters — no system is
hardcoded as "the" tracker, since access is granted per consumer.

## Reads

`.platform/personas/personas.yaml`, `.platform/workloads/*.yaml`, and any gaps flagged
by `architect-permissions-mapper`.

## Writes

`.platform/worktracking/links.json` — array of `WorkItem` objects per
`.platform/schema/work_item.schema.json`. New tickets are always drafted for human
approval before creation — this skill never files tickets silently.

## Depends on

`architect-persona-generator`, `architect-workload-catalog`
