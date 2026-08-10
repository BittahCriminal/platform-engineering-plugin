---
name: platform-observability
description: Observability as a platform capability — OpenTelemetry standardization, cross-signal correlation, auto-instrumentation, dashboards-as-code, and SLO-based reliability. Use when designing or reviewing platform observability, instrumenting services, choosing telemetry tooling, setting up dashboards/alerts, defining SLOs/SLIs/error budgets, or diagnosing why incidents take too long to resolve.
---

# Platform Observability

Monitoring tells you something is wrong; observability explains why.
Observability is the ability to determine any internal state of the system by
asking questions from the outside — and on a platform it is a *product* the
platform team ships, not a tool each app team assembles. 70% of platform
teams cite data noise and lack of context as the main cause of prolonged
outages; standardized telemetry resolves incidents ~44% faster.

## The platform team's dual mandate

1. **Observe your own platform** — clusters, cloud resources, databases,
   message brokers, CI/CD, shared services — well enough to push changes with
   confidence.
2. **Provide observability as a service** to application teams: a paved path
   to visibility with golden defaults developers can adjust, not a restriction.

Out of the box for every service on the platform: auto-instrumentation,
standard dashboards, pre-set alerts and sampling. Developers get insight by
default; the platform team owns the telemetry lifecycle (intentional
collection → standardization → correlation) — that ownership is non-negotiable.

## Signals: beyond the three pillars

Metrics (trends, alerting), logs (forensic context), traces/spans (request
journey and bottlenecks) — plus production profiles (what code burns CPU/
memory) and RUM (real user experience). Treat them as one narrative, not
silos. The superpower is **cross-signal correlation**: shared resource
attributes + trace context propagation let you navigate alert → slow trace →
the log line of the deploy that caused it. That navigation is what cuts MTTR.

## Standardize on OpenTelemetry

- **Semantic conventions** — one vocabulary (`service.name`,
  `http.response.status_code`) and shared resource attributes
  (`cloud.region`, `k8s.pod.name`) across all signals. Without them:
  conflicting labels, broken queries, brittle dashboards.
- **OTel Operator** for auto-instrumentation — manual instrumentation fails
  at scale (gaps, noise, duplicated toil).
- **OTel Collector** as the telemetry router and policy engine: sample
  high-volume traces, redact sensitive fields, drop debug logs — centrally,
  without touching application code, and without vendor lock-in.

## Telemetry quality: four tests

Design telemetry to answer specific failure-mode questions, not to
"instrument everything". Evaluate every signal on: **Semantics** (clearly
defined meaning), **Context** (service version, region, conditions),
**Relations** (linked to related signals — a log that points to its trace),
**Accuracy**. Telemetry without context is just noise.

## Reliability targets: SLOs and error budgets

(Standard practice layered on top of the telemetry foundation above.)

- Define **SLIs** from the user's perspective (availability, latency,
  correctness) per golden path — not per microservice internals.
- Set **SLOs** the business actually needs; 100% is wrong. The gap is the
  **error budget**: spend it on releases, freeze features when it's exhausted.
- Alert on symptoms and budget burn rate, not causes — a page means a user
  is hurting or the budget is burning fast; everything else is a ticket.

## Priorities in order

1. Automate instrumentation at scale (Operator, not per-team effort)
2. Standardize with OTel semantic conventions — define and enforce
3. Centralize control at the Collector (sampling, redaction, cost)
4. GitOps everything: dashboards-as-code (e.g. Perses — YAML in Git,
   PR-reviewed, CI-deployed) and alert rules the same way
5. Ship paved paths with smart, adjustable defaults

## Anti-patterns

- Observability as an afterthought, or a collection of siloed tools
- Monitoring-only alerting: "it's broken" with no why-context
- Manual instrumentation and hand-edited dashboards
- Custom labels / mismatched field names per team
- "Instrument everything" instead of question-driven telemetry design
- Treating observability as a cost center — measured ROI averages 2.6x

## As an agent

When reviewing a service or design on the platform: check it emits OTel with
the platform's semantic conventions, is auto-instrumented (not hand-rolled),
has a dashboard and alerts defined as code, and has an SLO with an owner.
Flag any signal that fails the four quality tests, and any alert that pages
on a cause rather than a symptom.
