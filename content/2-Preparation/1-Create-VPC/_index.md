---
title : "Create VPC"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---

{{% notice note %}}
Creating an Amazon Virtual Private Cloud (VPC) is the foundational step for this lab. It provides a logically isolated virtual network that you define, acting as the secure and private environment where all your project's AWS resources (such as subnets, instances, and services) will reside. This isolation ensures that your resources are contained within your control and not exposed to the public internet unless explicitly configured.
{{% /notice %}}

#### Step-by-Step VPC Creation

1. Navigate to the [AWS Management Console](https://aws.amazon.com/console/)
    - In the search bar, find and select **VPC**
    ![image.png](../../images/2/2.1/image.png)
2. Initiate VPC creation:
    - Select **Your VPCs** from the left navigation panel
    - Click on **Create VPC** button in the top-right corner
    ![image.png](../images/2/2.1/image%201.png)
3. Configure your VPC settings:
    - Under **Resources to create**, select **VPC only**
    - Enter **Name tag**:  `NSM-VPC`
    - Set **IPv4 CIDR block**: `10.0.0.0/16`
    ![image.png](../images/2/2.1/image%202.png)
4. Complete the VPC creation:
    - Review your settings
    - Click **Create VPC**
    ![image.png](../images/2/2.1/image%203.png)
5. Verify successful VPC creation:
    - You should see a success message
    - Your new VPC will appear in the VPC list
    ![image.png](../images/2/2.1/image%204.png)