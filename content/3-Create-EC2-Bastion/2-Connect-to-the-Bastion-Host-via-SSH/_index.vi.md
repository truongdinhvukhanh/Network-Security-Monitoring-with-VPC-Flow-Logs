---
title : "Kết nối với Bastion Host qua SSH"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 3.2 </b> "
---

{{% notice note %}}
Bước này hướng dẫn cách kết nối an toàn đến host **NSM-Bastion** của bạn bằng SSH. Thiết lập kết nối SSH tới Bastion Host là rất quan trọng vì nó hoạt động như một máy chủ trung gian bảo mật, cho phép bạn truy cập các tài nguyên khác trong private subnets (vốn không thể truy cập trực tiếp từ internet). Điều này đảm bảo rằng hạ tầng nội bộ của bạn vẫn được cô lập và bảo vệ, với tất cả các điểm truy cập được kiểm soát chặt chẽ thông qua Bastion Host.
{{% /notice %}}

1. Mở Command Prompt với quyền Quản trị viên
2. Xóa tất cả các quyền truy cập hiện tại vào tệp:
    ```powershell
    icacls "<your-path-to-keypairfile>" /inheritance:r
    ```
    ```powershell
    icacls "<your-path-to-keypairfile>" /remove:g *S-1-1-0
    ```
    - Thay thế `<your-path-to-keypairfile>` bằng đường dẫn thực tế đến tệp `NSM-Key.pem` của bạn
    - `/inheritance:r`: Vô hiệu hóa việc kế thừa quyền từ thư mục cha
    - `/remove:g *S-1-1-0`: Xóa quyền cho nhóm "Everyone"
    ![image.png](../../images/3/3.2/image.png)
3. Cấp quyền Đọc & Thực thi cho người dùng hiện tại:
    ```powershell
    icacls "<your-path-to-keypairfile>" /grant:r <YourName>:(RX)
    ```
    - Thay thế `<YourName>` bằng tên người dùng Windows thực tế của bạn
    - `(RX)`: Viết tắt của Read & Execute (Đọc & Thực thi)
    - Nếu bạn không chắc chắn về tên người dùng của mình, bạn có thể chạy lệnh `whoami` để tìm. Ví dụ, nếu kết quả là `users/aws`, hãy thay thế `<YourName>` bằng `aws`
    ![image.png](../../images/3/3.2/image%201.png)
4. Kiểm tra các quyền đã gán:
    ```powershell
    icacls "<your-path-to-keypairfile>"
    ```
    ![image.png](../../images/3/3.2/image%202.png)
5. Kết nối với Bastion Host qua SSH:
    ```powershell
    ssh -i "<your-path-to-keypairfile>" ec2-user@<Public-IP>
    ```
    - Thay thế `<your-path-to-keypairfile>` bằng đường dẫn đến tệp `NSM-Key.pem` của bạn.
    - Thay thế `<Public-IP>` bằng địa chỉ IP công cộng của EC2 instance của bạn.
    **Nhắc nhở kết nối lần đầu:**
    Lần đầu tiên bạn kết nối, bạn sẽ được hỏi "Are you sure you want to continue connecting (yes/no/[fingerprint])?". Gõ `yes`
    ![image.png](../../images/3/3.2/image%203.png)
    Bạn đã hoàn thành thành công việc tạo và xác minh Bastion EC2.