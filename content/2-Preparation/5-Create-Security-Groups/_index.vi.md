---
title : "Tạo Security Groups"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 2.5 </b> "
---

{{% notice note %}}
Security Groups là nền tảng để định nghĩa kiểm soát truy cập mạng cho các thành phần khác nhau trong lab này. Bằng cách tạo **SG-Bastion**, **SG-Firehose**, và **SG-OpenSearch**, chúng ta thiết lập quyền kiểm soát chi tiết đối với lưu lượng truy cập được phép đến các instances và services của bạn. Điều này đảm bảo rằng chỉ những truy cập được ủy quyền (ví dụ: SSH đến Bastion, Firehose đến OpenSearch) mới được phép, từ đó nâng cao tổng thể bảo mật của giải pháp đã triển khai của bạn.
{{% /notice %}}

#### Security Group cho Bastion
1. Truy cập giao diện Security Group:
    - Điều hướng đến bảng điều khiển **VPC**
    - Chọn **Security Groups** từ bảng điều hướng bên trái
    - Nhấp **Create security group**
    ![image.png](../../images/2/2.5/image.png)
2. Cấu hình Security Group cho Bastion:
    - **Security group name**: Nhập `SG-Bastion`
    - **Description**: Nhập `Security group for Bastion Host access`
    - **VPC**: Chọn **NSM-VPC** từ danh sách thả xuống
    ![image.png](../../images/2/2.5/image%201.png)
3. Định nghĩa các quy tắc Inbound:
    - Nhấp **Add rule**
    - Cấu hình quyền truy cập SSH:
        - **Type**: Chọn **SSH**
        - **Source**: Chọn **My IP** (tự động sử dụng địa chỉ IPv4 công cộng hiện tại của bạn)
    ![image.png](../../images/2/2.5/image%202.png)
4. Xem lại các quy tắc Outbound:
    - Theo mặc định, tất cả lưu lượng outbound đều được cho phép
    - Nhấp **Create security group**
    ![image.png](../../images/2/2.5/image%203.png)
5. Xác minh việc tạo thành công:
    - Bạn sẽ thấy một thông báo thành công
    - Security group mới của bạn sẽ xuất hiện trong danh sách
    ![image.png](../../images/2/2.5/image%204.png)
#### Security Group cho Firehose
1. Bắt đầu tạo một security group khác:
    - Điều hướng trở lại **Security Groups**
    - Nhấp **Create security group**
    ![image.png](../../images/2/2.5/image%205.png)
2. Cấu hình Security Group cho Firehose:
    - **Security group name**: Nhập `SG-Firehose`
    - **Description**: Nhập `Security group for Firehose`
    - **VPC**: Chọn **NSM-VPC** từ danh sách thả xuống
    ![image.png](../../images/2/2.5/image%206.png)
3. Hoàn tất việc tạo security group:
    - Xem lại cài đặt của bạn
    - Nhấp **Create security group**
    ![image.png](../../images/2/2.5/image%207.png)
4. Xác minh việc tạo thành công:
    - Bạn sẽ thấy một thông báo thành công
    - Security group mới của bạn sẽ xuất hiện trong danh sách
    ![image.png](../../images/2/2.5/image%208.png)
#### Security Group cho OpenSearch
1. Bắt đầu tạo một security group khác:
    - Điều hướng trở lại **Security Groups**
    - Nhấp **Create security group**
    ![image.png](../../images/2/2.5/image%209.png)
2. Cấu hình Security Group cho OpenSearch:
    - **Security group name**: Nhập `SG-OpenSearch`
    - **Description**: Nhập `Security group for OpenSearch domain access`
    - **VPC**: Chọn **NSM-VPC** từ danh sách thả xuống
    ![image.png](../../images/2/2.5/image%2010.png)
3. Định nghĩa các quy tắc Inbound:
    - Nhấp **Add rule**
    - Cấu hình quyền truy cập HTTPS cho Bastion:
        - **Type**: Chọn **HTTPS**
        - **Source**: Chọn **Custom**
        - Chọn ID security group của **SG-Bastion** bạn vừa tạo
    ![image.png](../../images/2/2.5/image%2011.png)
    - Nhấp **Add rule** một lần nữa
    - Cấu hình quyền truy cập HTTPS cho Firehose:
        - **Type**: Chọn **HTTPS**
        - **Source**: Chọn **Custom**
        - Chọn ID security group của **SG-Firehose** bạn vừa tạo
    ![image.png](../../images/2/2.5/image%2012.png)
4. Hoàn tất việc tạo security group:
    - Xem lại cài đặt của bạn
    - Nhấp **Create security group**
    ![image.png](../../images/2/2.5/image%2013.png)
5. Xác minh ba security groups:
    - Xác nhận ba security groups xuất hiện trong danh sách của bạn
    - Giờ đây bạn đã có các security groups chuyên dụng cho tài nguyên Bastion, Firehose và OpenSearch
    ![image.png](../../images/2/2.5/image%2014.png)