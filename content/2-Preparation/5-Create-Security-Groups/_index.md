---
title : "Create Security Groups"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 2.5 </b> "
---

{{% notice note %}}
Security Groups are fundamental to defining the network access control for the various components in this lab. By creating **SG-Bastion**, **SG-Firehos**, and **SG-OpenSearch**, we establish granular control over what traffic is allowed to reach your instances and services. This ensures that only authorized access (e.g., SSH to Bastion, Firehose to OpenSearch) is permitted, thereby enhancing the overall security posture of your deployed solution.
{{% /notice %}}

#### Bastion Security Group
1. Access the Security Group interface:
    - Navigate to the **VPC** console
    - Select **Security Groups** from the left navigation panel
    - Click **Create security group**    
    ![image.png](../images/2/2.5/image.png) 
2. Configure the Bastion Security Group:
    - **Security group name**: Enter `SG-Bastion`
    - **Description**: Enter `Security group for Bastion Host access`
    - **VPC**: Select the **NSM-VPC** from the dropdown    
    ![image.png](../images/2/2.5/image%201.png)    
3. Define inbound rules:
    - Click **Add rule**
    - Configure SSH access:
        - **Type**: Select **SSH**
        - **Source**: Select **My IP** (automatically uses your current public IPv4 address)    
    ![image.png](../images/2/2.5/image%202.png)    
4. Review outbound rules:
    - By default, all outbound traffic is allowed
    - Click **Create security group**    
    ![image.png](../images/2/2.5/image%203.png)    
5. Verify successful creation:
    - You should see a success message
    - Your new security group will appear in the list    
    ![image.png](../images/2/2.5/image%204.png)
#### Firehose Security Group
1. Initiate another security group creation:
    - Navigate back to **Security Groups**
    - Click **Create security group**    
    ![image.png](../images/2/2.5/image%205.png)    
2. Configure the Firehose Security Group:
    - **Security group name**: Enter `SG-Firehose`
    - **Description**: Enter `Security group for Firehose`
    - **VPC**: Select the **NSM-VPC** from the dropdown    
    ![image.png](../images/2/2.5/image%206.png)    
3. Complete the security group creation:
    - Review your settings
    - Click **Create security group**    
    ![image.png](../images/2/2.5/image%207.png)    
4. Verify successful creation:
    - You should see a success message
    - Your new security group will appear in the list    
    ![image.png](../images/2/2.5/image%208.png)
#### OpenSearch Security Group
1. Initiate another security group creation:
    - Navigate back to **Security Groups**
    - Click **Create security group**    
    ![image.png](../images/2/2.5/image%209.png)    
2. Configure the OpenSearch Security Group:
    - **Security group name**: Enter `SG-OpenSearch`
    - **Description**: Enter `Security group for OpenSearch domain access`
    - **VPC**: Select the **NSM-VPC** from the dropdown    
    ![image.png](../images/2/2.5/image%2010.png)    
3. Define inbound rules:
    - Click **Add rule**
    - Configure HTTPs access for Bastion:
        - **Type**: Select **SSH**
        - **Source**: Select **Custom**
        - Select the security group ID of **SG-Bastion** you just created    
    ![image.png](../images/2/2.5/image%2011.png)    
    - Click **Add rule** again
    - Configure HTTPs access for Firehose:
        - **Type**: Select **SSH**
        - **Source**: Select **Custom**
        - Select the security group ID of **SG-Firehose** you just created    
    ![image.png](../images/2/2.5/image%2012.png)    
4. Complete the security group creation:
    - Review your settings
    - Click **Create security group**    
    ![image.png](../images/2/2.5/image%2013.png)    
5. Verify three security groups:
    - Confirm three security groups appear in your list
    - You now have dedicated security groups for Bastion, Firehose and OpenSearch resources    
    ![image.png](../images/2/2.5/image%2014.png)