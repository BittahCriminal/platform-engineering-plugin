---
title: "Kubernetes - An Enterprise Guide, Third Edition"
kind: Book
authors: "Marc Boorshtein, Scott Surovich"
domain: "Cloud Native and Platform Engineering"
source_notion_url: "https://app.notion.com/3b8059b703e181c78561f9718697460d"
chapter_count: 19
capture_depth: condensed
fetched_date: 2026-08-11
notion_library: "Books and Research (master database: https://app.notion.com/p/codingsanitynet/39e059b703e18022a5eaf4a9a447b9f0)"
note: "Condensed capture: agent guide and conceptual diagram per chapter only. Full verbatim chapter transcripts are intentionally not reproduced here (copyright); see source_notion_url for the complete text."
---

# Kubernetes - An Enterprise Guide, Third Edition

*Marc Boorshtein, Scott Surovich — Book*

## Chapter 1: Docker and Container Essentials

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Understanding the need for containerization?
- What does this chapter explain about Understanding why Kubernetes removed Docker?

**Key points:**
- Source section: Technical requirements.
- Source section: Understanding the need for containerization.
- Source section: Understanding why Kubernetes removed Docker.
- Source section: Introducing Docker.

```mermaid
flowchart TD
    C["Docker and Container Essentials"]
    C --> S1["Technical requirements"]
    C --> S2["Understanding the need for containerization"]
    C --> S3["Understanding why Kubernetes removed Docker"]
    C --> S4["Introducing Docker"]
    C --> S5["Docker versus Moby"]
    C --> S6["Understanding Docker"]
```

## Chapter 2: Deploying Kubernetes Using KinD

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Introducing Kubernetes components and objects?
- What does this chapter explain about Interacting with a cluster?

**Key points:**
- Source section: Technical requirements.
- Source section: Introducing Kubernetes components and objects.
- Source section: Interacting with a cluster.
- Source section: Using development clusters.

```mermaid
flowchart TD
    C["Deploying Kubernetes Using KinD"]
    C --> S1["Technical requirements"]
    C --> S2["Introducing Kubernetes components and objects"]
    C --> S3["Interacting with a cluster"]
    C --> S4["Using development clusters"]
    C --> S5["Why did we select KinD for this book?"]
    C --> S6["Working with a basic KinD Kubernetes cluster"]
```

## Chapter 3: Kubernetes Bootcamp

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about An overview of Kubernetes components?
- What does this chapter explain about Exploring the control plane?

**Key points:**
- Source section: Technical requirements.
- Source section: An overview of Kubernetes components.
- Source section: Exploring the control plane.
- Source section: The Kubernetes API server.

```mermaid
flowchart TD
    C["Kubernetes Bootcamp"]
    C --> S1["Technical requirements"]
    C --> S2["An overview of Kubernetes components"]
    C --> S3["Exploring the control plane"]
    C --> S4["The Kubernetes API server"]
    C --> S5["The etcd database"]
    C --> S6["kube-scheduler"]
```

## Chapter 4: Services, Load Balancing, and Network Policies

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Exposing workloads to requests?
- What does this chapter explain about Understanding how Services work?

**Key points:**
- Source section: Technical requirements.
- Source section: Exposing workloads to requests.
- Source section: Understanding how Services work.
- Source section: Creating a Service.

```mermaid
flowchart TD
    C["Services, Load Balancing, and Network Policies"]
    C --> S1["Technical requirements"]
    C --> S2["Exposing workloads to requests"]
    C --> S3["Understanding how Services work"]
    C --> S4["Creating a Service"]
    C --> S5["Using DNS to resolve services"]
    C --> S6["Understanding different service types"]
```

## Chapter 5: External DNS and Global Load Balancing

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Making service names available externally?
- What does this chapter explain about Setting up ExternalDNS?

**Key points:**
- Source section: Technical requirements.
- Source section: Making service names available externally.
- Source section: Setting up ExternalDNS.
- Source section: Integrating ExternalDNS and CoreDNS.

```mermaid
flowchart TD
    C["External DNS and Global Load Balancing"]
    C --> S1["Technical requirements"]
    C --> S2["Making service names available externally"]
    C --> S3["Setting up ExternalDNS"]
    C --> S4["Integrating ExternalDNS and CoreDNS"]
    C --> S5["Adding an ETCD zone to CoreDNS"]
    C --> S6["ExternalDNS configuration options"]
```

## Chapter 6: Integrating Authentication into Your Cluster

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Getting Help?
- What does this chapter explain about Understanding how Kubernetes knows who you are?

**Key points:**
- Source section: Technical requirements.
- Source section: Getting Help.
- Source section: Understanding how Kubernetes knows who you are.
- Source section: External users.

```mermaid
flowchart TD
    C["Integrating Authentication into Your Cluster"]
    C --> S1["Technical requirements"]
    C --> S2["Getting Help"]
    C --> S3["Understanding how Kubernetes knows who you are"]
    C --> S4["External users"]
    C --> S5["Groups in Kubernetes"]
    C --> S6["Service accounts"]
```

## Chapter 7: RBAC Policies and Auditing

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Introduction to RBAC?
- What does this chapter explain about What’s a Role??

**Key points:**
- Source section: Technical requirements.
- Source section: Introduction to RBAC.
- Source section: What’s a Role?.
- Source section: Identifying a Role.

```mermaid
flowchart TD
    C["RBAC Policies and Auditing"]
    C --> S1["Technical requirements"]
    C --> S2["Introduction to RBAC"]
    C --> S3["What’s a Role?"]
    C --> S4["Identifying a Role"]
    C --> S5["Roles versus ClusterRoles"]
    C --> S6["Negative Roles"]
```

## Chapter 8: Managing Secrets

**Questions this chapter answers:**
- What does this chapter explain about Technical Requirements?
- What does this chapter explain about Getting Help?
- What does this chapter explain about Examining the difference between Secrets and Configuration Data?

**Key points:**
- Source section: Technical Requirements.
- Source section: Getting Help.
- Source section: Examining the difference between Secrets and Configuration Data.
- Source section: Managing Secrets in an Enterprise.

```mermaid
flowchart TD
    C["Managing Secrets"]
    C --> S1["Technical Requirements"]
    C --> S2["Getting Help"]
    C --> S3["Examining the difference between Secrets and Configuration Data"]
    C --> S4["Managing Secrets in an Enterprise"]
    C --> S5["Threats to Secrets at Rest"]
    C --> S6["Threats to Secrets in Transit"]
```

## Chapter 9: Building Multitenant Clusters with vClusters

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Getting Help?
- What does this chapter explain about The Benefits and Challenges of Multitenancy?

**Key points:**
- Source section: Technical requirements.
- Source section: Getting Help.
- Source section: The Benefits and Challenges of Multitenancy.
- Source section: Exploring the Benefits of Multitenancy.

```mermaid
flowchart TD
    C["Building Multitenant Clusters with vClusters"]
    C --> S1["Technical requirements"]
    C --> S2["Getting Help"]
    C --> S3["The Benefits and Challenges of Multitenancy"]
    C --> S4["Exploring the Benefits of Multitenancy"]
    C --> S5["The Challenges of Multitenant Kubernetes"]
    C --> S6["Using vClusters for Tenants"]
```

## Chapter 10: Deploying a Secured Kubernetes Dashboard

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Getting help?
- What does this chapter explain about How does the dashboard know who you are??

**Key points:**
- Source section: Technical requirements.
- Source section: Getting help.
- Source section: How does the dashboard know who you are?.
- Source section: Dashboard architecture.

```mermaid
flowchart TD
    C["Deploying a Secured Kubernetes Dashboard"]
    C --> S1["Technical requirements"]
    C --> S2["Getting help"]
    C --> S3["How does the dashboard know who you are?"]
    C --> S4["Dashboard architecture"]
    C --> S5["Authentication methods"]
    C --> S6["Understanding dashboard security risks"]
```

## Chapter 11: Extending Security Using Open Policy Agent

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Introduction to dynamic admission controllers?
- What does this chapter explain about What is OPA and how does it work??

**Key points:**
- Source section: Technical requirements.
- Source section: Introduction to dynamic admission controllers.
- Source section: What is OPA and how does it work?.
- Source section: OPA architecture.

```mermaid
flowchart TD
    C["Extending Security Using Open Policy Agent"]
    C --> S1["Technical requirements"]
    C --> S2["Introduction to dynamic admission controllers"]
    C --> S3["What is OPA and how does it work?"]
    C --> S4["OPA architecture"]
    C --> S5["Rego, the OPA policy language"]
    C --> S6["Gatekeeper"]
```

## Chapter 12: Node Security with Gatekeeper

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about What is node security??
- What does this chapter explain about Understanding the difference between containers and VMs?

**Key points:**
- Source section: Technical requirements.
- Source section: What is node security?.
- Source section: Understanding the difference between containers and VMs.
- Source section: Container breakouts.

```mermaid
flowchart TD
    C["Node Security with Gatekeeper"]
    C --> S1["Technical requirements"]
    C --> S2["What is node security?"]
    C --> S3["Understanding the difference between containers and VMs"]
    C --> S4["Container breakouts"]
    C --> S5["Properly designing containers"]
    C --> S6["Using and Debugging Distroless Images"]
```

## Chapter 13: KubeArmor Securing Your Runtime

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about What is runtime security??
- What does this chapter explain about Introducing KubeArmor?

**Key points:**
- Source section: Technical requirements.
- Source section: What is runtime security?.
- Source section: Introducing KubeArmor.
- Source section: Introduction to Linux Security.

```mermaid
flowchart TD
    C["KubeArmor Securing Your Runtime"]
    C --> S1["Technical requirements"]
    C --> S2["What is runtime security?"]
    C --> S3["Introducing KubeArmor"]
    C --> S4["Introduction to Linux Security"]
    C --> S5["Welcome to KubeArmor"]
    C --> S6["Container security"]
```

## Chapter 14: Backing Up Workloads

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Understanding Kubernetes backups?
- What does this chapter explain about Performing an etcd backup?

**Key points:**
- Source section: Technical requirements.
- Source section: Understanding Kubernetes backups.
- Source section: Performing an etcd backup.
- Source section: Backing up the required certificates.

```mermaid
flowchart TD
    C["Backing Up Workloads"]
    C --> S1["Technical requirements"]
    C --> S2["Understanding Kubernetes backups"]
    C --> S3["Performing an etcd backup"]
    C --> S4["Backing up the required certificates"]
    C --> S5["Backing up the etcd database"]
    C --> S6["Introducing and setting up VMware’s Velero"]
```

## Chapter 15: Monitoring Clusters and Workloads

**Questions this chapter answers:**
- What does this chapter explain about Technical Requirements?
- What does this chapter explain about Getting Help?
- What does this chapter explain about Managing Metrics in Kubernetes?

**Key points:**
- Source section: Technical Requirements.
- Source section: Getting Help.
- Source section: Managing Metrics in Kubernetes.
- Source section: How Kubernetes Provides Metrics.

```mermaid
flowchart TD
    C["Monitoring Clusters and Workloads"]
    C --> S1["Technical Requirements"]
    C --> S2["Getting Help"]
    C --> S3["Managing Metrics in Kubernetes"]
    C --> S4["How Kubernetes Provides Metrics"]
    C --> S5["Deploying the Prometheus Stack"]
    C --> S6["Introduction to Prometheus"]
```

## Chapter 16: An Introduction to Istio

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Understanding the Control Plane and Data Plane?
- What does this chapter explain about The Control Plane?

**Key points:**
- Source section: Technical requirements.
- Source section: Understanding the Control Plane and Data Plane.
- Source section: The Control Plane.
- Source section: The Data Plane.

```mermaid
flowchart TD
    C["An Introduction to Istio"]
    C --> S1["Technical requirements"]
    C --> S2["Understanding the Control Plane and Data Plane"]
    C --> S3["The Control Plane"]
    C --> S4["The Data Plane"]
    C --> S5["Why should you care about a Service mesh?"]
    C --> S6["Workload observability"]
```

## Chapter 17: Building and Deploying Applications on Istio

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Comparing microservices and monoliths?
- What does this chapter explain about My history with microservices versus monolithic architecture?

**Key points:**
- Source section: Technical requirements.
- Source section: Comparing microservices and monoliths.
- Source section: My history with microservices versus monolithic architecture.
- Source section: Comparing architectures in an application.

```mermaid
flowchart TD
    C["Building and Deploying Applications on Istio"]
    C --> S1["Technical requirements"]
    C --> S2["Comparing microservices and monoliths"]
    C --> S3["My history with microservices versus monolithic architecture"]
    C --> S4["Comparing architectures in an application"]
    C --> S5["Monolithic application design"]
    C --> S6["Microservices design"]
```

## Chapter 18: Provisioning a Multitenant Platform

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Designing a pipeline?
- What does this chapter explain about Opinionated platforms?

**Key points:**
- Source section: Technical requirements.
- Source section: Designing a pipeline.
- Source section: Opinionated platforms.
- Source section: Securing your pipeline.

```mermaid
flowchart TD
    C["Provisioning a Multitenant Platform"]
    C --> S1["Technical requirements"]
    C --> S2["Designing a pipeline"]
    C --> S3["Opinionated platforms"]
    C --> S4["Securing your pipeline"]
    C --> S5["Building our platform’s requirements"]
    C --> S6["Choosing our technology stack"]
```

## Chapter 19: Building a Developer Portal

**Questions this chapter answers:**
- What does this chapter explain about Technical Requirements?
- What does this chapter explain about Fulfilling Compute Requirements?
- What does this chapter explain about Using Cloud-Managed Kubernetes?

**Key points:**
- Source section: Technical Requirements.
- Source section: Fulfilling Compute Requirements.
- Source section: Using Cloud-Managed Kubernetes.
- Source section: Building a Home Lab.

```mermaid
flowchart TD
    C["Building a Developer Portal"]
    C --> S1["Technical Requirements"]
    C --> S2["Fulfilling Compute Requirements"]
    C --> S3["Using Cloud-Managed Kubernetes"]
    C --> S4["Building a Home Lab"]
    C --> S5["Customizing Nodes"]
    C --> S6["Accessing Services on Your Nodes"]
```
