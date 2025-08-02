---
title : "Create EC2 Bastion"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

#### Overview of EC2 Bastion Host Setup

In this section, we will set up and connect to an EC2 Bastion Host. A Bastion Host acts as a secure intermediary server that provides controlled access to your private network resources from an external network (like the internet). This is a critical component for securely managing instances located in private subnets, ensuring that direct SSH access to internal servers is minimized, thereby enhancing your overall cloud security posture.

#### Key Concepts:

* **EC2 Instance:** A virtual server in the Amazon Elastic Compute Cloud (EC2) for running applications.
* **Bastion Host:** A server that acts as a secure gateway to a private network, allowing controlled access to internal resources.
* **Key Pair:** A set of security credentials (public and private keys) used to prove your identity when connecting to EC2 instances.
* **SSH (Secure Shell):** A cryptographic network protocol for secure data communication, remote command-line login, and other secure network services.

#### Table of Contents:

* [3.1 Launch an EC2 Instance as a Bastion Host](/3-Create-EC2-Bastion/1-Launch-an-EC2-Instance-as-a-Bastion-Host/_index.md)
* [3.2 Connect to the Bastion Host via SSH](/3-Create-EC2-Bastion/2-Connect-to-the-Bastion-Host-via-SSH/_index.md)