---
title : "Tạo Internet Gateway"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---

{{% notice note %}}
Một Internet Gateway (IGW) rất quan trọng đối với lab này vì nó cho phép public subnet trong **NSM-VPC** của bạn giao tiếp với internet. Đây là điều kiện tiên quyết để các tài nguyên như Bastion Host trong public subnet có thể truy cập được để quản lý và để bất kỳ dịch vụ công cộng nào hoạt động như dự kiến.
{{% /notice %}}

#### Hướng dẫn từng bước tạo Internet Gateway

1. Truy cập giao diện Internet Gateway:
    - Điều hướng đến bảng điều khiển **VPC**
    - Chọn **Internet Gateways** từ bảng điều hướng bên trái
    - Nhấp **Create internet gateway**
    ![image.png](/images/2/2.3/image.png)
2. Cấu hình Internet Gateway của bạn:
    - Nhập **Name tag**: `NSM-IGW`
    - Nhấp **Create internet gateway**
    ![image.png](/images/2/2.3/image%201.png)
3. Xác minh việc tạo Internet Gateway thành công:
    - Bạn sẽ thấy một thông báo thành công
    - Internet Gateway mới của bạn sẽ xuất hiện trong danh sách
    ![image.png](/images/2/2.3/image%202.png)
4. Gắn Internet Gateway vào VPC của bạn:
    - Chọn Internet Gateway mới tạo của bạn
    - Nhấp vào danh sách thả xuống **Actions**
    - Chọn **Attach to VPC**
    - Chọn **NSM-VPC** từ danh sách thả xuống
    - Nhấp **Attach internet gateway**
    ![image.png](/images/2/2.3/image%203.png)
5. Xác nhận gắn thành công:
    - **State** của Internet Gateway của bạn sẽ chuyển thành **Attached**
    - Điều này cho thấy Internet Gateway hiện đang hoạt động với VPC của bạn
    ![image.png](/images/2/2.3/image%204.png)