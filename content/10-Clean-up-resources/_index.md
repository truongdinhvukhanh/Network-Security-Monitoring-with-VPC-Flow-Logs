---
title : "Clean up resources"
date : "`r Sys.Date()`"
weight : 10
chapter : false
pre : " <b> 10. </b> "
---

{{% notice note %}}
In this final section, you will learn how to properly clean up all the AWS resources provisioned throughout this lab. It is crucial to delete these resources to avoid incurring unnecessary costs and to maintain a tidy AWS account. This step-by-step guide ensures that you systematically remove all components of the network monitoring solution, from Firehose streams and EC2 instances to OpenSearch domains, VPCs, S3 buckets, and IAM roles/policies.
{{% /notice %}}

#### Delete Firehose Stream
- Navigate to [https://us-east-1.console.aws.amazon.com/firehose](https://us-east-1.console.aws.amazon.com/firehose)
- Select **NSM-FlowLogs-Firehose** stream
- Click **Delete**    
    ![image.png](image.png)    
- Type `NSM-FlowLogs-Firehose` and click **Delete**    
    ![image.png](image%201.png)
#### Delete Bastion Hose
- Navigate to [https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#Instances](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#Instances:)
- Select **NSM-Bastion-Host**
- Click **Instance state → Terminate (delete) instance**    
    ![image.png](image%202.png)    
- Click **Terminate (delete)**    
    ![image.png](image%203.png)
#### Delete OpenSearch Domain
- Navigate to [https://us-east-1.console.aws.amazon.com/aos/home?region=us-east-1#opensearch/dashboard](https://us-east-1.console.aws.amazon.com/aos/home?region=us-east-1#opensearch/dashboard)
- Select **nsm-opensearch**    
    ![image.png](image%204.png)    
- Click **Delete**    
    ![image.png](image%205.png)    
- Type `nsm-opensearch` and click **Delete**    
    ![image.png](image%206.png)    
- Waiting for **opensearch domain** to delete successfully    
    ![image.png](image%207.png)
#### Delete VPC
- Navigate to [https://us-east-1.console.aws.amazon.com/vpcconsole/home?region=us-east-1#vpcs:](https://us-east-1.console.aws.amazon.com/vpcconsole/home?region=us-east-1#vpcs:)
- Select **NSM-VPC**
- Click **Actions → Delete VPC**    
    ![image.png](image%208.png)    
- Type `delete` and click **Delete**    
    ![image.png](image%209.png)
#### Delete Elastic IP
- Select **Elastic IP** from the left navigation panel
- Select **Elastic IP**
- Click **Actions → Release Elastic IP addresses → Release**    
    ![image.png](image%2010.png)    
    ![image.png](image%2011.png)
#### Delete S3 Bucket
- Navigate to [https://us-east-1.console.aws.amazon.com/s3](https://us-east-1.console.aws.amazon.com/s3)
- Select your bucket (**nsm-flow-logs-YYYYMMDD**) → Click **Empty**    
    ![image.png](image%2012.png)    
- Type `permanently delete` *→* **Empty**    
    ![image.png](image%2013.png)    
- Click **Exit**    
    ![image.png](image%2014.png)    
- Select your bucket again (**nsm-flow-logs-YYYYMMDD**) → Click **Delete**    
    ![image.png](image%2015.png)    
- Type your bucket name → Click **Delete bucket**    
    ![image.png](image%2016.png)
#### Delete IAM Role and IAM Policy
- Navigate to [https://us-east-1.console.aws.amazon.com/iam](https://us-east-1.console.aws.amazon.com/iam/home#/home)
- Select **Role** from the left navigation panel
- Select **NSM-Firehose-Role**
- Click **Delete**    
    ![image.png](image%2017.png)    
- Type `NSM-Firehose-Role` → Click **Delete**
![image.png](image%2018.png)
- Select **Policies** from the left navigation panel
- Search for and select **NSM-Firehose-Policy**
- Click **Delete**
![image.png](image%2019.png)
- Type `NSM-Firehose-Policy` **→** Click **Delete**
![image.png](image%2020.png)