---
title : "Tạo Route Table"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 2.4 </b> "
---

{{% notice note %}}
Trong lab này, việc cấu hình một Route Table là rất quan trọng để định tuyến lưu lượng đến và từ các subnets của bạn. Cụ thể, chúng ta sẽ tạo một route table định tuyến tất cả lưu lượng truy cập internet từ **NSM-Public-Subnet** của bạn thông qua **NSM-IGW** mà bạn vừa tạo. Điều này đảm bảo rằng các tài nguyên trong public subnet có thể gửi và nhận dữ liệu từ internet, điều cần thiết cho chức năng dự kiến của chúng.
{{% /notice %}}

#### Hướng dẫn từng bước tạo Route Table
1. Truy cập giao diện Route Table:
    - Điều hướng đến bảng điều khiển **VPC**
    - Chọn **Route Tables** từ bảng điều hướng bên trái
    - Nhấp **Create route table**
    ![image.png](../images/2/2.4/image.png)
2. Cấu hình Route Table của bạn:
    - Nhập **Name**: `NSM-Public-RT`
    - Chọn **VPC**: Chọn **NSM-VPC** từ danh sách thả xuống
    - Nhấp **Create route table**
    ![image.png](../images/2/2.4/image%201.png)
3. Xác minh việc tạo Route Table thành công:
    - Bạn sẽ thấy một thông báo thành công
    - Route Table mới của bạn sẽ xuất hiện trong danh sách
    ![image.png](../images/2/2.4/image%202.png)
4. Sửa đổi các tuyến đường trong Route Table của bạn:
    - Chọn Route Table mới tạo của bạn
    - Nhấp vào danh sách thả xuống **Actions**
    - Chọn **Edit routes**
    ![image.png](../images/2/2.4/image%203.png)
5. Thêm một tuyến đường Internet:
    - Nhấp **Add route**
    - Đối với **Destination**, nhập **`0.0.0.0/0`** (đại diện cho tất cả lưu lượng IPv4)
    - Đối với **Target**, chọn **Internet Gateway** và chọn **NSM-IGW**
    - Nhấp **Save changes**
    ![image.png](../images/2/2.4/image%204.png)
6. Liên kết Route Table với public subnet của bạn:
    - Chọn tab **Subnet associations**
    - Nhấp **Edit subnet associations**
    ![image.png](../images/2/2.4/image%205.png)
7. Chọn các subnets phù hợp:
    - Chọn **NSM-Public-Subnet** bạn đã tạo trước đó
    - Nhấp **Save associations**
    ![image.png](../images/2/2.4/image%206.png)
8. Xác nhận các liên kết subnet của bạn:
    - Xem lại các subnets liên kết trong tab Subnet associations
    - Public subnet hiện đã được cấu hình để định tuyến lưu lượng internet thông qua Internet Gateway
    ![image.png](../images/2/2.4/image%207.png)