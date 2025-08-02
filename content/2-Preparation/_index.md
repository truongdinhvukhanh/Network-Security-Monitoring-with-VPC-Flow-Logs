---
title : "Preparation"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

#### Overview of Preparation Steps

In this section, we will establish the foundational AWS infrastructure required for our workshop. This includes setting up a Virtual Private Cloud (VPC) with its subnets, configuring internet connectivity using an Internet Gateway and Route Tables, defining network security with Security Groups, and creating necessary IAM policies and roles for service permissions. These steps are crucial for building a secure, scalable, and functional environment for your AWS resources.

#### Key Concepts:

* **Virtual Private Cloud (VPC):** A logically isolated virtual network within AWS where you can launch AWS resources.
* **Subnets:** Segments of a VPC's IP address range where you can place groups of isolated resources, categorized as public (internet-accessible) or private (internal only).
* **Internet Gateway (IGW):** A VPC component that enables communication between your VPC and the internet.
* **Route Table:** A set of rules that determine where network traffic from your subnet or gateway is directed.
* **Security Groups:** Virtual firewalls for your Amazon EC2 instances that control inbound and outbound traffic based on rules.
* **IAM Policy:** A document that defines permissions, specifying who can access which AWS resources and under what conditions.
* **IAM Role:** An AWS identity with permission policies that determine what the identity can and cannot do in AWS. Roles are assumed by trusted entities.

#### Contents:

* [2.1 Create VPC](/2-Preparation/1-Create-VPC/_index.md)
* [2.2 Create Subnets](/2-Preparation/2-Create-Subnets/_index.md)
* [2.3 Create Internet Gateway](/2-Preparation/3-Create-Internet-Gateway/_index.md)
* [2.4 Create Route Table](/2-Preparation/4-Create-Route-Table/_index.md)
* [2.5 Create Security Groups](/2-Preparation/5-Create-Security-Groups/_index.md)
* [2.6 Create IAM Policy and IAM Role](/2-Preparation/6-Create-IAM-Policy-and-IAM-Role/_index.md)
