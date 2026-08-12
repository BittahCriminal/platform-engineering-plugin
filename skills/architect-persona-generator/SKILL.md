---
name: architect-persona-generator
description: Generates org-specific platform personas from identity bindings and org data (Entra ID groups, GitHub teams), mapped onto the five-plane model from platform-blueprint. Use when you need a real persona map for a specific organization instead of the generic platform-blueprint roles.
status: planned
---

# Architect: Persona Generator

**Status:** Planned, not yet implemented. See [../../docs/idp-adp-architect/PLAN.md](../../docs/idp-adp-architect/PLAN.md) for the full domain plan.

## Role in the Architect tier

Replaces `platform-blueprint`'s generic persona table ("backend developer", "security
platform engineer", ...) with real names and groups from this organization, still
mapped onto the same five/six-plane model so the two skills stay comparable.

## Reads

`.platform/identity/bindings.json` (from `architect-permissions-mapper`) plus org group
data (Entra ID groups, GitHub team membership).

## Writes

`.platform/personas/personas.yaml` — array of `Persona` objects per
`.platform/schema/persona.schema.json`.

## Depends on

`architect-permissions-mapper`; conceptually built on `platform-blueprint`'s five-plane
model (Reference tier).
