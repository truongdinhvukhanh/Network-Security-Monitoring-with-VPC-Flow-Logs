---
title : "Create and configure OpenSearch Service"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

#### Overview of OpenSearch Service Setup

In this section, we will deploy and configure an Amazon OpenSearch Service domain. OpenSearch Service is a managed service that makes it easy to deploy, operate, and scale OpenSearch clusters in the AWS Cloud. For this workshop, OpenSearch will serve as the analytics engine and full-text search platform for your VPC Flow Logs, enabling you to store, search, and visualize network traffic data. You will configure the domain for private access within your VPC and set up an ingest pipeline to parse the incoming flow log data.

#### Key Concepts:

* **Amazon OpenSearch Service:** A managed service for deploying, operating, and scaling OpenSearch clusters.
* **OpenSearch Domain:** Your OpenSearch cluster, including data nodes, storage, and networking configurations.
* **Ingest Pipeline:** A series of processors that transform documents before they are indexed in OpenSearch.
* **Grok Processor:** A powerful tool within ingest pipelines used to parse unstructured log data into structured fields.
* **Index Template:** A way to automatically apply settings and mappings to new indices based on matching patterns.

#### Table of Contents:

* [5.1 Create OpenSearch Service Domain](/5-Create-and-configure-OpenSearch-Service/1-Create-OpenSearch-Service-Domain/_index.md)
* [5.2 Create Ingest Pipeline](/5-Create-and-configure-OpenSearch-Service/2-Create-Ingest-Pipeline/_index.md)