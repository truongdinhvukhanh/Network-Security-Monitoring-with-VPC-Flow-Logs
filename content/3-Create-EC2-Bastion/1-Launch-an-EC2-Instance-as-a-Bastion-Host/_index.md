---
title : "Launch an EC2 Instance as a Bastion Host"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 3.1 </b> "
---

{{% notice note %}}
In this step, you will launch an EC2 instance that will serve as your Bastion Host. This host is essential for securely accessing other EC2 instances and resources located in private subnets within your VPC, which do not have direct internet access. Setting up a Bastion Host centralizes access points, enhances security by reducing the attack surface, and provides a controlled entry point for administrative tasks in your private network.
{{% /notice %}}

1. Sign in to the [AWS Management Console](https://aws.amazon.com/console/)
    - In the search bar, type **EC2**
    - Select **EC2** from the services list    
    ![image.png](image.png)    
2. In the EC2 dashboard:
    - Click on **Instances** in the navigation pane
    - Click **Launch instances**    
    ![image.png](image%201.png)    
3. Name and Tags
    - **Name:** Enter `NSM-Bastion-Host`    
    ![image.png](image%202.png)    
4. Select the Amazon Machine Image (AMI):
    - Under **Quick Start**, select **Amazon Linux**
    - Choose **Amazon Linux 2023** from the available options    
    ![image.png](image%203.png)    
5. Choose instance specifications:
    - Choose **t2.micro**
    ![image.png](image%204.png)    
6. Create a Key Pair
    - Click **Create new key pair**        
        ![image.png](image%205.png)        
    - **Key pair name**: `NSM-Key`
    - **Key pair type**: Select **RSA**
    - **Private key file format:** Select **.pem**
    - Click **Create key pair**
    - **Important**: This file will be downloaded only once. Store it safely    
    ![image.png](image%206.png)    
7. Configure Network Settings
    - Click **Edit** in the Network settings section
    - **VPC:** Select your **NSM-VPC**
    - **Subnet:** Select your `NSM-Public-Subnet`
    - **Auto-assign public IP:** Enable
    - **Firewall (security groups):** Select existing security group
    - Choose `SG-Bastion` from the dropdown    
    ![image.png](image%207.png)    
8. **Review and Launch**
    - Review your settings
    - Click **Launch instance**
    ![image.png](image%208.png)    
9. **Wait for Instance to Initialize**
    - Click **View all instances**
    ![image.png](image%209.png)    
    - Wait until the **Instance state** shows "Running" and **Status checks** shows "2/2 checks passed"
    - Note the **Public IPv4 address** of your instance    
    ![image.png](image%2010.png)