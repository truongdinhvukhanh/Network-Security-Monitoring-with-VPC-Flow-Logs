---
title : "Giám sát an ninh mạng với VPC Flow Logs"
date :  "`r Sys.Date()`"
weight : 1
chapter : false
---
# Giám sát an ninh mạng với VPC Flow Logs
#### Tổng quan

Trong bài lab này, bạn sẽ học cách xây dựng một giải pháp **giám sát an ninh mạng toàn diện** trên Amazon Web Services (AWS). Bạn sẽ triển khai một **pipeline đầu cuối** để thu thập, đưa vào, lưu trữ, phân tích và trực quan hóa **VPC Flow Logs**, giúp tăng cường khả năng hiển thị và bảo mật cho hạ tầng đám mây của bạn. Giải pháp này sẽ cung cấp cho bạn **kinh nghiệm thực tế** trong việc tận dụng các dịch vụ AWS chính để đạt được khả năng quan sát mạng mạnh mẽ.

#### Các Module của bài lab

1.  [Giới thiệu](/1-Introduction/_index.md)
2.  [Các bước chuẩn bị](/2-Preparation/_index.md)
3.  [Tạo EC2 Bastion](/3-Create-EC2-Bastion/_index.md)
4.  [Tạo S3 Bucket](/4-Create-S3-Bucket/_index.md)
5.  [Tạo và cấu hình OpenSearch Service](/5-Create-and-configure-OpenSearch-Service/_index.md)
6.  [Tạo Kinesis Data Firehose](/6-Create-Kinesis-Data-Firehose/_index.md)
7.  [Tạo VPC Flow Log](/7-Create-VPC-Flow-Log/_index.md)
8.  [Xác minh luồng dữ liệu và tạo Dashboard](/8-Verify-data-flow-and-create-Dashboard/_index.md)
9.  [Truy vấn log với Athena](/9-Query-logs-with-Athena/_index.md)
10. [Dọn dẹp tài nguyên](/10-Clean-up-resources/_index.md)

{{% notice tip %}}
Hãy đảm bảo bạn hoàn thành module "Dọn dẹp tài nguyên" sau khi kết thúc bài lab để tránh phát sinh bất kỳ chi phí không mong muốn nào trên tài khoản AWS của bạn. Các tài nguyên AWS tiếp tục phát sinh chi phí cho đến khi chúng được chấm dứt hoặc xóa bỏ đúng cách.
{{% /notice %}}