---
title : "Tạo VPC"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---

{{% notice note %}}
Tạo một Amazon Virtual Private Cloud (VPC) là bước nền tảng cho lab này. Nó cung cấp một mạng ảo được cách ly logic mà bạn định nghĩa, đóng vai trò là môi trường an toàn và riêng tư nơi tất cả tài nguyên AWS của dự án (chẳng hạn như subnets, instances và services) sẽ cư trú. Sự cách ly này đảm bảo rằng các tài nguyên của bạn nằm trong tầm kiểm soát và không bị lộ ra internet công cộng trừ khi được cấu hình rõ ràng.
{{% /notice %}}

#### Hướng dẫn từng bước tạo VPC

1. Điều hướng đến [AWS Management Console](https://aws.amazon.com/console/)
    - Trong thanh tìm kiếm, tìm và chọn **VPC**
    ![image.png](../../images/2/2.1/image.png)
2. Bắt đầu tạo VPC:
    - Chọn **Your VPCs** từ bảng điều hướng bên trái
    - Nhấp vào nút **Create VPC** ở góc trên bên phải
    ![image.png](../../images/2/2.1/image%201.png)
3. Cấu hình cài đặt VPC của bạn:
    - Dưới **Resources to create**, chọn **VPC only**
    - Nhập **Name tag**: `NSM-VPC`
    - Đặt **IPv4 CIDR block**: `10.0.0.0/16`
    ![image.png](../../images/2/2.1/image%202.png)
4. Hoàn tất việc tạo VPC:
    - Xem lại cài đặt của bạn
    - Nhấp **Create VPC**
    ![image.png](../../images/2/2.1/image%203.png)
5. Xác minh việc tạo VPC thành công:
    - Bạn sẽ thấy một thông báo thành công
    - VPC mới của bạn sẽ xuất hiện trong danh sách VPC
    ![image.png](../../images/2/2.1/image%204.png)