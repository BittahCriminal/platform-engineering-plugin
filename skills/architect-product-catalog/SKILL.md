---
name: architect-product-catalog
description: Packages discovered workloads and golden-path patterns into a self-service product catalog — each entry a golden path with an SLA and an owning persona. Use when defining what a platform's self-service menu should contain, deciding whether a capability should be exposed as a product versus a one-off request, or reviewing catalog sprawl.
status: planned
---

# Architect: Product Catalog

**Status:** Planned, not yet implemented. See [../../docs/idp-adp-architect/PLAN.md](../../docs/idp-adp-architect/PLAN.md) for the full domain plan.

## Role in the Architect tier

`platform-blueprint` establishes golden paths as the unit of self-service; this
skill is what turns a *pattern* (a golden path template) into a *catalog entry* (a
`Product` a consumer can actually request) — the "Platform as a Product" mindset
made literal in the schema.

## Reads

`.platform/workloads/*.yaml` (from `architect-workload-catalog`) plus golden-path
pattern definitions (whatever templates the platform's IaC/CI slot already exposes —
Backstage templates, Humanitec/Kratix workflows, or a repo of Terraform modules with
a consistent interface).

## Writes

`.platform/catalog/products.yaml` — array of `Product` objects per
`.platform/schema/product.schema.json` (`name`, `golden_path`, `workload_types`,
`sla`, `owner_persona`).

## The core move: platform as a product, not a tool collection

A platform stops being "a collection of tools" the moment its capabilities are
exposed as products with an owner, a defined value proposition, and a feedback
loop — not just infrastructure someone can technically use if they know where to
look. The product catalog is where that distinction becomes machine-readable:
if a golden path has no `Product` entry, it isn't really self-service yet, no
matter how automated its IaC is
([*Understanding Platform Architecture to Build Platform as a Product*](https://app.notion.com/3b8059b703e18101a3d7ecf3b7000bd8)).
That chapter's **platform component model** and **composability** framing is the
generator's mental model for `workload_types`: a product should declare which
workload types it accepts as a set of composable capabilities, not a single
rigid shape — a "web-service" product might compose a `k8s.deployment` +
`network.load-balancer` + an observability sidecar, and the catalog entry should
name all three rather than hiding the composition inside opaque IaC.

## Avoiding the two catalog anti-patterns

**Building the wrong product.** The most common catalog mistake is packaging what
the platform team finds elegant to build rather than what consumers actually need —
the classic "don't give your users a faster horse" trap. The ACME worked example
in the source material is directly reusable as onboarding guidance for whoever
curates this catalog: start from the existing SDLC ("the life cycle of an
artifact") and the *specific* pain point in it, not from a green-field ideal
architecture
([*Building the Foundation for Supporting Platform Capabilities*](https://app.notion.com/3b8059b703e181f7b934f2d2496e8d73)).

**Freezing the catalog once it ships.** A product catalog that isn't revisited
becomes exactly the kind of rigid abstraction the agentic-era research warns decays
over time. Treat every `Product` entry as something that ages — sunset entries
whose golden path is deprecated rather than letting them silently rot, and prefer
lightweight, iterable architectures over heavyweight ones that resist change
([*Crafting Platform Products for the Future*](https://app.notion.com/3b8059b703e181b480fcf37cb163034d)).

## APIs as products (the `sla` field's model)

When a golden path exposes an API (not just infrastructure), the catalog should
borrow directly from API-product management: an API's `sla` isn't a single number,
it's a **Target Operating Model** decision about how centrally vs. federally the
product is owned and supported. A centrally-owned product can commit to a tighter
SLA than a federated one because support is concentrated; a federated product
trades SLA tightness for team autonomy
([*API Products' Target Operating Model*](https://app.notion.com/3b8059b703e181f99e45d7947a17985a)).
`owner_persona` should resolve to a real `architect-persona-generator` output
either way — an SLA with no accountable persona behind it is not enforceable, just
aspirational.

## Security and compliance are catalog attributes, not afterthoughts

A product that lets a consumer self-serve a resource but skips baked-in security
review at design time reintroduces exactly the risk `architect-permissions-mapper`
exists to catch downstream — Zero Trust and "secure to the left" thinking belongs
in the product definition itself (what does this product's golden path assume about
identity, secrets, and network exposure?), not bolted onto the IaC after the fact
([*Building Secure and Compliant Products*](https://app.notion.com/3b8059b703e181f5ade8d97f70e5469a)).
Concretely: a `Product` entry should not ship without its `golden_path` having
already passed through the plan-time and runtime enforcement layers described in
[Diagram 3](../../docs/idp-adp-architect/diagrams.md#3-three-layers-of-enforcement) —
cataloging a golden path is a statement that its guardrails are already proven, not
a promise to add them later.

## Depends on

`architect-workload-catalog`
