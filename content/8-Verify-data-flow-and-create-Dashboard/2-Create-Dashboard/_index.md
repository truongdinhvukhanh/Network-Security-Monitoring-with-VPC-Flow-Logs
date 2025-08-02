---
title : "Create Dashboard"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 8.2 </b> "
---

{{% notice note %}}
In this step, you will create a dashboard in OpenSearch Dashboards to visualize your VPC Flow Logs data. Building a dashboard helps you easily monitor and analyze network traffic patterns, identify anomalies, and gain deeper insights into your VPC's network activity through intuitive charts and statistics.
{{% /notice %}}

#### Create Visualizations and Dashboard
1. **Create a New Index Pattern**
    - In the left sidebar, click on **Dashboards Management**        
        ![image.png](/images/8/8.2/image.png)        
    - Click on **Index patterns**
    - Click **Create index pattern**        
        ![image.png](/images/8/8.2/image%201.png)        
    - **Index pattern name:** Enter `vpc-flow-logs*`
    - Click **Next step**        
        ![image.png](/images/8/8.2/image%202.png)        
    - **Time field:** Select **start**
    - Click **Create index pattern**        
        ![image.png](/images/8/8.2/image%203.png)        
        ![image.png](/images/8/8.2/image%204.png)        
2. **Create a Pie Chart for Traffic by Source IP**
    - In the left sidebar, click on **Visualize**        
        ![image.png](/images/8/8.2/image%205.png)        
    - Click **Create visualization**        
        ![image.png](/images/8/8.2/image%206.png)        
    - Select **Pie** as the visualization type        
        ![image.png](/images/8/8.2/image%207.png)       
    - Select your index pattern        
        ![image.png](/images/8/8.2/image%208.png)        
    - Under **Buckets**, click **Add →** **Split slices**        
        ![image.png](/images/8/8.2/image%209.png)        
    - **Aggregation:** Select **Terms**
    - **Field:** Select **srcaddr** (source IP address)
    - **Size:** 10
    - Click **Update** to see the visualization        
        ![image.png](/images/8/8.2/image%2010.png)        
    - Click **Save** and name it `Top Source IPs`        
        ![image.png](/images/8/8.2/image%2011.png)        
        ![image.png](/images/8/8.2/image%2012.png)        
3. **Create a Bar Chart for Traffic by Destination Port**
    - Return to **Visualizations List**        
        ![image.png](/images/8/8.2/image%2013.png)        
    - Click **Create visualization**        
        ![image.png](/images/8/8.2/image%2014.png)        
    - Select **Vertical bar** as the visualization type        
        ![image.png](/images/8/8.2/image%2015.png)        
    - Select your index pattern        
        ![image.png](/images/8/8.2/image%2016.png)        
    - Under **Buckets**, click **Add** → **X-axis**        
        ![image.png](/images/8/8.2/image%2017.png)        
    - **Aggregation:** Select **Terms**
    - **Field:** Select **dstport** (destination port)
    - **Size:** 10 (top 10 destination ports)
    - Click **Update** to see the visualization        
        ![image.png](/images/8/8.2/image%2018.png)        
    - Click **Save** and name it `Top Destination Ports`        
        ![image.png](/images/8/8.2/image%2019.png)        
        ![image.png](/images/8/8.2/image%2020.png)        
4. **Create a Line Chart for Traffic Over Time**
    - Return to **Visualizations List**        
        ![image.png](/images/8/8.2/image%2021.png)        
    - Click **Create visualization**        
        ![image.png](/images/8/8.2/image%2022.png)        
    - Select **Line** as the visualization type        
        ![image.png](/images/8/8.2/image%2023.png)        
    - Select your index pattern        
        ![image.png](/images/8/8.2/image%2024.png)        
    - Under **Buckets**, click **Add → X-axis**        
        ![image.png](/images/8/8.2/image%2025.png)        
    - **Aggregation:** Select **Date Histogram**
    - **Field:** Select **start**
    - **Interval:** Select **Auto**
    - Click **Update** to see the visualization        
        ![image.png](/images/8/8.2/image%2026.png)        
    - Click **Save** and name it `Traffic Over Time`        
        ![image.png](/images/8/8.2/image%2027.png)    
    ![image.png](/images/8/8.2/image%2028.png)    
5. **Create a New Dashboard**
    - In the left sidebar, click on **Dashboard**        
        ![image.png](/images/8/8.2/image%2029.png)        
    - Click **Create new dashboard**        
        ![image.png](/images/8/8.2/image%2030.png)        
    - Click **Add** in the top right        
        ![image.png](/images/8/8.2/image%2031.png)        
    - Select all the visualizations you created:
        - **Top Source IPs**
        - **Top Destination Ports**
        - **Traffic Over Time**        
        ![image.png](/images/8/8.2/image%2032.png)        
    - Arrange the visualizations by dragging and resizing them
- Click **Save** in the top right    
    ![image.png](/images/8/8.2/image%2033.png)    
- Name it `VPC Flow Logs Dashboard`    
    ![image.png](/images/8/8.2/image%2034.png)