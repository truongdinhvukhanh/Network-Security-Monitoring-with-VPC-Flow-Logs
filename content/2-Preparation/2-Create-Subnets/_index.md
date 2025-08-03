---
title : "Create Subnets"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

{{% notice note %}}
In this lab, creating public and private subnets within your VPC is essential for segmenting your network. The public subnet will host resources like the Bastion Host that require internet access, while the private subnet will securely house internal resources like your OpenSearch domain, ensuring they are not directly exposed to the internet. This setup enhances security and organizes your network for the planned architecture.
{{% /notice %}}

#### Create Public Subnet
1. Access the subnet creation interface:
    - Navigate to the **VPC** console
    - Select **Subnets** from the left navigation panel
    - Click **Create subnet**
    ![image.png](../images/2/2.2/image.png)
2. Select your VPC:
    - In the **Create subnet** interface, select the **NSM-VPC** from the dropdown
    ![image.png](../images/2/2.2/image%201.png)
3. Configure your public subnet:
    - **Subnet name**: Enter `NSM-Public-Subnet`
    - **Availability Zone**: Select `us-east-1a`
    - **IPv4 CIDR block:** Enter `10.0.1.0/24`
    - Click **Create subnet**
    ![image.png](../images/2/2.2/image%202.png)
4. Verify successful subnet creation:
    - You should see a success message
    - Your new subnet will appear in the subnet list
    ![image.png](../images/2/2.2/image%203.png)
5. Enable automatic public IP assignment for public subnet
    - Select **NSM-Public-Subnet** from the subnet list
    - Click **Actions** > **Edit subnet settings**
    ![image.png](../images/2/2.2/image%204.png)
6. Configure auto-assign IP settings:
    - Under **Auto-assign IP settings**, check **Enable auto-assign public IPv4 address**
    - Click **Save**
    ![image.png](../images/2/2.2/image%205.png)
    ![image.png](../images/2/2.2/image%206.png)
#### Create Private Subnet
1. Click **Create subnet**    
    ![image.png](../images/2/2.2/image%207.png)
2. Enter the following details:
    - **VPC ID:** Select **NSM-VPC** from the dropdown
    - **Subnet name:** Enter `NSM-Private-Subnet`
    - **Availability Zone:** Select `us-east-1a`
    - **IPv4 CIDR block:** Enter `10.0.2.0/24`
3. Click **Create subnet**
    ![image.png](../images/2/2.2/image%208.png)
    ![image.png](../images/2/2.2/image%209.png)