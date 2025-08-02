---
title : "Tạo EC2 Bastion"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

#### Tổng quan về Thiết lập EC2 Bastion Host

Trong phần này, chúng ta sẽ thiết lập và kết nối với một **EC2 Bastion Host**. Một Bastion Host hoạt động như một máy chủ trung gian bảo mật, cung cấp quyền truy cập được kiểm soát vào các tài nguyên mạng riêng của bạn từ một mạng bên ngoài (như internet). Đây là một thành phần quan trọng để quản lý an toàn các instance nằm trong private subnets, đảm bảo rằng việc truy cập SSH trực tiếp vào các máy chủ nội bộ được giảm thiểu, từ đó nâng cao tổng thể bảo mật đám mây của bạn.

#### Các khái niệm chính:

* **EC2 Instance:** Một máy chủ ảo trong Amazon Elastic Compute Cloud (EC2) để chạy các ứng dụng.
* **Bastion Host:** Một máy chủ hoạt động như một cổng bảo mật đến một mạng riêng, cho phép truy cập có kiểm soát vào các tài nguyên nội bộ.
* **Key Pair:** Một bộ thông tin xác thực bảo mật (khóa công khai và khóa riêng tư) được sử dụng để chứng minh danh tính của bạn khi kết nối với các EC2 instance.
* **SSH (Secure Shell):** Một giao thức mạng mã hóa để giao tiếp dữ liệu an toàn, đăng nhập dòng lệnh từ xa và các dịch vụ mạng an toàn khác.

#### Mục lục:

* [3.1 Khởi chạy EC2 Instance làm Bastion Host](/3-Create-EC2-Bastion/1-Launch-an-EC2-Instance-as-a-Bastion-Host/_index.md)
* [3.2 Kết nối với Bastion Host qua SSH](/3-Create-EC2-Bastion/2-Connect-to-the-Bastion-Host-via-SSH/_index.md)