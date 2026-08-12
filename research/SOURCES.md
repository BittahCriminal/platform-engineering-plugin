# Sources — IDP/ADP Architect

Source log for the `platform-engineering-plugin`, pulled from the
[Books and Research](https://app.notion.com/p/codingsanitynet/39e059b703e18022a5eaf4a9a447b9f0)
Notion database. Each Reference-tier skill already cites the reports/books that shaped
it in its own SKILL.md; this file is the master index and additionally maps sources
forward to the planned Architect-tier skills (`architect-*`) that don't have content to
cite yet.

**Status:** populated 2026-08-11 from the Notion library. Content-status/source-status
columns are as tracked in Notion (`Extracted`/`Enriched`/`Mixed`, `Complete`/`Partial`).

**Local mirror (2026-08-11):** the 32 Notion-linked rows below (Cloud Native and Platform
Engineering, DevOps and CI/CD, Data Engineering and Analytics, and Software Engineering
and Management sections) now link to local markdown files under
[`sources/`](sources/) instead of the Notion pages directly, so this research is available
without network/Notion access. Report-kind sources (Weave Intelligence, 1 chapter each) are
mirrored at full depth — agent guide, Mermaid diagram, and complete transcript. Book-kind
sources are mirrored at condensed depth — agent guide and Mermaid diagram per chapter, with
the full verbatim transcript intentionally omitted (copyright); each file's front matter
keeps the original Notion `source_notion_url` for provenance and full-text lookup.

## Cloud Native and Platform Engineering

| Source | Kind | Author | Informs | Status |
|---|---|---|---|---|
| [Reference Architecture of an Internal Developer Platform on Azure](sources/cloud-native-platform-engineering/reference-architecture-idp-azure.md) | Report | Weave Intelligence | `platform-blueprint`; `architect-infra-discovery` (Azure adapter) | Enriched / Complete |
| [Reference Architecture of an Internal Developer Platform on AWS](sources/cloud-native-platform-engineering/reference-architecture-idp-aws.md) | Report | Weave Intelligence | `platform-blueprint`; `architect-infra-discovery` (AWS adapter) | Enriched / Complete |
| [Reference Architecture for an AI/ML Internal Developer Platform on GCP](sources/cloud-native-platform-engineering/reference-architecture-aiml-idp-gcp.md) | Report | Weave Intelligence | `platform-blueprint`; `architect-infra-discovery` (GCP adapter) | Enriched / Complete |
| [Building the Sovereign Internal Developer Platform](sources/cloud-native-platform-engineering/building-the-sovereign-idp.md) | Report | Weave Intelligence | `platform-blueprint` (sovereignty axis) | Enriched / Complete |
| [Platform Engineering for Architects](sources/cloud-native-platform-engineering/platform-engineering-for-architects.md) | Book | Max Körbächer, Andreas Grabner, Hilliary Lipsig | `platform-blueprint`; `architect-blueprint` (capstone frame) | Extracted / Complete |
| [The Platform Engineering Playbook](sources/cloud-native-platform-engineering/platform-engineering-playbook.md) | Book | — | `platform-blueprint`; `architect-product-catalog` (Platform as a Product) | Extracted / Complete |
| [Cloud Native Anti-Patterns](sources/cloud-native-platform-engineering/cloud-native-anti-patterns.md) | Book | Gerald Bachlmayr, Aiden Ziegelaar, Alan Blockley, Bojan Zivic | `platform-blueprint` (anti-patterns); `architect-permissions-mapper` (flag rules) | Extracted / Complete |
| [Kubernetes Cluster Lifecycle Management for Platform Engineers](sources/cloud-native-platform-engineering/kubernetes-cluster-lifecycle-management.md) | Report | Weave Intelligence | `cluster-lifecycle`; `architect-infra-discovery` (K8s adapter) | Enriched / Complete |
| [Kubernetes - An Enterprise Guide, Third Edition](sources/cloud-native-platform-engineering/kubernetes-an-enterprise-guide-3e.md) | Book | Marc Boorshtein, Scott Surovich | `cluster-lifecycle`; `architect-permissions-mapper` (K8s RBAC) | Extracted / Complete |
| [The Kubernetes Bible](sources/cloud-native-platform-engineering/the-kubernetes-bible.md) | Book | Gineesh Madapparambath, Russ McKendrick | `cluster-lifecycle`; `architect-infra-discovery` (K8s adapter) | Extracted / Complete |
| [50 Kubernetes Concepts Every DevOps Engineer Should Know](sources/cloud-native-platform-engineering/50-kubernetes-concepts.md) | Book | Michael Levan | `cluster-lifecycle`; `architect-workload-catalog` (K8s workload types) | Extracted / Complete |
| [Kubernetes Autoscaling](sources/cloud-native-platform-engineering/kubernetes-autoscaling.md) | Book | Christian Melendez | `cluster-lifecycle` | Extracted / Complete |
| [Mastering Terraform](sources/cloud-native-platform-engineering/mastering-terraform.md) | Book | Mark Tinderholt | `architect-infra-discovery` (IaC-declared resources); `platform-blueprint` (IaC slot) | Extracted / Complete |
| [Observability for Platform Engineers](sources/cloud-native-platform-engineering/observability-for-platform-engineers.md) | Report | Weave Intelligence | `platform-observability` | Enriched / Complete |
| [Observability in the AI-Native Era](sources/cloud-native-platform-engineering/observability-in-the-ai-native-era.md) | Book | Andreas Grabner, Hilliary Lipsig, Robert Rati, Max Körbächer | `platform-observability`; `ai-native-platform` | Extracted / Complete |
| [Vulnerability Management for Platform Engineers](sources/cloud-native-platform-engineering/vulnerability-management-for-platform-engineers.md) | Report | Weave Intelligence | `platform-security`; `architect-permissions-mapper` (over-privileged flag) | Enriched / Complete |
| [Cloud Development Environments for Platform Engineers](sources/cloud-native-platform-engineering/cloud-development-environments-for-platform-engineers.md) | Report | Weave Intelligence | `cloud-dev-environments` | Enriched / Complete |
| [The Four Levels of Agentic Software Development in the Enterprise](sources/cloud-native-platform-engineering/four-levels-of-agentic-software-development.md) | Report | Weave Intelligence | `ai-native-platform` | Enriched / Complete |
| [Operationalizing AI Coding Agents in Regulated Industries](sources/cloud-native-platform-engineering/operationalizing-ai-coding-agents-regulated-industries.md) | Report | Weave Intelligence | `ai-native-platform`; `architect-permissions-mapper` (governed-access framing) | Enriched / Complete |
| [The Great Unlock - How Platform Engineering Creates AI-Native Enterprises](sources/cloud-native-platform-engineering/the-great-unlock-ai-native-enterprises.md) | Report | Weave Intelligence | `ai-native-platform` | Enriched / Complete |
| [State of AI in Platform Engineering](sources/cloud-native-platform-engineering/state-of-ai-in-platform-engineering.md) | Report | Weave Intelligence | `platform-state-of-play` | Enriched / Complete |
| [State of Platform Engineering Report - Volume 4](sources/cloud-native-platform-engineering/state-of-platform-engineering-report-v4.md) | Report | Weave Intelligence | `platform-state-of-play` | Enriched / Complete |

## DevOps and CI/CD

| Source | Kind | Author | Informs | Status |
|---|---|---|---|---|
| [Azure DevOps Explained](sources/devops-cicd/azure-devops-explained.md) | Book | — | `architect-work-sync` (Azure DevOps Boards adapter) | Enriched / **Partial** |
| [Designing and Implementing Microsoft DevOps Solutions AZ-400 Certification Guide](sources/devops-cicd/designing-implementing-ms-devops-az400.md) | Book | Werner Rall | `architect-work-sync` (Azure DevOps); `cluster-lifecycle` (CI/CD) | Extracted / **Partial** |
| [Implementing CI-CD Using Azure Pipelines](sources/devops-cicd/implementing-cicd-using-azure-pipelines.md) | Book | Piti Champeethong, Roberto Mardeni | `cluster-lifecycle` (CI slot); `architect-workload-catalog` (pipeline-defined workloads) | Extracted / Complete |
| [CI/CD Design Patterns](sources/devops-cicd/cicd-design-patterns.md) | Book | Garima Bajpai, Michel Schildmeijer, Muktesh Mishra, Pawel Piwosz | `cluster-lifecycle`; `platform-blueprint` (Integration & Delivery plane) | Extracted / Complete |
| [Implementing GitOps with Kubernetes](sources/devops-cicd/implementing-gitops-with-kubernetes.md) | Book | Pietro Libro, Artem Lajko | `cluster-lifecycle` (GitOps-first principle); `architect-infra-discovery` (drift detection) | Extracted / Complete |
| [Hands-On Python for DevOps](sources/devops-cicd/hands-on-python-for-devops.md) | Book | Ankur Roy | Implementation reference for `architect-*` adapter scripts (not a domain-knowledge source) | Extracted / Complete |
| [Application Lifecycle Management on Microsoft Power Platform](sources/devops-cicd/alm-on-microsoft-power-platform.md) | Book | Benedikt Bergmann | Tangential — Power Platform ALM, not core to this plugin's scope | Extracted / Complete |

## Data Engineering and Analytics (Kubernetes-adjacent only)

| Source | Kind | Author | Informs | Status |
|---|---|---|---|---|
| [Big Data on Kubernetes](sources/data-engineering-analytics/big-data-on-kubernetes.md) | Book | Neylson Crepalde, Thariq Mahmood | `architect-workload-catalog` (data-pipeline workload type) | Extracted / Complete |

## Software Engineering and Management (selective)

| Source | Kind | Author | Informs | Status |
|---|---|---|---|---|
| [Technical Program Manager's Handbook](sources/software-engineering-management/technical-program-managers-handbook.md) | Book | Joshua Alan Teter | `architect-persona-generator` (non-engineer personas); `architect-work-sync` | Extracted / Complete |
| [Enterprise API Management](sources/software-engineering-management/enterprise-api-management.md) | Book | Luis Weir | `architect-product-catalog` (API-as-product) | Mixed / Complete |

## Out of scope for this plugin (logged in the same Notion library)

The library also holds an **AI and Machine Learning** domain (agent-building books:
"30 Agents Every AI Engineer Must Build," "Building Agents with OpenAI Agents SDK,"
"Building AI Agents with LLMs, RAG, and Knowledge Graphs," etc.) plus general
**Software Engineering and Management** titles (Clean Code in Python/TypeScript,
"Clean Architecture with .NET"). These map to the "Agentic Harnesses" domain from the
original ask, not platform engineering — likely a separate plugin. Flagged as an open
decision rather than pulled in here; revisit once the Agentic Harnesses plugin scope is
defined.

## Web sources (agentic platform engineering series)

Distinct from the Notion book-chapter citations above — these are the live web
articles/repos fetched directly (Microsoft "All Things Azure" devblogs plus two
GitHub repos), which ground the agentic-era addenda in `architect-infra-discovery`
and `architect-permissions-mapper`, most of `architect-blueprint`, and the diagram
redraws in [../docs/idp-adp-architect/diagrams.md](../docs/idp-adp-architect/diagrams.md).

| Source | Kind | Informs | Status |
|---|---|---|---|
| [Agentic Platform Engineering with GitHub Copilot](https://devblogs.microsoft.com/all-things-azure/agentic-platform-engineering-with-github-copilot/) | Article | `architect-blueprint` (three-act model, GitHub-as-control-plane, Cluster Doctor); `architect-work-sync` (App of Apps, repository_dispatch pattern); Diagrams 7-9 | Fetched, fully read, diagrams extracted |
| [microsoftgbb/agentic-platform-engineering](https://github.com/microsoftgbb/agentic-platform-engineering) | Repo (readme) | `architect-blueprint` | Fetched, fully read |
| [Platform Engineering for the Agentic AI Era](https://devblogs.microsoft.com/all-things-azure/platform-engineering-for-the-agentic-ai-era/) | Article | `architect-blueprint` (agentic shift, layers of enforcement, org/repo agent inheritance, ops loop, role shift); Diagrams 1-6 | Fetched, fully read, diagrams extracted |
| [Azure Container Apps observability](https://learn.microsoft.com/en-us/azure/container-apps/observability) | Docs page | `platform-observability` (tangential — Azure-specific observability surface) | Fetched, fully read |
| [Azure/git-ape](https://github.com/Azure/git-ape) | Repo | `architect-blueprint` (framework-assessment loop) | Referenced by title only — direct fetch blocked by robots.txt |
| [The Human-Scale Problem in Platform Engineering](https://devblogs.microsoft.com/all-things-azure/the-human-scale-problem-in-platform-engineering/) | Article | `architect-blueprint`; `architect-persona-generator` | Fetched, fully read |
| [When Infrastructure Scales But Understanding Doesn't](https://devblogs.microsoft.com/all-things-azure/when-infrastructure-scales-but-understanding-doesnt/) | Article | `architect-blueprint` (tool sprawl, golden/paved paths, domain-specific agents, Context Engineering) | Fetched, fully read |
| [DevExpGbb/agentic-platform-engineering](https://github.com/DevExpGbb/agentic-platform-engineering) | Repo (readme) | `architect-blueprint` (Act-1/2/3 folder structure, platform-as-product value chain) | Fetched, fully read |
| [AKS + RunAI Model Streamer walkthrough](https://blog.aks.azure.com/2026/07/13/runai-streamer-vllm) | Article | `architect-permissions-mapper` (Workload Identity Federation addendum, `legacy-credential` flag) | Fetched, fully read |
| [Putting Agentic Platform Engineering to the Test](https://devblogs.microsoft.com/all-things-azure/putting-agentic-platform-engineering-to-the-test/) | Article | `architect-blueprint` (Git-Ape demo repo context, `@git-ape`/`@Git-ape Onboarding` agent invocation pattern) | Fetched, fully read |
| [Agentic DevOps: Practices, Principles, and Strategic Direction](https://devblogs.microsoft.com/all-things-azure/agentic-devops-practices-principles-strategic-direction/) | Article | `architect-blueprint` (Agentic DevOps Maturity Model rubric); `architect-persona-generator` (System Designer/Agent Operator/Quality Steward personas) | Fetched, fully read — no diagram images (all native HTML tables) |
| [Best of Both Worlds for Agentic Refactoring: GitHub Copilot + MicroVMs via Docker Sandbox](https://devblogs.microsoft.com/all-things-azure/best-of-both-worlds-for-agentic-refactoring-github-copilot-microvms-via-docker-sandbox/) | Article | Tangential — sandboxed agent execution, not core to this plugin's `.platform/**` scope | Fetched, fully read — page content polluted with unrelated spam comments below the article boundary (filtered out); no diagram images (terminal/IDE screenshots only) |
| [Frameworks Only Matter When They Force Decisions](https://devblogs.microsoft.com/all-things-azure/frameworks-only-matter-when-they-force-decisions/) | Article | `architect-blueprint` (framework-assessment loop, WAF/NIST scorecard pattern); `architect-infra-discovery` (policy-assignment-as-resource addendum) | Fetched, fully read — no diagram images (assessment loop and scorecards are prose/HTML tables) |

## Workload-specification components (Score, Radius, Kratix, Dapr)

A fourth deep-dive pass, distinct from the agentic-platform-engineering series above.
Requested explicitly as candidate *components* fulfilling this plugin's resource,
security, observability, and CI/CD/delivery planes — none of the four is treated as a
complete IDP/ADP solution on its own. Full cross-project mapping and per-plane
synthesis: [../docs/idp-adp-architect/workload-spec-components.md](../docs/idp-adp-architect/workload-spec-components.md).
Raw archived doc pages and cloned repos (kept for offline/no-network continuity) live
under `/home/user/workspace/pe_plugin_research/` outside this repo, at the pinned
commits cited below.

| Source | Kind | Informs | Status |
|---|---|---|---|
| [Score docs](https://docs.score.dev/docs/) | Docs site | `architect-workload-catalog` (portable workload contract) | Fetched, fully read |
| [Score spec reference](https://docs.score.dev/docs/score-specification/score-spec-reference/) | Docs page | `architect-workload-catalog` (resource model: `type`/`class`/`id`/`params`) | Fetched, fully read |
| [score-spec/spec](https://github.com/score-spec/spec) (commit `1c2427d`) | Repo | `architect-workload-catalog` | Cloned, README + canonical schema read |
| [Score canonical JSON Schema (score-v1b1.json)](https://github.com/score-spec/spec/blob/main/score-v1b1.json) | Schema file | `architect-workload-catalog` | Fetched, fully read |
| [CNCF Sandbox acceptance announcement](https://www.cncf.io/blog/2024/08/08/score-accepted-as-a-cncf-sandbox-project/) | Article | `architect-workload-catalog` (maturity/governance status) | Fetched, fully read |
| [CNCF Score project page](https://www.cncf.io/projects/score/) | Docs page | `architect-workload-catalog` | Fetched, fully read |
| [score-compose README](https://github.com/score-spec/score-compose/blob/main/README.md) (commit `8296be5`) | Repo README | `architect-workload-catalog` (translator matrix) | Cloned, fully read |
| [score-k8s README](https://github.com/score-spec/score-k8s/blob/main/README.md) (commit `314e437`) | Repo README | `architect-workload-catalog` (translator matrix) | Cloned, fully read |
| [score-helm README](https://github.com/score-spec/score-helm/blob/main/README.md) (commit `cbc9c87`) | Repo README | `architect-workload-catalog` (translator matrix — flagged deprecated) | Cloned, fully read |
| [Humanitec Score overview](https://developer.humanitec.com/app-humanitec-io/docs/score/overview/) | Docs page | `architect-workload-catalog` (Humanitec translator) | Fetched, fully read |
| [Radius announcement — Enabling Developer Collaboration with Radius](https://opensource.microsoft.com/blog/2023/10/18/enabling-developer-collaboration-with-radius/) | Article | `architect-permissions-mapper`, `architect-blueprint` (origin/context) | Fetched, fully read |
| [Radius docs home](https://docs.radapp.io/) | Docs site | `architect-blueprint`, `architect-permissions-mapper` | Fetched, fully read |
| [Radius Application concepts](https://docs.radapp.io/concepts/applications/) | Docs page | `architect-blueprint` (Bicep application-topology grammar) | Fetched, fully read |
| [Radius Environment concepts](https://docs.radapp.io/concepts/environments/) | Docs page | `architect-blueprint` | Fetched, fully read |
| [Radius Resource Type concepts](https://docs.radapp.io/concepts/resource-types/) | Docs page | `architect-blueprint` | Fetched, fully read |
| [Radius Recipes concepts](https://docs.radapp.io/concepts/recipes/) | Docs page | `architect-blueprint` (Recipe/Recipe Pack validation target) | Fetched, fully read |
| [Radius Recipe Pack schema](https://docs.radapp.io/reference/resources/radius/radius.core/2025-08-01-preview/recipepacks/) | Reference page | `architect-blueprint`, `architect-permissions-mapper` (still preview — flagged) | Fetched, fully read |
| [Radius Dashboard overview](https://docs.radapp.io/guides/tooling/dashboard/overview/) | Docs page | `architect-blueprint` (topology UI, not observability) | Fetched, fully read |
| [Radius Azure connection how-to](https://docs.radapp.io/guides/author-apps/azure/azure-connection/) | Docs page | `architect-permissions-mapper` (Connection as intent edge, Azure-only role automation) | Fetched, fully read |
| [Radius Azure Workload Identity setup](https://docs.radapp.io/guides/operations/providers/azure-provider/howto-azure-provider-wi/) | Docs page | `architect-permissions-mapper` (control-plane vs. workload identity) | Fetched, fully read |
| [Radius AWS IRSA setup](https://docs.radapp.io/guides/operations/providers/aws-provider/howto-aws-provider-irsa/) | Docs page | `architect-permissions-mapper` (control-plane vs. workload identity) | Fetched, fully read |
| [radius-project/radius](https://github.com/radius-project/radius) (commit `89f7c62`) | Repo | `architect-blueprint`, `architect-permissions-mapper` | Cloned, README + source read |
| [radius-project/docs](https://github.com/radius-project/docs) (commit `800d284`) | Repo | `architect-blueprint`, `architect-permissions-mapper` | Cloned, fully read |
| [Kratix docs home](https://docs.kratix.io/) | Docs site | `architect-product-catalog`, `architect-work-sync` | Fetched, fully read |
| [Kratix README](https://github.com/syntasso/kratix/blob/7b12ae65677ef22f9ccf33cf72590886f5921e56/README.md) | Repo README | `architect-product-catalog`, `architect-work-sync` | Cloned, fully read |
| [Kratix Promise reference](https://docs.kratix.io/main/reference/promises/intro) | Docs page | `architect-product-catalog` (Promise as fulfillment backend) | Fetched, fully read |
| [Kratix Promise workflows](https://docs.kratix.io/main/reference/promises/workflows) | Docs page | `architect-work-sync` (Configure/Delete pipeline mechanics) | Fetched, fully read |
| [Kratix Resource workflows](https://docs.kratix.io/main/reference/resources/workflows) | Docs page | `architect-work-sync` | Fetched, fully read |
| [Kratix Promise upgrades overview](https://docs.kratix.io/main/reference/promises/promise-upgrade/intro) | Docs page | `architect-product-catalog` (Revision/Release status) | Fetched, fully read |
| [Kratix multi-destination management](https://docs.kratix.io/main/reference/destinations/multidestination-management) | Docs page | `architect-work-sync` (scheduler/`destinationSelectors`) | Fetched, fully read |
| [Kratix GitStateStore reference](https://docs.kratix.io/main/reference/statestore/gitstatestore) | Reference page | `architect-work-sync` (State Store handoff to GitOps) | Fetched, fully read |
| [Kratix internal objects (platform concepts)](https://docs.kratix.io/main/platform-concepts/kratix-resources) | Docs page | `architect-work-sync` (Work/WorkPlacement lifecycle, never-edit-in-place rule) | Fetched, fully read |
| [Kratix compound Promises guide](https://docs.kratix.io/main/guides/compound-promises) | Docs page | `architect-product-catalog` (`requiredPromises` composition) | Fetched, fully read |
| [Kratix Marketplace](https://docs.kratix.io/marketplace) | Docs page | `architect-product-catalog` (starter code, not certified) | Fetched, fully read |
| [syntasso/kratix-marketplace](https://github.com/syntasso/kratix-marketplace) | Repo | `architect-product-catalog` | Referenced, README read |
| [Kratix v0.125.0 release notes](https://github.com/syntasso/kratix/releases/tag/v0.125.0) | Release notes | `architect-product-catalog` (maturity/versioning caveat) | Fetched, fully read |
| [OpenUK Syntasso case study](https://openuk.uk/case-studies/case-study-syntasso/) | Case study | `architect-product-catalog` (CNCF-donation-ambition caveat — not currently CNCF) | Fetched, fully read |
| [NatWest × Kratix case study](https://www.syntasso.io/case-studies/natwest-uses-kratix-to-reduce-developer-cognitive-load-and-enable-platform-cocreation) | Case study | `architect-product-catalog` | Fetched, fully read |
| [syntasso/kratix](https://github.com/syntasso/kratix) (commit `7b12ae6`) | Repo | `architect-product-catalog`, `architect-work-sync` | Cloned, fully read |
| [Dapr docs home](https://docs.dapr.io/) | Docs site | `platform-observability`, `platform-security` | Fetched, fully read |
| [Dapr runtime README](https://github.com/dapr/dapr/blob/3044570/README.md) | Repo README | `platform-observability`, `platform-security` | Cloned, fully read |
| [Dapr building-block concept](https://github.com/dapr/docs/blob/f5d0b6d/daprdocs/content/en/concepts/building-blocks-concept.md) | Docs page | `platform-observability`, `platform-security` (building-block inventory) | Cloned, fully read |
| [Dapr sidecar overview](https://github.com/dapr/docs/blob/f5d0b6d/daprdocs/content/en/concepts/dapr-services/sidecar.md) | Docs page | `platform-observability` (emitter, not backend, caveat) | Cloned, fully read |
| [Dapr components concept](https://github.com/dapr/docs/blob/f5d0b6d/daprdocs/content/en/concepts/components-concept.md) | Docs page | `platform-security` (Component `scopes`) | Cloned, fully read |
| [Dapr component schema](https://github.com/dapr/docs/blob/f5d0b6d/daprdocs/content/en/reference/resource-specs/component-schema.md) | Reference page | `platform-security` | Cloned, fully read |
| [Dapr security concept](https://github.com/dapr/docs/blob/f5d0b6d/daprdocs/content/en/concepts/security-concept.md) | Docs page | `platform-security` (app ID identity, mTLS) | Cloned, fully read |
| [Dapr mTLS operations](https://github.com/dapr/docs/blob/f5d0b6d/daprdocs/content/en/operations/security/mtls.md) | Docs page | `platform-security` (Sentry CA, 24h cert validity) | Cloned, fully read |
| [Dapr component scopes](https://github.com/dapr/docs/blob/f5d0b6d/daprdocs/content/en/operations/components/component-scopes.md) | Docs page | `platform-security` | Cloned, fully read |
| [Dapr observability concept](https://github.com/dapr/docs/blob/f5d0b6d/daprdocs/content/en/concepts/observability-concept.md) | Docs page | `platform-observability` (native tracing/metrics emission) | Cloned, fully read |
| [Dapr metrics overview](https://github.com/dapr/docs/blob/f5d0b6d/daprdocs/content/en/operations/observability/metrics/metrics-overview.md) | Docs page | `platform-observability` | Cloned, fully read |
| [CNCF Dapr project page](https://www.cncf.io/projects/dapr/) | Docs page | `platform-observability`, `platform-security` (maturity status) | Fetched, fully read |
| [CNCF Dapr graduation announcement](https://www.cncf.io/announcements/2024/11/12/cloud-native-computing-foundation-announces-dapr-graduation/) | Article | `platform-observability`, `platform-security` | Fetched, fully read |
| [dapr/docs](https://github.com/dapr/docs) (commit `f5d0b6d`) | Repo | `platform-observability`, `platform-security` | Cloned, fully read |
| [dapr/dapr](https://github.com/dapr/dapr) (commit `3044570`) | Repo | `platform-observability`, `platform-security` | Cloned, fully read |
| [dapr/components-contrib](https://github.com/dapr/components-contrib) (commit `349892b`) | Repo | `platform-observability`, `platform-security` (component inventory counts) | Cloned, fully read |

## Not yet used

`Streamlit for Data Science`, `Python Feature Engineering Cookbook`, `The Definitive
Guide to Microsoft Fabric` (Data Engineering domain, non-K8s) and `Clean Code in
Python/TypeScript` (Software Engineering domain) are in the library but don't inform
any current Reference- or Architect-tier skill. Left out rather than force-fit.
