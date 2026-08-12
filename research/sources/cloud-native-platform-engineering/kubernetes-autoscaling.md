---
title: "Kubernetes Autoscaling"
kind: Book
authors: "Christian Melendez"
domain: "Cloud Native and Platform Engineering"
source_notion_url: "https://app.notion.com/3b8059b703e18104be67d7a86a89c8d1"
chapter_count: 13
capture_depth: condensed
fetched_date: 2026-08-11
notion_library: "Books and Research (master database: https://app.notion.com/p/codingsanitynet/39e059b703e18022a5eaf4a9a447b9f0)"
note: "Condensed capture: agent guide and conceptual diagram per chapter only. Full verbatim chapter transcripts are intentionally not reproduced here (copyright); see source_notion_url for the complete text."
---

# Kubernetes Autoscaling

*Christian Melendez — Book*

## Chapter 1: Introduction to Kubernetes Autoscaling

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Free Benefits with Your Book?
- What does this chapter explain about Scalability foundations?

**Key points:**
- Source section: Technical requirements.
- Source section: Free Benefits with Your Book.
- Source section: Scalability foundations.
- Source section: A bit of history.

```mermaid
flowchart TD
    C["Introduction to Kubernetes Autoscaling"]
    C --> S1["Technical requirements"]
    C --> S2["Free Benefits with Your Book"]
    C --> S3["Scalability foundations"]
    C --> S4["A bit of history"]
    C --> S5["Horizontal and vertical scaling"]
    C --> S6["Vertical scaling"]
```

## Chapter 2: Workload Autoscaling Overview

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Challenges of autoscaling workloads?
- What does this chapter explain about How does the Kubernetes scheduler work??

**Key points:**
- Source section: Technical requirements.
- Source section: Challenges of autoscaling workloads.
- Source section: How does the Kubernetes scheduler work?.
- Source section: Configuring requests.

```mermaid
flowchart TD
    C["Workload Autoscaling Overview"]
    C --> S1["Technical requirements"]
    C --> S2["Challenges of autoscaling workloads"]
    C --> S3["How does the Kubernetes scheduler work?"]
    C --> S4["Configuring requests"]
    C --> S5["Configuring limits"]
    C --> S6["What if you don’t specify resource requests or limits?"]
```

## Chapter 3: Workload Autoscaling with HPA and VPA

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about The Kubernetes Metrics Server?
- What does this chapter explain about The Metrics Server: The what and the why?

**Key points:**
- Source section: Technical requirements.
- Source section: The Kubernetes Metrics Server.
- Source section: The Metrics Server: The what and the why.
- Source section: Hands-on lab: Setting up the Metrics Server.

```mermaid
flowchart TD
    C["Workload Autoscaling with HPA and VPA"]
    C --> S1["Technical requirements"]
    C --> S2["The Kubernetes Metrics Server"]
    C --> S3["The Metrics Server: The what and the why"]
    C --> S4["Hands-on lab: Setting up the Metrics Server"]
    C --> S5["Hands-on lab: Using the Metrics Server"]
    C --> S6["HPA basics"]
```

## Chapter 4: Kubernetes Event-Driven Autoscaling – Part 1

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about KEDA: What it is and why you need it?
- What does this chapter explain about KEDA’s architecture?

**Key points:**
- Source section: Technical requirements.
- Source section: KEDA: What it is and why you need it.
- Source section: KEDA’s architecture.
- Source section: KEDA Operator.

```mermaid
flowchart TD
    C["Kubernetes Event-Driven Autoscaling – Part 1"]
    C --> S1["Technical requirements"]
    C --> S2["KEDA: What it is and why you need it"]
    C --> S3["KEDA’s architecture"]
    C --> S4["KEDA Operator"]
    C --> S5["KEDA Metrics Server"]
    C --> S6["Admission Webhooks"]
```

## Chapter 5: Kubernetes Event-Driven Autoscaling – Part 2

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Autoscaling in KEDA continued?
- What does this chapter explain about Scaling based on schedule?

**Key points:**
- Source section: Technical requirements.
- Source section: Autoscaling in KEDA continued.
- Source section: Scaling based on schedule.
- Source section: Hands-on lab: Scaling to zero during non-working hours.

```mermaid
flowchart TD
    C["Kubernetes Event-Driven Autoscaling – Part 2"]
    C --> S1["Technical requirements"]
    C --> S2["Autoscaling in KEDA continued"]
    C --> S3["Scaling based on schedule"]
    C --> S4["Hands-on lab: Scaling to zero during non-working hours"]
    C --> S5["KEDA’s HTTP add-on"]
    C --> S6["What if a KEDA scaler is not available?"]
```

## Chapter 6: Workload Autoscaling Operations

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Troubleshooting workload autoscaling?
- What does this chapter explain about Troubleshooting HPA?

**Key points:**
- Source section: Technical requirements.
- Source section: Troubleshooting workload autoscaling.
- Source section: Troubleshooting HPA.
- Source section: Reviewing HPA conditions and events.

```mermaid
flowchart TD
    C["Workload Autoscaling Operations"]
    C --> S1["Technical requirements"]
    C --> S2["Troubleshooting workload autoscaling"]
    C --> S3["Troubleshooting HPA"]
    C --> S4["Reviewing HPA conditions and events"]
    C --> S5["Checking Metrics Server logs"]
    C --> S6["Troubleshooting VPA"]
```

## Chapter 7: Data Plane Autoscaling Overview

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about What is data plane autoscaling??
- What does this chapter explain about Data plane autoscalers?

**Key points:**
- Source section: Technical requirements.
- Source section: What is data plane autoscaling?.
- Source section: Data plane autoscalers.
- Source section: CAS.

```mermaid
flowchart TD
    C["Data Plane Autoscaling Overview"]
    C --> S1["Technical requirements"]
    C --> S2["What is data plane autoscaling?"]
    C --> S3["Data plane autoscalers"]
    C --> S4["CAS"]
    C --> S5["Karpenter"]
    C --> S6["CAS on AWS"]
```

## Chapter 8: Node Autoscaling with Karpenter — Part 1

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about What is Karpenter??
- What does this chapter explain about How does Karpenter work in AWS??

**Key points:**
- Source section: Technical requirements.
- Source section: What is Karpenter?.
- Source section: How does Karpenter work in AWS?.
- Source section: History of Karpenter.

```mermaid
flowchart TD
    C["Node Autoscaling with Karpenter — Part 1"]
    C --> S1["Technical requirements"]
    C --> S2["What is Karpenter?"]
    C --> S3["How does Karpenter work in AWS?"]
    C --> S4["History of Karpenter"]
    C --> S5["Karpenter resources"]
    C --> S6["NodeClass"]
```

## Chapter 9: Node Autoscaling with Karpenter — Part 2

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Removing nodes?
- What does this chapter explain about Control flow architecture?

**Key points:**
- Source section: Technical requirements.
- Source section: Removing nodes.
- Source section: Control flow architecture.
- Source section: Disruption controller.

```mermaid
flowchart TD
    C["Node Autoscaling with Karpenter — Part 2"]
    C --> S1["Technical requirements"]
    C --> S2["Removing nodes"]
    C --> S3["Control flow architecture"]
    C --> S4["Disruption controller"]
    C --> S5["Termination controller"]
    C --> S6["Disruption"]
```

## Chapter 10: Karpenter Management Operations

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Advanced operations and troubleshooting?
- What does this chapter explain about Troubleshooting Karpenter?

**Key points:**
- Source section: Technical requirements.
- Source section: Advanced operations and troubleshooting.
- Source section: Troubleshooting Karpenter.
- Source section: Getting Karpenter events.

```mermaid
flowchart TD
    C["Karpenter Management Operations"]
    C --> S1["Technical requirements"]
    C --> S2["Advanced operations and troubleshooting"]
    C --> S3["Troubleshooting Karpenter"]
    C --> S4["Getting Karpenter events"]
    C --> S5["Events reference table"]
    C --> S6["Getting Karpenter logs"]
```

## Chapter 11: Practical Use Cases for Autoscaling in Kubernetes

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Common workloads for autoscaling?
- What does this chapter explain about Hands-on lab: Create an EKS cluster with batteries included?

**Key points:**
- Source section: Technical requirements.
- Source section: Common workloads for autoscaling.
- Source section: Hands-on lab: Create an EKS cluster with batteries included.
- Source section: Use case 1: Web applications.

```mermaid
flowchart TD
    C["Practical Use Cases for Autoscaling in Kubernetes"]
    C --> S1["Technical requirements"]
    C --> S2["Common workloads for autoscaling"]
    C --> S3["Hands-on lab: Create an EKS cluster with batteries included"]
    C --> S4["Use case 1: Web applications"]
    C --> S5["Hands-on lab: Autoscaling a web application"]
    C --> S6["1. Deploy Karpenter NodePool"]
```

## Chapter 12: Patterns and Recommendations

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Scaling down to zero?
- What does this chapter explain about Hands-on lab: Scaling to zero nodes?

**Key points:**
- Source section: Technical requirements.
- Source section: Scaling down to zero.
- Source section: Hands-on lab: Scaling to zero nodes.
- Source section: 1. Deploying a sample application.

```mermaid
flowchart TD
    C["Patterns and Recommendations"]
    C --> S1["Technical requirements"]
    C --> S2["Scaling down to zero"]
    C --> S3["Hands-on lab: Scaling to zero nodes"]
    C --> S4["1. Deploying a sample application"]
    C --> S5["2. Deploying the service account"]
    C --> S6["3. Deploying the ConfigMap"]
```

## Chapter 13: Unlock Your Exclusive Benefits

**Questions this chapter answers:**
- What does this chapter explain about Unlock this Book’s Free Benefits in 3 Easy Steps?
- What does this chapter explain about Step 1?
- What does this chapter explain about Step 2?

**Key points:**
- Source section: Unlock this Book’s Free Benefits in 3 Easy Steps.
- Source section: Step 1.
- Source section: Step 2.
- Source section: Step 3.

```mermaid
flowchart TD
    C["Unlock Your Exclusive Benefits"]
    C --> S1["Unlock this Book’s Free Benefits in 3 Easy Steps"]
    C --> S2["Step 1"]
    C --> S3["Step 2"]
    C --> S4["Step 3"]
    C --> S5["Need help?"]
```
