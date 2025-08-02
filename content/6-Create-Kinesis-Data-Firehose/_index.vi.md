---
title : "Tạo Kinesis Data Firehose"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 6. </b> "
---

{{% notice note %}}
Trong phần này, bạn sẽ tạo và cấu hình một **Amazon Kinesis Data Firehose delivery stream**. Luồng Firehose này là một thành phần quan trọng sẽ tự động thu thập, chuyển đổi và tải dữ liệu VPC Flow Logs của bạn từ một nguồn Direct PUT vào **Amazon OpenSearch Service domain** của bạn và cũng sao lưu dữ liệu vào **S3 bucket** của bạn. Firehose đơn giản hóa quá trình truyền dữ liệu đáng tin cậy đến các đích khác nhau, đảm bảo rằng dữ liệu đo lường mạng của bạn được thu thập hiệu quả và sẵn sàng để phân tích.
{{% /notice %}}

#### Tạo Kinesis Data Firehose Delivery Stream
1. Đăng nhập vào [AWS Management Console](https://aws.amazon.com/console/)
    - Trong thanh tìm kiếm, gõ `Firehose`
    - Chọn **Amazon Data Firehose** từ danh sách dịch vụ
    ![image.png](/images/6/image.png)
2. Tạo luồng Firehose
    - Chọn **Firehose streams** từ ngăn điều hướng bên trái
    - Nhấp **Create Firehose stream**
    ![image.png](/images/6/image%201.png)
3. Chọn nguồn và đích
    - **Source:** Chọn **Direct PUT**
    - **Destination:** Chọn **Amazon OpenSearch Service**
    ![image.png](/images/6/image%202.png)
4. **Firehose stream name:** Nhập `NSM-FlowLogs-Firehose`
    ![image.png](/images/6/image%203.png)
5. Cấu hình cài đặt đích
    - **OpenSearch Service domain:**
        - Nhấp **Browse**
        ![image.png](/images/6/image%204.png)
        - Chọn **nsm-opensearch** và nhấp **Choose**
        ![image.png](/images/6/image%205.png)
    - **Index:** Nhập `vpc-flow-logs`
    - **Index rotation:** Chọn **Every day**
    ![image.png](/images/6/image%206.png)
6. **Kết nối VPC đích**
    - **VPC:** `NSM-VPC`
    - **Subnets:** `NSM-Private-Subnet`
    - **Security groups:** Chọn `SG-Firehose`
    ![image.png](/images/6/image%207.png)
7. Cài đặt sao lưu
    - **Source record backup in Amazon S3:** Chọn **All data**
    - **S3 backup bucket:**
        - Nhấp **Browse**
        ![image.png](/images/6/image%208.png)
        - Chọn S3 Bucket của bạn (`nsm-flow-logs-YYYYMMDD`) và nhấp **Choose**
        ![image.png](/images/6/image%209.png)
    - **S3 prefix**
        ```
        flow-logs/year=!{timestamp:yyyy}/month=!{timestamp:MM}/day=!{timestamp:dd}/hour=!{timestamp:HH}/
        ```
    - **S3 error output prefix:** `errors/`
    ![image.png](/images/6/image%2010.png)
8. Cài đặt Nâng cao
    - **Service access**
        - Chọn **Choose existing IAM role**
        - Chọn **NSM-Firehose-Role** từ danh sách thả xuống
    ![image.png](/images/6/image%2011.png)
9. Tạo
    - Nhấp **Create delivery stream** ở cuối trang
    - Chờ cho trạng thái luồng phân phối thay đổi thành **Active**
    ![image.png](/images/6/image%2012.png)
    ![image.png](/images/6/image%2013.png)