---
title : "Khởi chạy EC2 Instance làm Bastion Host"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 3.1 </b> "
---

{{% notice note %}}
Trong bước này, bạn sẽ khởi chạy một **EC2 instance** sẽ đóng vai trò là **Bastion Host** của bạn. Host này rất cần thiết để truy cập an toàn các EC2 instance và tài nguyên khác nằm trong private subnets trong VPC của bạn, những tài nguyên không có quyền truy cập internet trực tiếp. Việc thiết lập một Bastion Host giúp tập trung các điểm truy cập, tăng cường bảo mật bằng cách giảm bề mặt tấn công và cung cấp một điểm vào được kiểm soát cho các tác vụ quản trị trong mạng riêng của bạn.
{{% /notice %}}

1. Đăng nhập vào [AWS Management Console](https://aws.amazon.com/console/)
    - Trong thanh tìm kiếm, gõ **EC2**
    - Chọn **EC2** từ danh sách dịch vụ
    ![image.png](../images/3/3.1/image.png)
2. Trong bảng điều khiển EC2:
    - Nhấp vào **Instances** trong ngăn điều hướng
    - Nhấp **Launch instances**
    ![image.png](../images/3/3.1/image%201.png)
3. Tên và Thẻ
    - **Name:** Nhập `NSM-Bastion-Host`
    ![image.png](../images/3/3.1/image%202.png)
4. Chọn Amazon Machine Image (AMI):
    - Dưới **Quick Start**, chọn **Amazon Linux**
    - Chọn **Amazon Linux 2023** từ các tùy chọn có sẵn
    ![image.png](../images/3/3.1/image%203.png)
5. Chọn thông số kỹ thuật instance:
    - Chọn **t2.micro**
    ![image.png](../images/3/3.1/image%204.png)
6. Tạo Key Pair
    - Nhấp **Create new key pair**
    ![image.png](../images/3/3.1/image%205.png)
    - **Key pair name**: `NSM-Key`
    - **Key pair type**: Chọn **RSA**
    - **Private key file format:** Chọn **.pem**
    - Nhấp **Create key pair**
    - **Quan trọng**: Tệp này sẽ chỉ được tải xuống một lần. Hãy lưu trữ nó an toàn
    ![image.png](../images/3/3.1/image%206.png)
7. Cấu hình Cài đặt Mạng
    - Nhấp **Edit** trong phần Network settings
    - **VPC:** Chọn **NSM-VPC** của bạn
    - **Subnet:** Chọn `NSM-Public-Subnet` của bạn
    - **Auto-assign public IP:** Bật
    - **Firewall (security groups):** Chọn existing security group
    - Chọn `SG-Bastion` từ danh sách thả xuống
    ![image.png](../images/3/3.1/image%207.png)
8. **Xem lại và Khởi chạy**
    - Xem lại cài đặt của bạn
    - Nhấp **Launch instance**
    ![image.png](../images/3/3.1/image%208.png)
9. **Chờ Instance khởi tạo**
    - Nhấp **View all instances**
    ![image.png](../images/3/3.1/image%209.png)
    - Đợi cho đến khi **Instance state** hiển thị "Running" và **Status checks** hiển thị "2/2 checks passed"
    - Lưu ý **Public IPv4 address** của instance của bạn
    ![image.png](../images/3/3.1/image%2010.png)