---
title : "Chuẩn bị"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

#### Tổng quan về các bước chuẩn bị

Trong phần này, chúng ta sẽ thiết lập hạ tầng AWS nền tảng cần thiết cho workshop của mình. Điều này bao gồm việc thiết lập Virtual Private Cloud (VPC) với các subnets, cấu hình kết nối internet bằng Internet Gateway và Route Tables, định nghĩa bảo mật mạng bằng Security Groups, và tạo các IAM policies và IAM roles cần thiết cho quyền của dịch vụ. Các bước này rất quan trọng để xây dựng một môi trường an toàn, có khả năng mở rộng và chức năng cho các tài nguyên AWS của bạn.

#### Các khái niệm chính:

* **Virtual Private Cloud (VPC):** Một mạng ảo được cách ly logic trong AWS nơi bạn có thể khởi chạy các tài nguyên AWS.
* **Subnets:** Các phân đoạn của dải địa chỉ IP của VPC nơi bạn có thể đặt các nhóm tài nguyên được cách ly, được phân loại là public (có thể truy cập internet) hoặc private (chỉ nội bộ).
* **Internet Gateway (IGW):** Một thành phần của VPC cho phép giao tiếp giữa VPC của bạn và internet.
* **Route Table:** Một tập hợp các quy tắc xác định nơi lưu lượng mạng từ subnet hoặc gateway của bạn được định tuyến.
* **Security Groups:** Các tường lửa ảo cho các Amazon EC2 instances của bạn, kiểm soát lưu lượng vào và ra dựa trên các quy tắc.
* **IAM Policy:** Một tài liệu định nghĩa quyền hạn, chỉ rõ ai có thể truy cập tài nguyên AWS nào và trong điều kiện nào.
* **IAM Role:** Một danh tính AWS với các chính sách quyền hạn xác định những gì danh tính đó có thể và không thể làm trong AWS. Các Role được đảm nhiệm bởi các thực thể đáng tin cậy.

#### Nội dung:

* [2.1 Tạo VPC](/2-Preparation/1-Create-VPC/_index.md)
* [2.2 Tạo Subnets](/2-Preparation/2-Create-Subnets/_index.md)
* [2.3 Tạo Internet Gateway](/2-Preparation/3-Create-Internet-Gateway/_index.md)
* [2.4 Tạo Route Table](/2-Preparation/4-Create-Route-Table/_index.md)
* [2.5 Tạo Security Groups](/2-Preparation/5-Create-Security-Groups/_index.md)
* [2.6 Tạo IAM Policy và IAM Role](/2-Preparation/6-Create-IAM-Policy-and-IAM-Role/_index.md)