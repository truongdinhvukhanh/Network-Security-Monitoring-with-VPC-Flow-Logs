---
title : "Verify data flow and create Dashboard"
date : "`r Sys.Date()`"
weight : 8
chapter : false
pre : " <b> 8. </b> "
---

#### Overview of Data Flow Verification and Dashboard Creation

{{% notice note %}}
In this section, we will verify the VPC Flow Logs data flow from its source to Amazon OpenSearch Service and create a dashboard to visualize this data. This is the final step to ensure your entire network monitoring architecture is functioning correctly, allowing you to easily search, analyze, and monitor network traffic within your VPC through custom charts and metrics.
{{% /notice %}}

#### Key Concepts:

* **Amazon OpenSearch Service:** A managed service for deploying, operating, and scaling OpenSearch clusters.
* **OpenSearch Dashboards:** A web-based user interface for OpenSearch to visualize and manage data.
* **Index Pattern:** A pattern used in OpenSearch Dashboards to identify the indices you want to explore and visualize.
* **Discover:** An OpenSearch Dashboards feature that allows you to search, filter, and explore raw data.
* **Visualization:** Charts and graphs created from data in OpenSearch to present information visually.
* **Dashboard:** A collection of visualizations arranged on a single page to provide an overview of the data.

#### Table of Contents:

* [8.1 Verify data flow](/8-Verify-data-flow-and-create-Dashboard/1-Verify-data-flow/_index.md)
* [8.2 Create Dashboard](/8-Verify-data-flow-and-create-Dashboard/2-Create-Dashboard/_index.md)