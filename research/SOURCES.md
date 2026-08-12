# Sources — IDP/ADP Architect

Source log for the `platform-engineering-plugin`, pulled from the
[Books and Research](https://app.notion.com/p/codingsanitynet/39e059b703e18022a5eaf4a9a447b9f0)
Notion database. Each Reference-tier skill already cites the reports/books that shaped
it in its own SKILL.md; this file is the master index and additionally maps sources
forward to the planned Architect-tier skills (`architect-*`) that don't have content to
cite yet.

**Status:** populated 2026-08-11 from the Notion library. Content-status/source-status
columns are as tracked in Notion (`Extracted`/`Enriched`/`Mixed`, `Complete`/`Partial`).

## Cloud Native and Platform Engineering

| Source | Kind | Author | Informs | Status |
|---|---|---|---|---|
| [Reference Architecture of an Internal Developer Platform on Azure](https://app.notion.com/3b8059b703e1812eb297ee11197decd4) | Report | Weave Intelligence | `platform-blueprint`; `architect-infra-discovery` (Azure adapter) | Enriched / Complete |
| [Reference Architecture of an Internal Developer Platform on AWS](https://app.notion.com/3b8059b703e1816596fcc1cedfe2284e) | Report | Weave Intelligence | `platform-blueprint`; `architect-infra-discovery` (AWS adapter) | Enriched / Complete |
| [Reference Architecture for an AI/ML Internal Developer Platform on GCP](https://app.notion.com/3b8059b703e181a6ada6ded95f884de7) | Report | Weave Intelligence | `platform-blueprint`; `architect-infra-discovery` (GCP adapter) | Enriched / Complete |
| [Building the Sovereign Internal Developer Platform](https://app.notion.com/3b8059b703e181e6a28bd46d066a954c) | Report | Weave Intelligence | `platform-blueprint` (sovereignty axis) | Enriched / Complete |
| [Platform Engineering for Architects](https://app.notion.com/39e059b703e1811c900aed95c12b98fd) | Book | Max Körbächer, Andreas Grabner, Hilliary Lipsig | `platform-blueprint`; `architect-blueprint` (capstone frame) | Extracted / Complete |
| [The Platform Engineering Playbook](https://app.notion.com/3b8059b703e181fa90c6dd748e8d1ac8) | Book | — | `platform-blueprint`; `architect-product-catalog` (Platform as a Product) | Extracted / Complete |
| [Cloud Native Anti-Patterns](https://app.notion.com/3b8059b703e181fb866bd054689b199c) | Book | Gerald Bachlmayr, Aiden Ziegelaar, Alan Blockley, Bojan Zivic | `platform-blueprint` (anti-patterns); `architect-permissions-mapper` (flag rules) | Extracted / Complete |
| [Kubernetes Cluster Lifecycle Management for Platform Engineers](https://app.notion.com/3b8059b703e181d69629c698de881664) | Report | Weave Intelligence | `cluster-lifecycle`; `architect-infra-discovery` (K8s adapter) | Enriched / Complete |
| [Kubernetes - An Enterprise Guide, Third Edition](https://app.notion.com/3b8059b703e181c78561f9718697460d) | Book | Marc Boorshtein, Scott Surovich | `cluster-lifecycle`; `architect-permissions-mapper` (K8s RBAC) | Extracted / Complete |
| [The Kubernetes Bible](https://app.notion.com/39e059b703e18142ad92ccbb05918482) | Book | Gineesh Madapparambath, Russ McKendrick | `cluster-lifecycle`; `architect-infra-discovery` (K8s adapter) | Extracted / Complete |
| [50 Kubernetes Concepts Every DevOps Engineer Should Know](https://app.notion.com/3b8059b703e1817a9de3e251893b66cd) | Book | Michael Levan | `cluster-lifecycle`; `architect-workload-catalog` (K8s workload types) | Extracted / Complete |
| [Kubernetes Autoscaling](https://app.notion.com/3b8059b703e18104be67d7a86a89c8d1) | Book | Christian Melendez | `cluster-lifecycle` | Extracted / Complete |
| [Mastering Terraform](https://app.notion.com/3b8059b703e181c6a4ead0a4e8f21dcf) | Book | Mark Tinderholt | `architect-infra-discovery` (IaC-declared resources); `platform-blueprint` (IaC slot) | Extracted / Complete |
| [Observability for Platform Engineers](https://app.notion.com/3b8059b703e1813e832cdcf82c853043) | Report | Weave Intelligence | `platform-observability` | Enriched / Complete |
| [Observability in the AI-Native Era](https://app.notion.com/3b8059b703e181ddbe28fa65f427fcbe) | Book | Andreas Grabner, Hilliary Lipsig, Robert Rati, Max Körbächer | `platform-observability`; `ai-native-platform` | Extracted / Complete |
| [Vulnerability Management for Platform Engineers](https://app.notion.com/3b8059b703e181b69a18c4adbd90218f) | Report | Weave Intelligence | `platform-security`; `architect-permissions-mapper` (over-privileged flag) | Enriched / Complete |
| [Cloud Development Environments for Platform Engineers](https://app.notion.com/3b8059b703e181bb8272c742d695fe21) | Report | Weave Intelligence | `cloud-dev-environments` | Enriched / Complete |
| [The Four Levels of Agentic Software Development in the Enterprise](https://app.notion.com/3b8059b703e18104863dd219a0a12d3b) | Report | Weave Intelligence | `ai-native-platform` | Enriched / Complete |
| [Operationalizing AI Coding Agents in Regulated Industries](https://app.notion.com/3b8059b703e1818ea8b0df3ada3526ad) | Report | Weave Intelligence | `ai-native-platform`; `architect-permissions-mapper` (governed-access framing) | Enriched / Complete |
| [The Great Unlock - How Platform Engineering Creates AI-Native Enterprises](https://app.notion.com/3b8059b703e181189b93eaf9cc8fa858) | Report | Weave Intelligence | `ai-native-platform` | Enriched / Complete |
| [State of AI in Platform Engineering](https://app.notion.com/3b8059b703e181438a69d221fd255fb7) | Report | Weave Intelligence | `platform-state-of-play` | Enriched / Complete |
| [State of Platform Engineering Report - Volume 4](https://app.notion.com/3b8059b703e181e398d1f44032278244) | Report | Weave Intelligence | `platform-state-of-play` | Enriched / Complete |

## DevOps and CI/CD

| Source | Kind | Author | Informs | Status |
|---|---|---|---|---|
| [Azure DevOps Explained](https://app.notion.com/3b8059b703e1817a8e5bf2b50db19c58) | Book | — | `architect-work-sync` (Azure DevOps Boards adapter) | Enriched / **Partial** |
| [Designing and Implementing Microsoft DevOps Solutions AZ-400 Certification Guide](https://app.notion.com/3b8059b703e181c79cf2fc21b34f7958) | Book | Werner Rall | `architect-work-sync` (Azure DevOps); `cluster-lifecycle` (CI/CD) | Extracted / **Partial** |
| [Implementing CI-CD Using Azure Pipelines](https://app.notion.com/3b8059b703e181c9994bef34268b57b3) | Book | Piti Champeethong, Roberto Mardeni | `cluster-lifecycle` (CI slot); `architect-workload-catalog` (pipeline-defined workloads) | Extracted / Complete |
| [CI/CD Design Patterns](https://app.notion.com/3b8059b703e1819eb06fca5dfe61bda3) | Book | Garima Bajpai, Michel Schildmeijer, Muktesh Mishra, Pawel Piwosz | `cluster-lifecycle`; `platform-blueprint` (Integration & Delivery plane) | Extracted / Complete |
| [Implementing GitOps with Kubernetes](https://app.notion.com/3b8059b703e1816aa550e1148a83411c) | Book | Pietro Libro, Artem Lajko | `cluster-lifecycle` (GitOps-first principle); `architect-infra-discovery` (drift detection) | Extracted / Complete |
| [Hands-On Python for DevOps](https://app.notion.com/3b8059b703e1819682c5ef19380cb7a9) | Book | Ankur Roy | Implementation reference for `architect-*` adapter scripts (not a domain-knowledge source) | Extracted / Complete |
| [Application Lifecycle Management on Microsoft Power Platform](https://app.notion.com/3b8059b703e1814db1bdccf9b62ca5c9) | Book | Benedikt Bergmann | Tangential — Power Platform ALM, not core to this plugin's scope | Extracted / Complete |

## Data Engineering and Analytics (Kubernetes-adjacent only)

| Source | Kind | Author | Informs | Status |
|---|---|---|---|---|
| [Big Data on Kubernetes](https://app.notion.com/3b8059b703e181d8b323c934229e65d1) | Book | Neylson Crepalde, Thariq Mahmood | `architect-workload-catalog` (data-pipeline workload type) | Extracted / Complete |

## Software Engineering and Management (selective)

| Source | Kind | Author | Informs | Status |
|---|---|---|---|---|
| [Technical Program Manager's Handbook](https://app.notion.com/3b8059b703e181508b08db999b9bd1ed) | Book | Joshua Alan Teter | `architect-persona-generator` (non-engineer personas); `architect-work-sync` | Extracted / Complete |
| [Enterprise API Management](https://app.notion.com/3b8059b703e181dfb33ed7bfc1055600) | Book | Luis Weir | `architect-product-catalog` (API-as-product) | Mixed / Complete |

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

## Not yet used

`Streamlit for Data Science`, `Python Feature Engineering Cookbook`, `The Definitive
Guide to Microsoft Fabric` (Data Engineering domain, non-K8s) and `Clean Code in
Python/TypeScript` (Software Engineering domain) are in the library but don't inform
any current Reference- or Architect-tier skill. Left out rather than force-fit.
