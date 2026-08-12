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

## Addendum — Kratix Promise as the fulfillment backend

[Kratix](https://docs.kratix.io/) is the fulfillment backend this catalog's `Product`
entries are pointing at, when the org uses it: a **Promise** is a cluster-scoped
custom resource that installs a namespaced CRD as the consumer's request form and
carries the delivery logic that honors requests against it. One catalog `Product` can
map to one Promise (or a versioned Promise Release), which is a materially stronger
binding than a hand-maintained Backstage template with no live fulfillment status
behind it
([Kratix README](https://github.com/syntasso/kratix/blob/7b12ae65677ef22f9ccf33cf72590886f5921e56/README.md);
[Promise reference](https://docs.kratix.io/main/reference/promises/intro)).

**What a `Product` entry should surface from the Promise, beyond the schema's own
fields.** A Promise's `spec.api` (the consumer-facing CRD schema), `destinationSelectors`
(eligible environments), `requiredPromises` (composition dependencies), and its
Revision/Release/availability status are all *runtime facts* that should synchronize into
the catalog entry rather than being copied once and left stale — "which API exists" and
"which delivery revision fulfils existing requests" are related but distinct facts a
catalog UI needs to show separately
([Promise upgrades overview](https://docs.kratix.io/main/reference/promises/promise-upgrade/intro)).
Ownership, support tier, cost/quota policy, and portal taxonomy remain catalog concerns
that should NOT be inferred from the Promise alone — a Promise defines the mechanism, not
the organizational accountability this schema's `owner_persona`/`sla` fields already own.

**Do not treat the Marketplace as a certified catalog.** Kratix documents a
community/Syntasso Marketplace (Postgres, Kafka, cert-manager, ArgoCD, Vault, Dapr, and
more) explicitly as starter code under active development — review, pin, and test any
marketplace Promise before it backs a `Product` entry; do not surface marketplace
availability alone as evidence a capability is production-ready
([Kratix Marketplace](https://docs.kratix.io/marketplace)).

**Division of labor with Score-style workload specs.** Score (see
`architect-workload-catalog`'s addendum) answers "what does this workload need to run?";
Kratix answers "how can developers request this governed capability, and how does the
platform deliver it?" A catalog `Product` should associate a workload's Score resource
type with the Promise that fulfills it, rather than letting the workload definition
dictate infrastructure details Kratix is meant to govern. See
[../../docs/idp-adp-architect/workload-spec-components.md](../../docs/idp-adp-architect/workload-spec-components.md)
for the full cross-project mapping.

## Depends on

`architect-workload-catalog`
