---
title : "Introduction"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 1. </b> "
---

#### Overview of the Lab: Network Security Monitoring with VPC Flow Logs

{{% notice note %}}
This lab guides you through building a comprehensive network monitoring solution on AWS using VPC Flow Logs, Kinesis Data Firehose, Amazon OpenSearch Service, and Amazon S3. You will learn to capture, ingest, store, analyze, and visualize network traffic data from your Virtual Private Cloud (VPC). This architecture provides deep insights into network security, operational health, and enables proactive troubleshooting and threat detection.
{{% /notice %}}

#### Architecture Diagram

![Architecture Diagram](../../../static/images/Simple.drawio.png)

The diagram above illustrates the architecture we will implement:

1.  **User Access (1):** An administrator connects securely to the Bastion Host.
2.  **Bastion Host (2):** A secure EC2 instance in the public subnet acts as a jump server to access resources in the private subnet.
3.  **VPC Flow Logs (3):** Network traffic metadata from the VPC is captured and sent to Kinesis Data Firehose.
4.  **Amazon Kinesis Data Firehose (4):** A fully managed service that collects and delivers VPC Flow Logs to both Amazon OpenSearch Service and Amazon S3.
5.  **Amazon OpenSearch Service (5):** Processes and indexes the flow log data for real-time analysis and visualization via OpenSearch Dashboards.
6.  **Amazon S3 (6):** Provides durable and cost-effective storage for raw VPC Flow Logs, serving as a backup and a data source for Amazon Athena.
7.  **Amazon Athena (7):** An interactive query service that allows you to analyze flow log data directly from S3 using standard SQL.

#### Lab Breakdown: What You Will Do?

This workshop is structured into several key parts, each focusing on a specific component of the solution:

* **Part 2: Preparation:**
    You will set up the fundamental AWS network infrastructure, including creating a Virtual Private Cloud (VPC), defining public and private subnets, establishing an Internet Gateway, configuring route tables, and creating essential security groups. You will also create necessary IAM policies and roles to grant appropriate permissions to AWS services.

* **Part 3: Create EC2 Bastion:**
    You will launch and configure an EC2 instance to serve as a Bastion Host. This host will provide secure SSH access to your private network, enabling you to manage resources within your private subnets.

* **Part 4: Create S3 Bucket:**
    You will create an Amazon S3 bucket. This bucket will act as the durable storage destination for your raw VPC Flow Logs, ensuring data retention and providing a source for further analysis.

* **Part 5: Create and configure OpenSearch Service:**
    You will deploy an Amazon OpenSearch Service domain. This managed service will be configured to ingest, store, and allow for real-time analysis of your flow log data, along with setting up an ingest pipeline for data parsing.

* **Part 6: Create Kinesis Data Firehose:**
    You will set up an Amazon Kinesis Data Firehose delivery stream. This stream will be configured to automatically capture VPC Flow Logs and deliver them to both your OpenSearch Service domain and your S3 bucket.

* **Part 7: Create VPC Flow Log:**
    You will enable and configure VPC Flow Logs for your `NSM-VPC`. This step ensures that all network traffic within your VPC is captured and routed to the Kinesis Data Firehose stream for processing.

* **Part 8: Verify data flow and create Dashboard:**
    You will verify that the entire data pipeline is functioning correctly by checking data ingestion into OpenSearch and then create insightful dashboards in OpenSearch Dashboards to visualize and analyze your VPC Flow Logs.

* **Part 9: Query logs with Athena:**
    You will learn how to use Amazon Athena to query the raw VPC Flow Logs stored in your S3 bucket, performing ad-hoc analysis using standard SQL.

* **Part 10: Clean up resources:**
    Finally, you will follow steps to systematically remove all the AWS resources provisioned during this workshop to avoid any ongoing charges.

#### Contents:

* [Part 2: Preparation](/2-Preparation/_index.md)
* [Part 3: Create EC2 Bastion](/3-Create-EC2-Bastion/_index.md)
* [Part 4: Create S3 Bucket](/4-Create-S3-Bucket/_index.md)
* [Part 5: Create and configure OpenSearch Service](/5-Create-and-configure-OpenSearch-Service/_index.md)
* [Part 6: Create Kinesis Data Firehose](/6-Create-Kinesis-Data-Firehose/_index.md)
* [Part 7: Create VPC Flow Log](/7-Create-VPC-Flow-Log/_index.md)
* [Part 8: Verify data flow and create Dashboard](/8-Verify-data-flow-and-create-Dashboard/_index.md)
* [Part 9: Query logs with Athena](/9-Query-logs-with-Athena/_index.md)
* [Part 10: Clean up resources](/10-Clean-up-resources/_index.md)