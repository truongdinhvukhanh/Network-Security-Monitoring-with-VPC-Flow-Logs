---
title : "Tạo VPC Flow Log"
date : "`r Sys.Date()`"
weight : 7
chapter : false
pre : " <b> 7. </b> "
---

{{% notice note %}}
Trong phần này, bạn sẽ cấu hình **VPC Flow Logs** để thu thập thông tin chi tiết về lưu lượng IP đến và đi từ các giao diện mạng trong Virtual Private Cloud (VPC) của bạn. Đây là một bước quan trọng để giám sát mạng, phân tích bảo mật và khắc phục sự cố trong môi trường AWS của bạn. VPC Flow Logs sẽ được cấu hình để gửi tất cả dữ liệu lưu lượng truy cập trực tiếp đến **Kinesis Data Firehose stream** mà bạn đã thiết lập trước đó, đảm bảo việc đưa dữ liệu vào **OpenSearch Service domain** của bạn theo thời gian thực để phân tích và trực quan hóa ngay lập tức.
{{% /notice %}}

#### Tạo VPC Flow Log để Giám sát Mạng
1. Điều hướng đến [AWS Management Console](https://aws.amazon.com/console/)
    - Trong thanh tìm kiếm, tìm và chọn **VPC**
    ![image.png](/images/7/image.png)
2. Tạo flow log
    - Chọn **NSM-VPC** của bạn
    - Chọn tab **Flow logs**
    - Nhấp **Create flow log**
    ![image.png](/images/7/image%201.png)
3. Cấu hình flow log:
    - **Filter**: All (thu thập tất cả lưu lượng truy cập)
    - **Maximum aggregation interval:** 1 minute
    - **Destination**: Send to Amazon Data Firehose in the same account
    - **Firehose delivery stream:** Chọn **NSM-FlowLogs-Firehose** từ danh sách thả xuống
    - **Log format:** AWS default format
    ![image.png](/images/7/image%202.png)
4. Nhấp **Create flow log**
    ![image.png](/images/7/image%203.png)