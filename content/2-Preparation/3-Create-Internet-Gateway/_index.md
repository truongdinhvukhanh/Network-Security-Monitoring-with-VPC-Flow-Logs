---
title : "Create Internet Gateway"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---

{{% notice note %}}
An Internet Gateway (IGW) is crucial for this lab as it enables the public subnet within your **NSM-VPC** to communicate with the internet. This is a prerequisite for resources like the Bastion Host in the public subnet to be accessible for management and for any public services to function as intended.
{{% /notice %}}

#### Step-by-Step Internet Gateway Creation

1. Access the Internet Gateway interface:
    - Navigate to the **VPC** console
    - Select **Internet Gateways** from the left navigation panel
    - Click **Create internet gateway**
    ![image.png](../images/2/2.3/image.png)
2. Configure your Internet Gateway:
    - Enter **Name tag**: `NSM-IGW`
    - Click **Create internet gateway**
    ![image.png](../images/2/2.3/image%201.png)
3. Verify successful Internet Gateway creation:
    - You should see a success message
    - Your new Internet Gateway will appear in the list
    ![image.png](../images/2/2.3/image%202.png)
4. Attach the Internet Gateway to your VPC:
    - Select your newly created Internet Gateway
    - Click **Actions** dropdown
    - Select **Attach to VPC**
    - Choose the **NSM-VPC** from the dropdown
    - Click **Attach internet gateway**
    ![image.png](../images/2/2.3/image%203.png)
5. Confirm successful attachment:
    - The **State** of your Internet Gateway should change to **Attached**
    - This indicates the Internet Gateway is now operational with your VPC
    ![image.png](../images/2/2.3/image%204.png)