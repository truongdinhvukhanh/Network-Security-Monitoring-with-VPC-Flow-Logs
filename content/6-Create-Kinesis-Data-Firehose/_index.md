---
title : "Create Kinesis Data Firehose"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 6. </b> "
---

{{% notice note %}}
In this section, you will create and configure an Amazon Kinesis Data Firehose delivery stream. This Firehose stream is a critical component that will automatically capture, transform, and load your VPC Flow Logs data from a direct PUT source into your Amazon OpenSearch Service domain and also back up the data to your S3 bucket. Firehose simplifies the process of reliably streaming data to various destinations, ensuring your network telemetry is efficiently collected and made available for analysis.
{{% /notice %}}

#### Creating a Kinesis Data Firehose Delivery Stream
1. Sign in to the [AWS Management Console](https://aws.amazon.com/console/)
    - In the search bar, type `Firehose`
    - Select **Amazon Data Firehose** from the services list    
    ![image.png](image.png)    
2. Create Firehose stream
    - Select **Firehose streams** from the left navigation pane
    - Click **Create Firehose stream**    
    ![image.png](image%201.png)    
3. Choose source and destination
    - **Source:** Select **Direct PUT**
    - **Destination:** Select **Amazon OpenSearch Service**    
    ![image.png](image%202.png)    
4. **Firehose stream name:** Enter `NSM-FlowLogs-Firehose`    
    ![image.png](image%203.png)    
5. Configure Destination Settings
    - **OpenSearch Service domain:**
        - Click **Browse**            
            ![image.png](image%204.png)            
        - Select **nsm-opensearch** and click **Choose**            
            ![image.png](image%205.png)            
    - **Index:** Enter `vpc-flow-logs`
    - **Index rotation:** Select **Every day**        
        ![image.png](image%206.png)        
6. **Destination VPC connectivity**
    - **VPC:** `NSM-VPC`
    - **Subnets:** `NSM-Private-Subnet`
    - **Security groups:** Select `SG-Firehose`        
        ![image.png](image%207.png)        
7. Backup settings
    - **Source record backup in Amazon S3:** Select **All data**
    - **S3 backup bucket:**
        - Click **Browse**            
            ![image.png](image%208.png)            
        - Choose your S3 Bucket (`nsm-flow-logs-YYYYMMDD`) and click **Choose**            
            ![image.png](image%209.png)            
    - **S3 prefix**        
        ```
        flow-logs/year=!{timestamp:yyyy}/month=!{timestamp:MM}/day=!{timestamp:dd}/hour=!{timestamp:HH}/
        ```        
    - **S3 error output prefix:** `errors/`    
    ![image.png](image%2010.png)    
8. Advanced Settings
    - **Service access**
        - Select **Choose existing IAM role**
        - Select **NSM-Firehose-Role** from the dropdown    
    ![image.png](image%2011.png)    
9. Create
    - Click **Create delivery stream** at the bottom of the page
    - Wait for the delivery stream status to change to **Active**    
    ![image.png](image%2012.png)    
    ![image.png](image%2013.png)