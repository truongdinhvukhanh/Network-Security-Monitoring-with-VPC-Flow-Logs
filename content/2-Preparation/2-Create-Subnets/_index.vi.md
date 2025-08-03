---
title : "Tạo Subnets"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

{{% notice note %}}
Trong lab này, việc tạo public và private subnets trong VPC của bạn là rất cần thiết để phân đoạn mạng. Public subnet sẽ chứa các tài nguyên như Bastion Host yêu cầu truy cập internet, trong khi private subnet sẽ lưu trữ an toàn các tài nguyên nội bộ như OpenSearch domain của bạn, đảm bảo chúng không bị lộ trực tiếp ra internet. Thiết lập này giúp tăng cường bảo mật và tổ chức mạng của bạn cho kiến trúc đã lên kế hoạch.
{{% /notice %}}

#### Tạo Public Subnet
1. Truy cập giao diện tạo subnet:
    - Điều hướng đến bảng điều khiển **VPC**
    - Chọn **Subnets** từ bảng điều hướng bên trái
    - Nhấp **Create subnet**
    ![image.png](../images/2/2.2/image.png)
2. Chọn VPC của bạn:
    - Trong giao diện **Create subnet**, chọn **NSM-VPC** từ danh sách thả xuống
    ![image.png](../images/2/2.2/image%201.png)
3. Cấu hình public subnet của bạn:
    - **Subnet name**: Nhập `NSM-Public-Subnet`
    - **Availability Zone**: Chọn `us-east-1a`
    - **IPv4 CIDR block:** Nhập `10.0.1.0/24`
    - Nhấp **Create subnet**
    ![image.png](../images/2/2.2/image%202.png)
4. Xác minh việc tạo subnet thành công:
    - Bạn sẽ thấy một thông báo thành công
    - Subnet mới của bạn sẽ xuất hiện trong danh sách subnet
    ![image.png](../images/2/2.2/image%203.png)
5. Bật tự động gán IP công cộng cho public subnet
    - Chọn **NSM-Public-Subnet** từ danh sách subnet
    - Nhấp **Actions** > **Edit subnet settings**
    ![image.png](../images/2/2.2/image%204.png)
6. Cấu hình cài đặt tự động gán IP:
    - Dưới **Auto-assign IP settings**, chọn **Enable auto-assign public IPv4 address**
    - Nhấp **Save**
    ![image.png](../images/2/2.2/image%205.png)
    ![image.png](../images/2/2.2/image%206.png)
#### Tạo Private Subnet
1. Nhấp **Create subnet**
    ![image.png](../images/2/2.2/image%207.png)
2. Nhập các chi tiết sau:
    - **VPC ID:** Chọn **NSM-VPC** từ danh sách thả xuống
    - **Subnet name:** Nhập `NSM-Private-Subnet`
    - **Availability Zone:** Chọn `us-east-1a`
    - **IPv4 CIDR block:** Nhập `10.0.2.0/24`
3. Nhấp **Create subnet**
    ![image.png](../images/2/2.2/image%208.png)
    ![image.png](../images/2/2.2/image%209.png)