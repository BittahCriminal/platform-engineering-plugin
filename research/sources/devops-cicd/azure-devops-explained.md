---
title: "Azure DevOps Explained"
kind: Book
authors: "Not recorded"
isbn: "9781803238937"
domain: "DevOps and CI/CD"
source_notion_url: "https://app.notion.com/3b8059b703e1817a8e5bf2b50db19c58"
chapter_count: 2
capture_depth: condensed
fetched_date: 2026-08-11
notion_library: "Books and Research (master database: https://app.notion.com/p/codingsanitynet/39e059b703e18022a5eaf4a9a447b9f0)"
note: "Condensed capture: agent guide and conceptual diagram per chapter only. Full verbatim chapter transcripts are intentionally not reproduced here (copyright); see source_notion_url for the complete text."
---

# Azure DevOps Explained

*Not recorded — Book*

## Chapter 1: Azure DevOps Overview

**Questions this chapter answers:**
- Which principles define a DevOps operating model?
- How do Azure DevOps services support the application lifecycle?
- Where do planning, source control, pipelines, testing, and artifacts connect?
- How is the chapter's starter scenario organized?

**Key points:**
- DevOps combines customer focus, product thinking, end-to-end ownership, autonomous teams, learning, and automation.
- Azure Boards, Repos, Pipelines, Test Plans, and Artifacts cover complementary lifecycle responsibilities.
- Continuous feedback and infrastructure as code connect delivery work to operational learning.
- Tool adoption is useful only when paired with the organizational principles described in the chapter.

```mermaid
flowchart LR
    B["Plan: Azure Boards"] --> R["Code: Azure Repos"]
    R --> P["Build and release: Azure Pipelines"]
    P --> T["Validate: Test Plans"]
    T --> A["Package: Artifacts"]
    A --> O["Operate and monitor"]
    O --> B
```

## Chapter 2: Managing Projects with Azure DevOps Boards

**Questions this chapter answers:**
- How are Azure DevOps organizations and projects created?
- How do work items, backlogs, boards, and sprints relate?
- What role do process templates play?
- How can queries expose project state?

**Key points:**
- The organization and project establish the administrative boundary for delivery work.
- Process templates define work-item types and workflow behavior.
- Backlogs prioritize work, boards visualize flow, and sprints organize time-boxed execution.
- Queries provide reusable views over work-item state and relationships.

```mermaid
flowchart LR
    O["Azure DevOps organization"] --> P["Project"]
    P --> W["Work items"]
    W --> B["Backlog"]
    B --> S["Sprint"]
    W --> K["Kanban board"]
    W --> Q["Queries and reporting"]
```
