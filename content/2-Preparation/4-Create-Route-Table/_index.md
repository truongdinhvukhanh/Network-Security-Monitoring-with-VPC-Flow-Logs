---
title : "Create Route Table"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 2.4 </b> "
---

{{% notice note %}}
In this lab, configuring a Route Table is vital for directing traffic to and from your subnets. Specifically, we will create a route table that routes all internet-bound traffic from your **NSM-Public-Subnet** through the **NSM-IGW** you just created. This ensures that resources in the public subnet can send and receive data from the internet, which is necessary for their intended functionality.
{{% /notice %}}

#### Step-by-Step Route Table Creation
1. Access the Route Table interface:
    - Navigate to the **VPC** console
    - Select **Route Tables** from the left navigation panel
    - Click **Create route table**
    ![image.png](/images/2/2.4/image.png)
2. Configure your Route Table:
    - Enter **Name**: `NSM-Public-RT`
    - Select **VPC**: Choose the **NSM-VPC** from the dropdown
    - Click **Create route table**    
    ![image.png](/images/2/2.4/image%201.png)    
3. Verify successful Route Table creation:
    - You should see a success message
    - Your new Route Table will appear in the list    
    ![image.png](/images/2/2.4/image%202.png)    
4. Modify the routes in your Route Table:
    - Select your newly created Route Table
    - Click **Actions** dropdown
    - Select **Edit routes**    
    ![image.png](/images/2/2.4/image%203.png)    
5. Add an Internet route:
    - Click **Add route**
    - For **Destination**, enter **`0.0.0.0/0`** (represents all IPv4 traffic)
    - For **Target**, select **Internet Gateway** and choose **NSM-IGW**
    - Click **Save changes**    
    ![image.png](/images/2/2.4/image%204.png)    
6. Associate the Route Table with your public subnet:
    - Select the **Subnet associations** tab
    - Click **Edit subnet associations**    
    ![image.png](/images/2/2.4/image%205.png)    
7. Select the appropriate subnets:
    - Select the **NSM-Public-Subnet** you created earlier
    - Click **Save associations**    
    ![image.png](/images/2/2.4/image%206.png)    
8. Confirm your subnet associations:
    - Review the associated subnets in the Subnet associations tab
    - The public subnet is now configured to route internet traffic through the Internet Gateway    
    ![image.png](/images/2/2.4/image%207.png)