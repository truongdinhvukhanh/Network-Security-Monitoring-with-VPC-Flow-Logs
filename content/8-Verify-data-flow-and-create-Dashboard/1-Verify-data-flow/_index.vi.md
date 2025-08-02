---
title : "Xác minh luồng dữ liệu"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 8.1 </b> "
---

{{% notice note %}}
Trong bước này, bạn sẽ xác minh rằng VPC Flow Logs đang được thu thập và gửi thành công đến Amazon OpenSearch Service thông qua Kinesis Data Firehose. Việc kiểm tra luồng dữ liệu này là rất cần thiết để đảm bảo toàn bộ đường ống giám sát mạng của bạn đang hoạt động như mong đợi, cung cấp dữ liệu mạng theo thời gian thực để phân tích và trực quan hóa sau này.
{{% /notice %}}

#### Xác minh việc nhập dữ liệu vào OpenSearch Dashboards
1. Tạo lưu lượng mạng để kiểm tra
    Trước khi xác minh luồng dữ liệu, hãy đảm bảo bạn có một số lưu lượng mạng để phân tích:
    - SSH vào Bastion Host của bạn bằng cặp khóa của bạn
    - Từ Bastion Host, hãy thử kết nối với các tài nguyên khác trong VPC của bạn
    - Chạy một số lệnh mạng cơ bản như `ping`, `curl` hoặc `wget`
    ![image.png](/images/8/8.1/image.png)
    - Chờ khoảng 5 - 10 phút

2. Xác minh việc gửi qua Kinesis Data Firehose
    - Điều hướng đến [**Amazon Kinesis console**](https://us-east-1.console.aws.amazon.com/firehose)
    - Chọn luồng **NSM-FlowLogs-Firehose** của bạn
    ![image.png](/images/8/8.1/image%201.png)
    - Nhấp vào tab **Monitoring**
    ![image.png](/images/8/8.1/image%202.png)
    - Tìm kiếm:
        - **Incoming records** (phải lớn hơn 0)
        - **Incoming bytes** (phải lớn hơn 0)
        - **S3 delivery success** (phải khớp với số bản ghi đến)
        - **OpenSearch delivery success** (phải khớp với số bản ghi đến)
    ![image.png](/images/8/8.1/image%203.png)
3. Kiểm tra lỗi
    - Tìm kiếm bất kỳ nhật ký lỗi nào:
        - **Destination error logs**
        - **Backup error logs**
    - Nếu bạn thấy lỗi, hãy kiểm tra nhật ký CloudWatch cho luồng Firehose của bạn
    ![image.png](/images/8/8.1/image%204.png)
4. Xác minh việc gửi đến S3 Bucket
    - Điều hướng đến [the AWS S3 Console](https://us-east-1.console.aws.amazon.com/s3)
    - Nhấp vào tên S3 bucket của bạn
    ![image.png](/images/8/8.1/image%205.png)
    - Điều hướng qua cấu trúc tiền tố bạn đã cấu hình (ví dụ: `flow-logs/year=2025/month=07/day=22/hour=17/`)
    - Bạn sẽ thấy các tệp có dấu thời gian tương ứng với thời điểm nhật ký luồng của bạn được tạo
    ![image.png](/images/8/8.1/image%206.png)
5. Xác minh việc gửi đến OpenSearch Service
    - Quay lại: `https://localhost:9200/_dashboards/`
    - Trong **Dev Tools**
    - Chạy lệnh sau để liệt kê tất cả các chỉ mục:
        ```
        GET _cat/indices?v
        ```
    - Tìm kiếm các chỉ mục khớp với mẫu chỉ mục bạn đã cấu hình (ví dụ: `vpc-flow-logs`)
    - Xác minh rằng chỉ mục có các tài liệu (cột **docs.count** phải lớn hơn 0)
    ![image.png](/images/8/8.1/image%207.png)