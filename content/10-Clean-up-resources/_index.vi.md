---
title : "Dọn dẹp tài nguyên"
date : "`r Sys.Date()`"
weight : 10
chapter : false
pre : " <b> 10. </b> "
---

{{% notice note %}}
Trong phần cuối cùng này, bạn sẽ tìm hiểu cách dọn dẹp đúng cách tất cả các tài nguyên AWS đã được cấp phát trong suốt bài lab này. Điều quan trọng là phải xóa các tài nguyên này để tránh phát sinh chi phí không cần thiết và để duy trì một tài khoản AWS gọn gàng. Hướng dẫn từng bước này đảm bảo rằng bạn loại bỏ một cách có hệ thống tất cả các thành phần của giải pháp giám sát mạng, từ Firehose streams và EC2 instances đến OpenSearch domains, VPCs, S3 buckets và IAM roles/policies.
{{% /notice %}}

#### Xóa Firehose Stream
- Điều hướng đến [https://us-east-1.console.aws.amazon.com/firehose](https://us-east-1.console.aws.amazon.com/firehose)
- Chọn luồng **NSM-FlowLogs-Firehose**
- Nhấp **Delete**
    ![image.png](../images/10/image.png)
- Gõ `NSM-FlowLogs-Firehose` và nhấp **Delete**
    ![image.png](../images/10/image%201.png)
#### Xóa Bastion Host
- Điều hướng đến [https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#Instances](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#Instances:)
- Chọn **NSM-Bastion-Host**
- Nhấp **Instance state → Terminate (delete) instance**
    ![image.png](../images/10/image%202.png)
- Nhấp **Terminate (delete)**
    ![image.png](../images/10/image%203.png)
#### Xóa OpenSearch Domain
- Điều hướng đến [https://us-east-1.console.aws.amazon.com/aos/home?region=us-east-1#opensearch/dashboard](https://us-east-1.console.aws.amazon.com/aos/home?region=us-east-1#opensearch/dashboard)
- Chọn **nsm-opensearch**
    ![image.png](../images/10/image%204.png)
- Nhấp **Delete**
    ![image.png](../images/10/image%205.png)
- Gõ `nsm-opensearch` và nhấp **Delete**
    ![image.png](../images/10/image%206.png)
- Đợi cho **opensearch domain** xóa thành công
    ![image.png](../images/10/image%207.png)
#### Xóa VPC
- Điều hướng đến [https://us-east-1.console.aws.amazon.com/vpcconsole/home?region=us-east-1#vpcs:](https://us-east-1.console.aws.amazon.com/vpcconsole/home?region=us-east-1#vpcs:)
- Chọn **NSM-VPC**
- Nhấp **Actions → Delete VPC**
    ![image.png](../images/10/image%208.png)
- Gõ `delete` và nhấp **Delete**
    ![image.png](../images/10/image%209.png)
#### Xóa Elastic IP
- Chọn **Elastic IP** từ bảng điều hướng bên trái
- Chọn **Elastic IP**
- Nhấp **Actions → Release Elastic IP addresses → Release**
    ![image.png](../images/10/image%2010.png)
    ![image.png](../images/10/image%2011.png)
#### Xóa S3 Bucket
- Điều hướng đến [https://us-east-1.console.aws.amazon.com/s3](https://us-east-1.console.aws.amazon.com/s3)
- Chọn bucket của bạn (**nsm-flow-logs-YYYYMMDD**) → Nhấp **Empty**
    ![image.png](../images/10/image%2012.png)
- Gõ `permanently delete` *→* **Empty**
    ![image.png](../images/10/image%2013.png)
- Nhấp **Exit**
    ![image.png](../images/10/image%2014.png)
- Chọn lại bucket của bạn (**nsm-flow-logs-YYYYMMDD**) → Nhấp **Delete**
    ![image.png](../images/10/image%2015.png)
- Gõ tên bucket của bạn → Nhấp **Delete bucket**
    ![image.png](../images/10/image%2016.png)
#### Xóa IAM Role và IAM Policy
- Điều hướng đến [https://us-east-1.console.aws.amazon.com/iam](https://us-east-1.console.aws.amazon.com/iam/home#/home)
- Chọn **Role** từ bảng điều hướng bên trái
- Chọn **NSM-Firehose-Role**
- Nhấp **Delete**
    ![image.png](../images/10/image%2017.png)
- Gõ `NSM-Firehose-Role` → Nhấp **Delete**
![image.png](../images/10/image%2018.png)
- Chọn **Policies** từ bảng điều hướng bên trái
- Tìm kiếm và chọn **NSM-Firehose-Policy**
- Nhấp **Delete**
![image.png](../images/10/image%2019.png)
- Gõ `NSM-Firehose-Policy` **→** Nhấp **Delete**
![image.png](../images/10/image%2020.png)