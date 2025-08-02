---
title : "Xác minh luồng dữ liệu và tạo Dashboard"
date : "`r Sys.Date()`"
weight : 8
chapter : false
pre : " <b> 8. </b> "
---

#### Tổng quan về Xác minh Luồng Dữ liệu và Tạo Dashboard

{{% notice note %}}
Trong phần này, chúng ta sẽ xác minh luồng dữ liệu VPC Flow Logs từ nguồn đến Amazon OpenSearch Service và tạo một bảng điều khiển để trực quan hóa dữ liệu này. Đây là bước cuối cùng để đảm bảo toàn bộ kiến trúc giám sát mạng của bạn đang hoạt động chính xác, cho phép bạn dễ dàng tìm kiếm, phân tích và giám sát lưu lượng mạng trong VPC của mình thông qua các biểu đồ và số liệu tùy chỉnh.
{{% /notice %}}

#### Các khái niệm chính:

* **Amazon OpenSearch Service:** Một dịch vụ được quản lý để triển khai, vận hành và mở rộng các OpenSearch clusters.
* **OpenSearch Dashboards:** Giao diện người dùng dựa trên web cho OpenSearch để trực quan hóa và quản lý dữ liệu.
* **Index Pattern:** Một mẫu được sử dụng trong OpenSearch Dashboards để xác định các chỉ mục bạn muốn khám phá và trực quan hóa.
* **Discover:** Một tính năng của OpenSearch Dashboards cho phép bạn tìm kiếm, lọc và khám phá dữ liệu thô.
* **Visualization:** Các biểu đồ và đồ thị được tạo từ dữ liệu trong OpenSearch để trình bày thông tin một cách trực quan.
* **Dashboard:** Một tập hợp các visualization được sắp xếp trên một trang duy nhất để cung cấp cái nhìn tổng quan về dữ liệu.

#### Mục lục:

* [8.1 Xác minh luồng dữ liệu](/8-Verify-data-flow-and-create-Dashboard/1-Verify-data-flow/_index.md)
* [8.2 Tạo Dashboard](/8-Verify-data-flow-and-create-Dashboard/2-Create-Dashboard/_index.md)