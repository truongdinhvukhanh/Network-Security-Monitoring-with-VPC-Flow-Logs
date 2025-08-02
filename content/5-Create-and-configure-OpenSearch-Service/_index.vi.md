---
title : "Tạo và cấu hình OpenSearch Service"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

#### Tổng quan về Thiết lập OpenSearch Service

Trong phần này, chúng ta sẽ triển khai và cấu hình một **Amazon OpenSearch Service domain**. OpenSearch Service là một dịch vụ được quản lý giúp dễ dàng triển khai, vận hành và mở rộng các OpenSearch cluster trong AWS Cloud. Đối với workshop này, OpenSearch sẽ đóng vai trò là công cụ phân tích và nền tảng tìm kiếm toàn văn bản cho VPC Flow Logs của bạn, cho phép bạn lưu trữ, tìm kiếm và trực quan hóa dữ liệu lưu lượng mạng. Bạn sẽ cấu hình domain để truy cập riêng tư trong VPC của mình và thiết lập một ingest pipeline để phân tích cú pháp dữ liệu nhật ký luồng đến.

#### Các khái niệm chính:

* **Amazon OpenSearch Service:** Một dịch vụ được quản lý để triển khai, vận hành và mở rộng các OpenSearch clusters.
* **OpenSearch Domain:** OpenSearch cluster của bạn, bao gồm các data nodes, storage và cấu hình mạng.
* **Ingest Pipeline:** Một chuỗi các bộ xử lý giúp biến đổi tài liệu trước khi chúng được lập chỉ mục trong OpenSearch.
* **Grok Processor:** Một công cụ mạnh mẽ trong ingest pipelines được sử dụng để phân tích dữ liệu nhật ký không có cấu trúc thành các trường có cấu trúc.
* **Index Template:** Một cách để tự động áp dụng các cài đặt và ánh xạ cho các chỉ mục mới dựa trên các mẫu phù hợp.

#### Mục lục:

* [5.1 Tạo OpenSearch Service Domain](/5-Create-and-configure-OpenSearch-Service/1-Create-OpenSearch-Service-Domain/_index.md)
* [5.2 Tạo Ingest Pipeline](/5-Create-and-configure-OpenSearch-Service/2-Create-Ingest-Pipeline/_index.md)