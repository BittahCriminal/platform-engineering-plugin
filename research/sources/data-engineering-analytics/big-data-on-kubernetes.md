---
title: "Big Data on Kubernetes"
kind: Book
authors: "Neylson Crepalde, Thariq Mahmood"
isbn: "9781835462140"
domain: "Data Engineering and Analytics"
source_notion_url: "https://app.notion.com/3b8059b703e181d8b323c934229e65d1"
chapter_count: 12
capture_depth: condensed
fetched_date: 2026-08-11
notion_library: "Books and Research (master database: https://app.notion.com/p/codingsanitynet/39e059b703e18022a5eaf4a9a447b9f0)"
note: "Condensed capture: agent guide and conceptual diagram per chapter only. Full verbatim chapter transcripts are intentionally not reproduced here (copyright); see source_notion_url for the complete text."
---

# Big Data on Kubernetes

*Neylson Crepalde, Thariq Mahmood — Book*
## Chapter 1: The Modern Data Stack

**Questions this chapter answers:**
- What does this chapter explain about Chapter 4: The Modern Data Stack?
- What does this chapter explain about Data architectures?
- What does this chapter explain about The Lambda architecture?

**Key points:**
- Source section: Chapter 4: The Modern Data Stack.
- Source section: Data architectures.
- Source section: The Lambda architecture.
- Source section: The Kappa architecture.

```mermaid
flowchart TD
    C["The Modern Data Stack"]
    C --> S1["Chapter 4: The Modern Data Stack"]
    C --> S2["Data architectures"]
    C --> S3["The Lambda architecture"]
    C --> S4["The Kappa architecture"]
    C --> S5["Comparing Lambda and Kappa"]
    C --> S6["Data lake design for big data"]
```

## Chapter 2: Big Data Processing with Apache Spark

**Questions this chapter answers:**
- What does this chapter explain about Chapter 5: Big Data Processing with Apache Spark?
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Getting started with Spark?

**Key points:**
- Source section: Chapter 5: Big Data Processing with Apache Spark.
- Source section: Technical requirements.
- Source section: Getting started with Spark.
- Source section: Installing Spark locally.

```mermaid
flowchart TD
    C["Big Data Processing with Apache Spark"]
    C --> S1["Chapter 5: Big Data Processing with Apache Spark"]
    C --> S2["Technical requirements"]
    C --> S3["Getting started with Spark"]
    C --> S4["Installing Spark locally"]
    C --> S5["Spark architecture"]
    C --> S6["Spark executors"]
```

## Chapter 3: Building Pipelines with Apache Airflow

**Questions this chapter answers:**
- What does this chapter explain about Chapter 6: Building Pipelines with Apache Airflow?
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Getting started with Airflow?

**Key points:**
- Source section: Chapter 6: Building Pipelines with Apache Airflow.
- Source section: Technical requirements.
- Source section: Getting started with Airflow.
- Source section: Installing Airflow with Astro.

```mermaid
flowchart TD
    C["Building Pipelines with Apache Airflow"]
    C --> S1["Chapter 6: Building Pipelines with Apache Airflow"]
    C --> S2["Technical requirements"]
    C --> S3["Getting started with Airflow"]
    C --> S4["Installing Airflow with Astro"]
    C --> S5["Airflow architecture"]
    C --> S6["Airflow’s distributed architecture"]
```

## Chapter 4: Apache Kafka for Real-Time Events and Data Ingestion

**Questions this chapter answers:**
- What does this chapter explain about Chapter 7: Apache Kafka for Real-Time Events and Data Ingestion?
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Getting started with Kafka?

**Key points:**
- Source section: Chapter 7: Apache Kafka for Real-Time Events and Data Ingestion.
- Source section: Technical requirements.
- Source section: Getting started with Kafka.
- Source section: Exploring the Kafka architecture.

```mermaid
flowchart TD
    C["Apache Kafka for Real-Time Events and Data Ingestion"]
    C --> S1["Chapter 7: Apache Kafka for Real-Time Events and Data Ingestion"]
    C --> S2["Technical requirements"]
    C --> S3["Getting started with Kafka"]
    C --> S4["Exploring the Kafka architecture"]
    C --> S5["The PubSub design"]
    C --> S6["How Kafka delivers exactly-once semantics"]
```

## Chapter 5: Deploying the Big Data Stack on Kubernetes

**Questions this chapter answers:**
- What does this chapter explain about Chapter 8: Deploying the Big Data Stack on Kubernetes?
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Deploying Spark on Kubernetes?

**Key points:**
- Source section: Chapter 8: Deploying the Big Data Stack on Kubernetes.
- Source section: Technical requirements.
- Source section: Deploying Spark on Kubernetes.
- Source section: Deploying Airflow on Kubernetes.

```mermaid
flowchart TD
    C["Deploying the Big Data Stack on Kubernetes"]
    C --> S1["Chapter 8: Deploying the Big Data Stack on Kubernetes"]
    C --> S2["Technical requirements"]
    C --> S3["Deploying Spark on Kubernetes"]
    C --> S4["Deploying Airflow on Kubernetes"]
    C --> S5["Deploying Kafka on Kubernetes"]
    C --> S6["Summary"]
```

## Chapter 6: Data Consumption Layer

**Questions this chapter answers:**
- What does this chapter explain about Chapter 9: Data Consumption Layer?
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Getting started with SQL query engines?

**Key points:**
- Source section: Chapter 9: Data Consumption Layer.
- Source section: Technical requirements.
- Source section: Getting started with SQL query engines.
- Source section: The limitations of traditional data warehouses.

```mermaid
flowchart TD
    C["Data Consumption Layer"]
    C --> S1["Chapter 9: Data Consumption Layer"]
    C --> S2["Technical requirements"]
    C --> S3["Getting started with SQL query engines"]
    C --> S4["The limitations of traditional data warehouses"]
    C --> S5["The rise of SQL query engines"]
    C --> S6["The architecture of SQL query engines"]
```

## Chapter 7: Building a Big Data Pipeline on Kubernetes

**Questions this chapter answers:**
- What does this chapter explain about Chapter 10: Building a Big Data Pipeline on Kubernetes?
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Checking the deployed tools?

**Key points:**
- Source section: Chapter 10: Building a Big Data Pipeline on Kubernetes.
- Source section: Technical requirements.
- Source section: Checking the deployed tools.
- Source section: Building a batch pipeline.

```mermaid
flowchart TD
    C["Building a Big Data Pipeline on Kubernetes"]
    C --> S1["Chapter 10: Building a Big Data Pipeline on Kubernetes"]
    C --> S2["Technical requirements"]
    C --> S3["Checking the deployed tools"]
    C --> S4["Building a batch pipeline"]
    C --> S5["Building the Airflow DAG"]
    C --> S6["Creating SparkApplication jobs"]
```

## Chapter 8: Generative AI on Kubernetes

**Questions this chapter answers:**
- What does this chapter explain about Chapter 11: Generative AI on Kubernetes?
- What does this chapter explain about Technical requirements?
- What does this chapter explain about What generative AI is and what it is not?

**Key points:**
- Source section: Chapter 11: Generative AI on Kubernetes.
- Source section: Technical requirements.
- Source section: What generative AI is and what it is not.
- Source section: The power of large neural networks.

```mermaid
flowchart TD
    C["Generative AI on Kubernetes"]
    C --> S1["Chapter 11: Generative AI on Kubernetes"]
    C --> S2["Technical requirements"]
    C --> S3["What generative AI is and what it is not"]
    C --> S4["The power of large neural networks"]
    C --> S5["Challenges and limitations"]
    C --> S6["Using Amazon Bedrock to work with foundational models"]
```

## Chapter 9: Where to Go from Here

**Questions this chapter answers:**
- What does this chapter explain about Chapter 12: Where to Go from Here?
- What does this chapter explain about Important topics for big data in Kubernetes?
- What does this chapter explain about Kubernetes monitoring and application monitoring?

**Key points:**
- Source section: Chapter 12: Where to Go from Here.
- Source section: Important topics for big data in Kubernetes.
- Source section: Kubernetes monitoring and application monitoring.
- Source section: Building a service mesh.

```mermaid
flowchart TD
    C["Where to Go from Here"]
    C --> S1["Chapter 12: Where to Go from Here"]
    C --> S2["Important topics for big data in Kubernetes"]
    C --> S3["Kubernetes monitoring and application monitoring"]
    C --> S4["Building a service mesh"]
    C --> S5["Security considerations"]
    C --> S6["Automated scalability"]
```

## Chapter 10: Getting Started with Containers

**Questions this chapter answers:**
- What does this chapter explain about Chapter 1: Getting Started with Containers?
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Container architecture?

**Key points:**
- Source section: Chapter 1: Getting Started with Containers.
- Source section: Technical requirements.
- Source section: Container architecture.
- Source section: Installing Docker.

```mermaid
flowchart TD
    C["Getting Started with Containers"]
    C --> S1["Chapter 1: Getting Started with Containers"]
    C --> S2["Technical requirements"]
    C --> S3["Container architecture"]
    C --> S4["Installing Docker"]
    C --> S5["Windows"]
    C --> S6["macOS"]
```

## Chapter 11: Kubernetes Architecture

**Questions this chapter answers:**
- What does this chapter explain about Chapter 2: Kubernetes Architecture?
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Control plane?

**Key points:**
- Source section: Chapter 2: Kubernetes Architecture.
- Source section: Technical requirements.
- Source section: Control plane.
- Source section: Node components.

```mermaid
flowchart TD
    C["Kubernetes Architecture"]
    C --> S1["Chapter 2: Kubernetes Architecture"]
    C --> S2["Technical requirements"]
    C --> S3["Control plane"]
    C --> S4["Node components"]
    C --> S5["Pods"]
    C --> S6["Deployments"]
```

## Chapter 12: Getting Hands-On with Kubernetes

**Questions this chapter answers:**
- What does this chapter explain about Chapter 3: Getting Hands-On with Kubernetes?
- What does this chapter explain about Technical requirements?
- What does this chapter explain about Installing kubectl?

**Key points:**
- Source section: Chapter 3: Getting Hands-On with Kubernetes.
- Source section: Technical requirements.
- Source section: Installing kubectl.
- Source section: Deploying a local cluster using Kind.

```mermaid
flowchart TD
    C["Getting Hands-On with Kubernetes"]
    C --> S1["Chapter 3: Getting Hands-On with Kubernetes"]
    C --> S2["Technical requirements"]
    C --> S3["Installing kubectl"]
    C --> S4["Deploying a local cluster using Kind"]
    C --> S5["Installing kind"]
    C --> S6["Deploying the cluster"]
```
