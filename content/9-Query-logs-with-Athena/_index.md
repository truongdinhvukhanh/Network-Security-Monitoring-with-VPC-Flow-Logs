---
title : "Query logs with Athena"
date : "`r Sys.Date()`"
weight : 9
chapter : false
pre : " <b> 9. </b> "
---

{{% notice note %}}
In this section, you will utilize Amazon Athena to query the VPC Flow Logs stored in your S3 bucket. Athena is an interactive query service that makes it easy to analyze data directly in Amazon S3 using standard SQL. This step demonstrates how to efficiently perform ad-hoc analysis on your raw flow log data, providing an alternative or complementary method to OpenSearch for deep dive investigations and custom reporting on your network traffic.
{{% /notice %}}

#### Querying VPC Flow Logs with Amazon Athena
1. Configure Athena Query Results Location
    - Navigate to [Athena Console](https://console.aws.amazon.com/athena/)
    - **First-time setup**: If this is your first time, click **"Explore the query editor"**
    - Click **Settings** tab at the top
    - Click **Manage**        
        ![image.png](../images/9/image.png)        
    - Enter S3 location: `s3://nsm-flow-logs-YYYYMMDD/athena-results/`
    
        (replace **nsm-flow-logs-YYYYMMDD** with your actual bucket name)
    - Click **Save**        
        ![image.png](../images/9/image%201.png)
2. Create Database    
    - In the Athena **Query Editor**, run this command:    
    ```sql
    CREATE DATABASE IF NOT EXISTS vpc_flow_logs_db;
    ```    
    ![image.png](../images/9/image%202.png)    
    ![image.png](../images/9/image%203.png)    

3. Create VPC Flow Logs Table    
    - Run this command    
    ```sql
    CREATE EXTERNAL TABLE vpc_flow_logs_db.vpc_flow_logs (
      version int,
      account_id string,
      interface_id string,
      srcaddr string,
      dstaddr string,
      srcport int,
      dstport int,
      protocol int,
      packets bigint,
      bytes bigint,
      windowstart bigint,
      windowend bigint,
      action string,
      flowlogstatus string
    )
    ROW FORMAT DELIMITED
    FIELDS TERMINATED BY ' '
    LOCATION 's3://nsm-flow-logs-20250727/flow-logs/'
    TBLPROPERTIES (
      'skip.header.line.count'='0'
    );
    ```    
    ![image.png](../images/9/image%204.png)    
4. Verify Table Creation    
    ```sql
    SHOW TABLES;
    ```    
    ![image.png](../images/9/image%205.png)    
5. Test with Sample Queries
    - Basic Data Exploration        
        ```sql
        -- View first 10 records to understand your data structure
        SELECT *
        FROM vpc_flow_logs
        LIMIT 10;
        ```        
        ![image.png](../images/9/image%206.png)        
    - Count Total Records        
        ```sql
        -- Count total flow log records
        SELECT COUNT(*) as total_records
        FROM vpc_flow_logs;
        ```        
        ![image.png](../images/9/image%207.png)        
    - Data Quality Check        
        ```sql
        -- Check for different actions in your logs
        SELECT 
            action,
            COUNT(*) as count
        FROM vpc_flow_logs
        GROUP BY action;
        ```        
        ![image.png](../images/9/image%208.png)        
6. Example Queries for Analysis
    - SSH Traffic Analysis (Port 22)        
        ```sql
        -- Find SSH connection attempts
        SELECT 
            srcaddr,
            dstaddr,
            action,
            packets,
            bytes,
            from_unixtime(windowstart) as start_time,
            from_unixtime(windowend) as end_time
        FROM vpc_flow_logs
        WHERE dstport = 22
        ORDER BY windowstart DESC
        LIMIT 20;
        ```        
        ![image.png](../images/9/image%209.png)        
    - Rejected Connections Analysis        
        ```sql
        -- Analyze rejected connections
        SELECT 
            srcaddr,
            dstaddr,
            dstport,
            COUNT(*) as rejected_count
        FROM vpc_flow_logs
        WHERE action = 'REJECT'
        GROUP BY srcaddr, dstaddr, dstport
        ORDER BY rejected_count DESC
        LIMIT 15;
        ```        
        ![image.png](../images/9/image%2010.png)        
7. View Query Results in S3
    - Navigate to [https://s3.console.aws.amazon.com/](https://s3.console.aws.amazon.com/)
    - Navigate to bucket: `nsm-flow-logs-YYYY-MM-DD`        
        ![image.png](../images/9/image%2011.png)        
    - Open folder: `athena-results/`        
        ![image.png](../images/9/image%2012.png)        
        ![image.png](../images/9/image%2013.png)