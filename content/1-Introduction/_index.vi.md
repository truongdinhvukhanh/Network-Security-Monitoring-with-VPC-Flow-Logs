---
title : "Giới thiệu"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 1. </b> "
---

#### Tổng quan về Lab: Giám sát an ninh mạng với VPC Flow Logs

{{% notice note %}}
Lab này sẽ hướng dẫn bạn xây dựng một giải pháp giám sát mạng toàn diện trên AWS bằng cách sử dụng VPC Flow Logs, Kinesis Data Firehose, Amazon OpenSearch Service và Amazon S3. Bạn sẽ học cách thu thập, đưa vào, lưu trữ, phân tích và trực quan hóa dữ liệu lưu lượng mạng từ Virtual Private Cloud (VPC) của bạn. Kiến trúc này cung cấp cái nhìn sâu sắc về bảo mật mạng, tình trạng hoạt động và cho phép khắc phục sự cố cũng như phát hiện mối đe dọa một cách chủ động.
{{% /notice %}}

#### Sơ đồ kiến trúc

![Architecture Diagram](../../images/Simple.drawio.png)

Sơ đồ trên minh họa kiến trúc chúng ta sẽ triển khai:

1.  **Truy cập người dùng (1):** Một quản trị viên kết nối an toàn với Bastion Host.
2.  **Bastion Host (2):** Một EC2 instance bảo mật trong public subnet hoạt động như một jump server để truy cập tài nguyên trong private subnet.
3.  **VPC Flow Logs (3):** Metadata lưu lượng mạng từ VPC được thu thập và gửi đến Kinesis Data Firehose.
4.  **Amazon Kinesis Data Firehose (4):** Một dịch vụ được quản lý hoàn toàn để thu thập và chuyển VPC Flow Logs đến cả Amazon OpenSearch Service và Amazon S3.
5.  **Amazon OpenSearch Service (5):** Xử lý và lập chỉ mục dữ liệu nhật ký luồng để phân tích và trực quan hóa theo thời gian thực thông qua OpenSearch Dashboards.
6.  **Amazon S3 (6):** Cung cấp lưu trữ bền vững và hiệu quả chi phí cho VPC Flow Logs thô, đóng vai trò sao lưu và là nguồn dữ liệu cho Amazon Athena.
7.  **Amazon Athena (7):** Một dịch vụ truy vấn tương tác cho phép bạn phân tích dữ liệu nhật ký luồng trực tiếp từ S3 bằng SQL tiêu chuẩn.

#### Chi tiết Lab: Bạn sẽ làm gì?

Workshop này được cấu trúc thành một số phần chính, mỗi phần tập trung vào một thành phần cụ thể của giải pháp:

* **Phần 2: Chuẩn bị:**
    Bạn sẽ thiết lập hạ tầng mạng AWS cơ bản, bao gồm tạo Virtual Private Cloud (VPC), định nghĩa public và private subnets, thiết lập Internet Gateway, cấu hình route tables và tạo các security groups cần thiết. Bạn cũng sẽ tạo các IAM policies và roles cần thiết để cấp quyền phù hợp cho các dịch vụ AWS.

* **Phần 3: Tạo EC2 Bastion:**
    Bạn sẽ khởi chạy và cấu hình một EC2 instance để đóng vai trò là Bastion Host. Host này sẽ cung cấp quyền truy cập SSH an toàn vào mạng riêng của bạn, cho phép bạn quản lý tài nguyên trong private subnets của mình.

* **Phần 4: Tạo S3 Bucket:**
    Bạn sẽ tạo một Amazon S3 bucket. Bucket này sẽ đóng vai trò là đích lưu trữ bền vững cho VPC Flow Logs thô của bạn, đảm bảo việc lưu giữ dữ liệu và cung cấp nguồn cho các phân tích sâu hơn.

* **Phần 5: Tạo và cấu hình OpenSearch Service:**
    Bạn sẽ triển khai một Amazon OpenSearch Service domain. Dịch vụ được quản lý này sẽ được cấu hình để đưa vào, lưu trữ và cho phép phân tích dữ liệu nhật ký luồng của bạn theo thời gian thực, cùng với việc thiết lập một ingest pipeline để phân tích cú pháp dữ liệu.

* **Phần 6: Tạo Kinesis Data Firehose:**
    Bạn sẽ thiết lập một Amazon Kinesis Data Firehose delivery stream. Stream này sẽ được cấu hình để tự động thu thập VPC Flow Logs và gửi chúng đến cả OpenSearch Service domain và S3 bucket của bạn.

* **Phần 7: Tạo VPC Flow Log:**
    Bạn sẽ bật và cấu hình VPC Flow Logs cho `NSM-VPC` của mình. Bước này đảm bảo rằng tất cả lưu lượng mạng trong VPC của bạn được thu thập và chuyển đến Kinesis Data Firehose stream để xử lý.

* **Phần 8: Xác minh luồng dữ liệu và tạo Dashboard:**
    Bạn sẽ xác minh rằng toàn bộ data pipeline đang hoạt động chính xác bằng cách kiểm tra việc đưa dữ liệu vào OpenSearch và sau đó tạo các dashboards đầy đủ thông tin trong OpenSearch Dashboards để trực quan hóa và phân tích VPC Flow Logs của bạn.

* **Phần 9: Truy vấn nhật ký với Athena:**
    Bạn sẽ học cách sử dụng Amazon Athena để truy vấn các VPC Flow Logs thô được lưu trữ trong S3 bucket của bạn, thực hiện phân tích ad-hoc bằng SQL tiêu chuẩn.

* **Phần 10: Dọn dẹp tài nguyên:**
    Cuối cùng, bạn sẽ làm theo các bước để loại bỏ có hệ thống tất cả các tài nguyên AWS đã được cung cấp trong buổi workshop này để tránh bất kỳ chi phí phát sinh nào.

#### Nội dung:

* [Phần 2: Chuẩn bị](/2-Preparation/_index.md)
* [Phần 3: Tạo EC2 Bastion](/3-Create-EC2-Bastion/_index.md)
* [Phần 4: Tạo S3 Bucket](/4-Create-S3-Bucket/_index.md)
* [Phần 5: Tạo và cấu hình OpenSearch Service](/5-Create-and-configure-OpenSearch-Service/_index.md)
* [Phần 6: Tạo Kinesis Data Firehose](/6-Create-Kinesis-Data-Firehose/_index.md)
* [Phần 7: Tạo VPC Flow Log](/7-Create-VPC-Flow-Log/_index.md)
* [Phần 8: Xác minh luồng dữ liệu và tạo Dashboard](/8-Verify-data-flow-and-create-Dashboard/_index.md)
* [Phần 9: Truy vấn nhật ký với Athena](/9-Query-logs-with-Athena/_index.md)
* [Phần 10: Dọn dẹp tài nguyên](/10-Clean-up-resources/_index.md)