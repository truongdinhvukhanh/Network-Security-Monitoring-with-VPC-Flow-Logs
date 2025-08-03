---
title : "Create S3 Bucket"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

{{% notice note %}}
In this section, you will create an Amazon S3 (Simple Storage Service) bucket. This S3 bucket is a crucial component of our project's architecture as it will serve as the primary storage destination for the data processed by Kinesis Firehose. S3 provides highly durable, scalable, and secure object storage, making it an ideal choice for reliably storing raw or processed data before further analysis or long-term archiving.
{{% /notice %}}

#### Create the S3 Bucket
1. Sign in to the AWS Management Console
    - In the search bar, type **S3**
    - Select **S3** from the services list    
    ![image.png](../../images/4/image.png)    
2. In the **S3** interface, select **Create bucket**    
    ![image.png](../../images/4/image%201.png)    
3. In the **Create bucket** interface
    - **Bucket type:** Select **General purpose**
    - **Bucket name**: Type `nsm-flow-logs-YYYYMMDD` (replace YYYYMMDD with today's date to ensure uniqueness)    
    ![image.png](../../images/4/image%202.png)    
4. Click **Create bucket**   
    ![image.png](../../images/4/image%203.png)    
    ![image.png](../../images/4/image%204.png)  
#### Create Folder Structure for Organized Data Storage
1. Select your newly created bucket    
    ![image.png](../../images/4/image%205.png)    
2. Scroll down and click **Create folder**   
    ![image.png](../../images/4/image%206.png)    
3. Create the following folders:
    - `flow-logs` (for VPC Flow Logs data)       
        ![image.png](../../images/4/image%207.png)        
    - `athena-results` (for storing Athena query results)        
        ![image.png](../../images/4/image%208.png)        
4. Verify two foders was created successfully    
    ![image.png](../../images/4/image%209.png)  
#### Configure Bucket Policy for Firehose Access
1. Go to the **Permissions** tab
2. Scroll down to **Bucket policy** and click **Edit**
    ![image.png](../../images/4/image%2010.png)    
3. Copy and paste the following policy, replacing the placeholders:    
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "AllowFirehoseDelivery",
                "Effect": "Allow",
                "Principal": {
                    "Service": "firehose.amazonaws.com"
                },
                "Action": [
                    "s3:AbortMultipartUpload",
                    "s3:GetBucketLocation",
                    "s3:GetObject",
                    "s3:ListBucket",
                    "s3:ListBucketMultipartUploads",
                    "s3:PutObject"
                ],
                "Resource": [
                    "arn:aws:s3:::nsm-flow-logs-YYYYMMDD",
                    "arn:aws:s3:::nsm-flow-logs-YYYYMMDD/*"
                ],
                "Condition": {
                    "StringEquals": {
                        "aws:SourceAccount": "YOUR-ACCOUNT-ID"
                    },
                    "ArnLike": {
                        "aws:SourceArn": "arn:aws:firehose:us-east-1:YOUR-ACCOUNT-ID:deliverystream/*"
                    }
                }
            },
            {
                "Sid": "AllowAthenaAccess",
                "Effect": "Allow",
                "Principal": {
                    "Service": "athena.amazonaws.com"
                },
                "Action": [
                    "s3:GetBucketLocation",
                    "s3:GetObject",
                    "s3:ListBucket",
                    "s3:ListBucketMultipartUploads",
                    "s3:ListMultipartUploadParts",
                    "s3:AbortMultipartUpload",
                    "s3:PutObject"
                ],
                "Resource": [
                    "arn:aws:s3:::nsm-flow-logs-YYYYMMDD",
                    "arn:aws:s3:::nsm-flow-logs-YYYYMMDD/*"
                ]
            }
        ]
    }
    ```    
    Replace:    
    - `nsm-flow-logs-YYYYMMDD` with your actual bucket name (4 places)
    - `YOUR-ACCOUNT-ID` with your AWS account ID (found in the top-right corner of the AWS console)
    - Ensure the region matches your setup (us-east-1 in this example)    
    ![image.png](../../images/4/image%2011.png)    
4. Click **Save changes** 
    ![image.png](../../images/4/image%2012.png)