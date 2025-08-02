---
title : "Create VPC Flow Log"
date : "`r Sys.Date()`"
weight : 7
chapter : false
pre : " <b> 7. </b> "
---

{{% notice note %}}
In this section, you will configure VPC Flow Logs to capture detailed information about the IP traffic going to and from network interfaces in your Virtual Private Cloud (VPC). This is a crucial step for network monitoring, security analysis, and troubleshooting within your AWS environment. The VPC Flow Logs will be configured to send all traffic data directly to the Kinesis Data Firehose stream you previously set up, ensuring real-time ingestion into your OpenSearch Service domain for immediate analysis and visualization.
{{% /notice %}}

#### Creating a VPC Flow Log for Network Monitoring
1. Navigate to the [AWS Management Console](https://aws.amazon.com/console/)
    - In the search bar, find and select **VPC**    
    ![image.png](/images/7/image.png)    
2. Create flow log
    - Select your **NSM-VPC**
    - Choose the **Flow logs** tab
    - Click **Create flow log**    
    ![image.png](/images/7/image%201.png)    
3. Configure the flow log:
    - **Filter**: All (captures all traffic)
    - **Maximum aggregation interval:** 1 minute
    - **Destination**: Send to Amazon Data Firehose in the same account
    - **Firehose delivery stream:** Select **NSM-FlowLogs-Firehose** from the dropdown
    - **Log format:** AWS default format
    ![image.png](/images/7/image%202.png)    
4. Click **Create flow log**
    ![image.png](/images/7/image%203.png)