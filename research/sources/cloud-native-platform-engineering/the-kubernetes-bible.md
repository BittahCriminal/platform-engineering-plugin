---
title: "The Kubernetes Bible"
kind: Book
authors: "Gineesh Madapparambath, Russ McKendrick"
isbn: "9781835464717"
domain: "Cloud Native and Platform Engineering"
source_notion_url: "https://app.notion.com/39e059b703e18142ad92ccbb05918482"
chapter_count: 21
capture_depth: condensed
fetched_date: 2026-08-11
notion_library: "Books and Research (master database: https://app.notion.com/p/codingsanitynet/39e059b703e18022a5eaf4a9a447b9f0)"
note: "Condensed capture: agent guide and conceptual diagram per chapter only. Full verbatim chapter transcripts are intentionally not reproduced here (copyright); see source_notion_url for the complete text."
---

# The Kubernetes Bible

*Gineesh Madapparambath, Russ McKendrick — Book*

## Chapter 1: Kubernetes Fundamentals

**Questions this chapter answers:**
- What does this chapter explain about Understanding monoliths and microservices?
- What does this chapter explain about Understanding the growth of the internet since the late 1990s?
- What does this chapter explain about Understanding the need for more frequent software releases?

**Key points:**
- Source section: Understanding monoliths and microservices.
- Source section: Understanding the growth of the internet since the late 1990s.
- Source section: Understanding the need for more frequent software releases.
- Source section: Understanding the organizational shift to agile methodologies.

```mermaid
flowchart TD
    C["Kubernetes Fundamentals"]
    C --> S1["Understanding monoliths and microservices"]
    C --> S2["Understanding the growth of the internet since the late 1990s"]
    C --> S3["Understanding the need for more frequent software releases"]
    C --> S4["Understanding the organizational shift to agile methodologies"]
    C --> S5["Understanding the shift from on-premises to the cloud"]
    C --> S6["Understanding why the cloud is well suited for scalability"]
```

## Chapter 2: Kubernetes Architecture – from Container Images to Running Pods

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about The name – Kubernetes?
- What does this chapter explain about Understanding the difference between the control plane nodes and compute nodes?

**Key points:**
- Source section: Technical requirements.
- Source section: The name – Kubernetes.
- Source section: Understanding the difference between the control plane nodes and compute nodes.
- Source section: The master and worker nodes.

```mermaid
flowchart TD
    C["Kubernetes Architecture – from Container Images to Running Pods"]
    C --> S1["Technical requirements"]
    C --> S2["The name – Kubernetes"]
    C --> S3["Understanding the difference between the control plane nodes and compute nodes"]
    C --> S4["The master and worker nodes"]
    C --> S5["Linux and Windows containers"]
    C --> S6["Kubernetes components"]
```

## Chapter 3: Installing Your First Kubernetes Cluster

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Installing a Kubernetes cluster with minikube?
- What does this chapter explain about Installing minikube?

**Key points:**
- Source section: Technical requirements.
- Source section: Installing a Kubernetes cluster with minikube.
- Source section: Installing minikube.
- Source section: Installing minikube on Linux.

```mermaid
flowchart TD
    C["Installing Your First Kubernetes Cluster"]
    C --> S1["Technical requirements"]
    C --> S2["Installing a Kubernetes cluster with minikube"]
    C --> S3["Installing minikube"]
    C --> S4["Installing minikube on Linux"]
    C --> S5["Installing minikube on macOS"]
    C --> S6["Installing minikube on Windows"]
```

## Chapter 4: Running Your Containers in Kubernetes

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Let’s explain the notion of Pods?
- What does this chapter explain about What are Pods??

**Key points:**
- Source section: Technical requirements.
- Source section: Let’s explain the notion of Pods.
- Source section: What are Pods?.
- Source section: Each Pod gets an IP address.

```mermaid
flowchart TD
    C["Running Your Containers in Kubernetes"]
    C --> S1["Technical requirements"]
    C --> S2["Let’s explain the notion of Pods"]
    C --> S3["What are Pods?"]
    C --> S4["Each Pod gets an IP address"]
    C --> S5["How should you design your Pods?"]
    C --> S6["Launching your first Pods"]
```

## Chapter 5: Using Multi-Container Pods and Design Patterns

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Understanding what multi-container Pods are?
- What does this chapter explain about Concrete scenarios where you need multi-container Pods?

**Key points:**
- Source section: Technical requirements.
- Source section: Understanding what multi-container Pods are.
- Source section: Concrete scenarios where you need multi-container Pods.
- Source section: Creating a Pod made up of two containers.

```mermaid
flowchart TD
    C["Using Multi-Container Pods and Design Patterns"]
    C --> S1["Technical requirements"]
    C --> S2["Understanding what multi-container Pods are"]
    C --> S3["Concrete scenarios where you need multi-container Pods"]
    C --> S4["Creating a Pod made up of two containers"]
    C --> S5["What happens when Kubernetes fails to launch one container in a Pod?"]
    C --> S6["Deleting a multi-container Pod"]
```

## Chapter 6: Namespaces, Quotas, and Limits for Multi-Tenancy in Kubernetes

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Introduction to Kubernetes namespaces?
- What does this chapter explain about The importance of namespaces in Kubernetes?

**Key points:**
- Source section: Technical requirements.
- Source section: Introduction to Kubernetes namespaces.
- Source section: The importance of namespaces in Kubernetes.
- Source section: How namespaces are used to split resources into chunks.

```mermaid
flowchart TD
    C["Namespaces, Quotas, and Limits for Multi-Tenancy in Kubernetes"]
    C --> S1["Technical requirements"]
    C --> S2["Introduction to Kubernetes namespaces"]
    C --> S3["The importance of namespaces in Kubernetes"]
    C --> S4["How namespaces are used to split resources into chunks"]
    C --> S5["Understanding default namespaces"]
    C --> S6["How namespaces impact your resources and services"]
```

## Chapter 7: Configuring Your Pods Using ConfigMaps and Secrets

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Understanding what ConfigMaps and Secrets are?
- What does this chapter explain about Decoupling your application and your configuration?

**Key points:**
- Source section: Technical requirements.
- Source section: Understanding what ConfigMaps and Secrets are.
- Source section: Decoupling your application and your configuration.
- Source section: Understanding how Pods consume ConfigMaps and Secrets.

```mermaid
flowchart TD
    C["Configuring Your Pods Using ConfigMaps and Secrets"]
    C --> S1["Technical requirements"]
    C --> S2["Understanding what ConfigMaps and Secrets are"]
    C --> S3["Decoupling your application and your configuration"]
    C --> S4["Understanding how Pods consume ConfigMaps and Secrets"]
    C --> S5["Configuring your Pods using ConfigMaps"]
    C --> S6["Listing ConfigMaps"]
```

## Chapter 8: Exposing Your Pods with Services

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Why would you want to expose your Pods??
- What does this chapter explain about Cluster networking in Kubernetes?

**Key points:**
- Source section: Technical requirements.
- Source section: Why would you want to expose your Pods?.
- Source section: Cluster networking in Kubernetes.
- Source section: IP address management in Kubernetes.

```mermaid
flowchart TD
    C["Exposing Your Pods with Services"]
    C --> S1["Technical requirements"]
    C --> S2["Why would you want to expose your Pods?"]
    C --> S3["Cluster networking in Kubernetes"]
    C --> S4["IP address management in Kubernetes"]
    C --> S5["Learning about network plugins"]
    C --> S6["What is a service mesh?"]
```

## Chapter 9: Persistent Storage in Kubernetes

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Why use persistent storage??
- What does this chapter explain about Introducing Volumes?

**Key points:**
- Source section: Technical requirements.
- Source section: Why use persistent storage?.
- Source section: Introducing Volumes.
- Source section: Introducing PersistentVolumes.

```mermaid
flowchart TD
    C["Persistent Storage in Kubernetes"]
    C --> S1["Technical requirements"]
    C --> S2["Why use persistent storage?"]
    C --> S3["Introducing Volumes"]
    C --> S4["Introducing PersistentVolumes"]
    C --> S5["Introducing PersistentVolume types"]
    C --> S6["Benefits brought by PersistentVolume"]
```

## Chapter 10: Running Production-Grade Kubernetes Workloads

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Ensuring High Availability and Fault Tolerance on Kubernetes?
- What does this chapter explain about High availability?

**Key points:**
- Source section: Technical requirements.
- Source section: Ensuring High Availability and Fault Tolerance on Kubernetes.
- Source section: High availability.
- Source section: Fault tolerance.

```mermaid
flowchart TD
    C["Running Production-Grade Kubernetes Workloads"]
    C --> S1["Technical requirements"]
    C --> S2["Ensuring High Availability and Fault Tolerance on Kubernetes"]
    C --> S3["High availability"]
    C --> S4["Fault tolerance"]
    C --> S5["HA and FT for Kubernetes applications"]
    C --> S6["What is ReplicationController?"]
```

## Chapter 11: Using Kubernetes Deployments for Stateless Workloads

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Introducing the Deployment object?
- What does this chapter explain about Creating a Deployment object?

**Key points:**
- Source section: Technical requirements.
- Source section: Introducing the Deployment object.
- Source section: Creating a Deployment object.
- Source section: Exposing Deployment Pods using Service objects.

```mermaid
flowchart TD
    C["Using Kubernetes Deployments for Stateless Workloads"]
    C --> S1["Technical requirements"]
    C --> S2["Introducing the Deployment object"]
    C --> S3["Creating a Deployment object"]
    C --> S4["Exposing Deployment Pods using Service objects"]
    C --> S5["Creating a Service declaratively"]
    C --> S6["Creating a Service imperatively"]
```

## Chapter 12: StatefulSet – Deploying Stateful Applications

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Introducing the StatefulSet object?
- What does this chapter explain about Managing state in containers?

**Key points:**
- Source section: Technical requirements.
- Source section: Introducing the StatefulSet object.
- Source section: Managing state in containers.
- Source section: Managing state in Kubernetes Pods.

```mermaid
flowchart TD
    C["StatefulSet – Deploying Stateful Applications"]
    C --> S1["Technical requirements"]
    C --> S2["Introducing the StatefulSet object"]
    C --> S3["Managing state in containers"]
    C --> S4["Managing state in Kubernetes Pods"]
    C --> S5["StatefulSet and how it differs from a Deployment object"]
    C --> S6["Exploring the limitations of StatefulSet"]
```

## Chapter 13: DaemonSet – Maintaining Pod Singletons on Nodes

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Introducing the DaemonSet object?
- What does this chapter explain about How DaemonSet Pods are scheduled?

**Key points:**
- Source section: Technical requirements.
- Source section: Introducing the DaemonSet object.
- Source section: How DaemonSet Pods are scheduled.
- Source section: Checking DaemonSets.

```mermaid
flowchart TD
    C["DaemonSet – Maintaining Pod Singletons on Nodes"]
    C --> S1["Technical requirements"]
    C --> S2["Introducing the DaemonSet object"]
    C --> S3["How DaemonSet Pods are scheduled"]
    C --> S4["Checking DaemonSets"]
    C --> S5["Creating and managing DaemonSets"]
    C --> S6["Creating a DaemonSet"]
```

## Chapter 14: Working with Helm Charts and Operators

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Understanding Helm?
- What does this chapter explain about Releasing software to Kubernetes using Helm?

**Key points:**
- Source section: Technical requirements.
- Source section: Understanding Helm.
- Source section: Releasing software to Kubernetes using Helm.
- Source section: Installing Helm on Linux.

```mermaid
flowchart TD
    C["Working with Helm Charts and Operators"]
    C --> S1["Technical requirements"]
    C --> S2["Understanding Helm"]
    C --> S3["Releasing software to Kubernetes using Helm"]
    C --> S4["Installing Helm on Linux"]
    C --> S5["Installing Helm on Windows"]
    C --> S6["Installing Helm on macOS"]
```

## Chapter 15: Kubernetes Clusters on Google Kubernetes Engine

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about What are Google Cloud Platform and Google Kubernetes Engine??
- What does this chapter explain about Google Cloud Platform?

**Key points:**
- Source section: Technical requirements.
- Source section: What are Google Cloud Platform and Google Kubernetes Engine?.
- Source section: Google Cloud Platform.
- Source section: Google Kubernetes Engine.

```mermaid
flowchart TD
    C["Kubernetes Clusters on Google Kubernetes Engine"]
    C --> S1["Technical requirements"]
    C --> S2["What are Google Cloud Platform and Google Kubernetes Engine?"]
    C --> S3["Google Cloud Platform"]
    C --> S4["Google Kubernetes Engine"]
    C --> S5["Preparing your local environment"]
    C --> S6["Creating a project"]
```

## Chapter 16: Launching a Kubernetes Cluster on Amazon Web Services with Amazon Elastic Kubernetes Service

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about What are Amazon Web Services and Amazon Elastic Kubernetes Service??
- What does this chapter explain about Amazon Web Services?

**Key points:**
- Source section: Technical requirements.
- Source section: What are Amazon Web Services and Amazon Elastic Kubernetes Service?.
- Source section: Amazon Web Services.
- Source section: Amazon Elastic Kubernetes Service.

```mermaid
flowchart TD
    C["Launching a Kubernetes Cluster on Amazon Web Services with Amazon Elastic Kubernetes Service"]
    C --> S1["Technical requirements"]
    C --> S2["What are Amazon Web Services and Amazon Elastic Kubernetes Service?"]
    C --> S3["Amazon Web Services"]
    C --> S4["Amazon Elastic Kubernetes Service"]
    C --> S5["Preparing your local environment"]
    C --> S6["Signing up for an AWS account"]
```

## Chapter 17: Kubernetes Clusters on Microsoft Azure with Azure Kubernetes Service

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about What are Microsoft Azure and Azure Kubernetes Service??
- What does this chapter explain about Microsoft Azure?

**Key points:**
- Source section: Technical requirements.
- Source section: What are Microsoft Azure and Azure Kubernetes Service?.
- Source section: Microsoft Azure.
- Source section: Azure Kubernetes Service.

```mermaid
flowchart TD
    C["Kubernetes Clusters on Microsoft Azure with Azure Kubernetes Service"]
    C --> S1["Technical requirements"]
    C --> S2["What are Microsoft Azure and Azure Kubernetes Service?"]
    C --> S3["Microsoft Azure"]
    C --> S4["Azure Kubernetes Service"]
    C --> S5["Preparing your local environment"]
    C --> S6["Creating a free Microsoft Azure account"]
```

## Chapter 18: Security in Kubernetes

**Questions this chapter answers:**
- What does this chapter explain about Technical Requirements?
- What does this chapter explain about Authentication and Authorization – User Access Control?
- What does this chapter explain about Authentication and User Management?

**Key points:**
- Source section: Technical Requirements.
- Source section: Authentication and Authorization – User Access Control.
- Source section: Authentication and User Management.
- Source section: The authentication workflow in Kubernetes.

```mermaid
flowchart TD
    C["Security in Kubernetes"]
    C --> S1["Technical Requirements"]
    C --> S2["Authentication and Authorization – User Access Control"]
    C --> S3["Authentication and User Management"]
    C --> S4["The authentication workflow in Kubernetes"]
    C --> S5["Authentication to the Kubernetes API"]
    C --> S6["Authentication Methods in Kubernetes"]
```

## Chapter 19: Advanced Techniques for Scheduling Pods

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Refresher – What is kube-scheduler??
- What does this chapter explain about Managing Node affinity?

**Key points:**
- Source section: Technical requirements.
- Source section: Refresher – What is kube-scheduler?.
- Source section: Managing Node affinity.
- Source section: Using nodeName for Pods.

```mermaid
flowchart TD
    C["Advanced Techniques for Scheduling Pods"]
    C --> S1["Technical requirements"]
    C --> S2["Refresher – What is kube-scheduler?"]
    C --> S3["Managing Node affinity"]
    C --> S4["Using nodeName for Pods"]
    C --> S5["Using nodeSelector for Pods"]
    C --> S6["Using the nodeAffinity configuration for Pods"]
```

## Chapter 20: Autoscaling Kubernetes Pods and Nodes

**Questions this chapter answers:**
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Pod resource requests and limits?
- What does this chapter explain about Autoscaling Pods vertically using a VerticalPodAutoscaler?

**Key points:**
- Source section: Technical requirements.
- Source section: Pod resource requests and limits.
- Source section: Autoscaling Pods vertically using a VerticalPodAutoscaler.
- Source section: Enabling InPlacePodVerticalScaling.

```mermaid
flowchart TD
    C["Autoscaling Kubernetes Pods and Nodes"]
    C --> S1["Technical requirements"]
    C --> S2["Pod resource requests and limits"]
    C --> S3["Autoscaling Pods vertically using a VerticalPodAutoscaler"]
    C --> S4["Enabling InPlacePodVerticalScaling"]
    C --> S5["Enabling a VPA in GKE"]
    C --> S6["Enabling a VPA for other Kubernetes clusters"]
```

## Chapter 21: Advanced Kubernetes: Traffic Management, Multi-Cluster Strategies, and More

**Questions this chapter answers:**
- What does this chapter explain about Technical Requirements?
- What does this chapter explain about Advanced Traffic Routing with Ingress?
- What does this chapter explain about Refresher – Kubernetes Services?

**Key points:**
- Source section: Technical Requirements.
- Source section: Advanced Traffic Routing with Ingress.
- Source section: Refresher – Kubernetes Services.
- Source section: Overview of the Ingress object.

```mermaid
flowchart TD
    C["Advanced Kubernetes: Traffic Management, Multi-Cluster Strategies, and More"]
    C --> S1["Technical Requirements"]
    C --> S2["Advanced Traffic Routing with Ingress"]
    C --> S3["Refresher – Kubernetes Services"]
    C --> S4["Overview of the Ingress object"]
    C --> S5["Using nginx as an Ingress Controller"]
    C --> S6["Deploying the NGINX Ingress Controller in minikube"]
```
