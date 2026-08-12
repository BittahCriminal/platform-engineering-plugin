---
name: architect-permissions-mapper
description: Normalizes Azure RBAC/Entra ID, AWS IAM, and Kubernetes RBAC into one IdentityBinding model, then flags over-privileged, cross-boundary, orphaned, and unowned access. Use when mapping permissions boundaries or auditing IAM/RBAC posture for a discovered environment.
status: planned
---

# Architect: Permissions Mapper

**Status:** Planned, not yet implemented. See [../../docs/idp-adp-architect/PLAN.md](../../docs/idp-adp-architect/PLAN.md) for the full domain plan.

## Role in the Architect tier

Turns three different native permission models into one comparable shape, and is the
connective tissue between "permissions boundaries" and "IAM and RBAC" — one mapper,
two views of its output.

## Reads

`.platform/inventory/resources.json` (from `architect-infra-discovery`) plus
Entra ID / IAM / K8s RBAC APIs via the same authenticated CLIs.

## Writes

`.platform/identity/bindings.json` — array of `IdentityBinding` objects per
`.platform/schema/identity_binding.schema.json`, each optionally flagged.

## Flag rules (v1)

- `over-privileged` — wildcard scope or cluster-admin-equivalent grant
- `cross-boundary` — principal holds bindings in more than one bounded context
- `orphaned` — principal no longer exists / has no active persona
- `unowned` — binding has no corresponding Workload or Product owner

## Depends on

`architect-infra-discovery`
