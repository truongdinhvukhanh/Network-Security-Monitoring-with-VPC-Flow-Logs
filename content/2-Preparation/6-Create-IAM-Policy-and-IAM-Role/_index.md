---
title : "Create IAM Policy and IAM Role"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 2.6 </b> "
---

{{% notice note %}}
In this lab, creating a dedicated IAM Policy (**NSM-Firehose-Policy**) and an IAM Role (**NSM-Firehose-Role**) is critical for securely enabling the Kinesis Firehose service to interact with other AWS resources like S3 and OpenSearch. This ensures that Firehose has *only* the necessary permissions to deliver data to its intended destinations without over-privileging, adhering to the principle of least privilege, which is essential for a secure architecture.
{{% /notice %}}

#### Create IAM Firehose Policy
1. Navigate to the **IAM Console**:
    - Navigate to the [AWS Management Console](https://aws.amazon.com/console/)
    - Search for and select **IAM** in the services search bar    
    ![image.png](../images/2/2.6/image.png)    
2. Initiate policy creation:
    - Navigate to **Policies** in the left navigation pane
    - Click **Create policy**    
    ![image.png](../images/2/2.6/image%201.png)    
3. Specify permissions:
    - Select the **JSON** tab
    - Paste the following **JSON** into the **JSON tab**        
        ```json
        {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": [
                        "s3:AbortMultipartUpload",
                        "s3:GetBucketLocation",
                        "s3:GetObject",
                        "s3:ListBucket",
                        "s3:ListBucketMultipartUploads",
                        "s3:PutObject"
                    ],
                    "Resource": [
                        "arn:aws:s3:::*",
                        "arn:aws:s3:::*/*"
                    ]
                },
                {
                    "Effect": "Allow",
                    "Action": [
                        "es:DescribeDomain",
                        "es:DescribeDomains",
                        "es:DescribeDomainConfig",
                        "es:ESHttpPost",
                        "es:ESHttpPut",
                        "es:ESHttpGet"
                    ],
                    "Resource": [
                        "arn:aws:es:*:*:domain/*"
                    ]
                },
                {
                    "Effect": "Allow",
                    "Action": [
                        "ec2:DescribeVpcs",
                        "ec2:DescribeVpcAttribute",
                        "ec2:DescribeSubnets",
                        "ec2:DescribeSecurityGroups",
                        "ec2:DescribeNetworkInterfaces",
                        "ec2:CreateNetworkInterface",
                        "ec2:CreateNetworkInterfacePermission",
                        "ec2:DeleteNetworkInterface"
                    ],
                    "Resource": "*"
                },
                {
                    "Effect": "Allow",
                    "Action": [
                        "logs:PutLogEvents"
                    ],
                    "Resource": [
                        "arn:aws:logs:*:*:log-group:/aws/kinesisfirehose/*:*"
                    ]
                }
            ]
        }
        ```    
    ![image.png](../images/2/2.6/image%202.png)    
    - Click **Next**:    
    ![image.png](../images/2/2.6/image%203.png)    
4. Configure policy details:
    - **Policy name:** Enter `NSM-Firehose-Policy`    
    ![image.png](../images/2/2.6/image%204.png)    
5. Review and create
    - Click **Create policy**    
    ![image.png](../images/2/2.6/image%205.png)    
6. Verify successful creation:
    - You should see a success message
    - Your new security group will be added in the list    
    ![image.png](../images/2/2.6/image%206.png)
#### Create IAM Firehose Roles
1. Create a new role:
    - In the left navigation pane, select **Roles**
    - Click **Create role**    
    ![image.png](../images/2/2.6/image%207.png)    
2. Select the trusted entity:
    - **Trusted entity type:** Choose **AWS service**
    - **Use case:** Search for and select `Firehose`
    - Click **Next**    
    ![image.png](../images/2/2.6/image%208.png)    
3. Add permissions:
    - Search for and select your custom Policy: `NSM-Firehose-Policy`
    - Click **Next**
    ![image.png](../images/2/2.6/image%209.png)
4. Configure role details:
    - **Role name:** Enter `NSM-Firehose-Role`
    - **Description:** Enter `Allows Firehose to deliver data to OpenSearch and S3`
    - Review the trust policy and permissions    
    ![image.png](../images/2/2.6/image%2010.png)
5. Review and create:
    - Verify all configurations are correct
    - Click **Create role**    
    ![image.png](../images/2/2.6/image%2011.png)    
6. Confirm role creation:
    - You should see a success message
    - The role is now ready for use    
    ![image.png](../images/2/2.6/image%2012.png)