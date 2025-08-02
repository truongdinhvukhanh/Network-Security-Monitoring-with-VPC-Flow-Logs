---
title : "Tạo OpenSearch Service Domain"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.1 </b> "
---

{{% notice note %}}
Trong bước này, bạn sẽ tạo **Amazon OpenSearch Service domain** của mình. Domain này sẽ hoạt động như nền tảng phân tích và tìm kiếm nhật ký tập trung cho dữ liệu VPC Flow Logs được thu thập trong lab này. Bạn sẽ cấu hình loại instance, bộ nhớ và quan trọng nhất là tích hợp nó vào private subnet của **NSM-VPC**, đảm bảo quyền truy cập an toàn chỉ từ bên trong mạng đã xác định của bạn, từ đó tăng cường cách ly và bảo mật dữ liệu.
{{% /notice %}}

1. Đăng nhập vào [AWS Management Console](https://aws.amazon.com/console/)
    - Trong thanh tìm kiếm, gõ `Amazon OpenSearch Service`
    - Chọn **Amazon OpenSearch Service** từ danh sách dịch vụ
    ![image.png](/images/5/5.1/image.png)
- Nhấp **Create domain** để bắt đầu
    ![image.png](/images/5/5.1/image%201.png)
1. Cấu hình Domain
    - **Domain name:** Nhập `nsm-opensearch`
    - **Domain creation method:** Chọn **Standard create**
    - **Templates:** Chọn **Dev/test** (cho môi trường lab)
    ![image.png](/images/5/5.1/image%202.png)
    - **Deployment option(s):** Chọn **Domain without standby** (đủ cho mục đích lab)
    - **Availability Zone(s):** Chọn **1-AZ**
    - **Version:** Chọn phiên bản OpenSearch mới nhất có sẵn (ví dụ: OpenSearch 2.19)
    ![image.png](/images/5/5.1/image%203.png)
2. Số lượng data nodes
    - **Instance family:** Chọn **General purpose** từ danh sách thả xuống
    - **Instance type:** Chọn **t3.small.search** (đủ cho mục đích lab)
    - **Number of data nodes:** Đặt thành 1 (cho môi trường lab)
    ![image.png](/images/5/5.1/image%204.png)
    - **Storage type:** Chọn **EBS**
    - **Volume type:** General Purpose (SSD) - gp3
    - **Storage size per node:** 10 GiB
    ![image.png](/images/5/5.1/image%205.png)
3. Cấu hình Mạng
    - **Network:** Chọn **VPC access**
    - **IP address type:** Chọn **IPv4 only**
    - **VPC:** Chọn **NSM-VPC** của bạn từ danh sách thả xuống
    - **Subnets:** Chọn **NSM-Private-Subnet**
    - **Security groups:** Chọn **SG-OpenSearch**
    ![image.png](/images/5/5.1/image%206.png)
4. **Kiểm soát truy cập chi tiết**
    - Bỏ chọn **Enable fine-grained access control**
    ![image.png](/images/5/5.1/image%207.png)
5. **Chính sách truy cập:**
    - Chọn **Configure domain level access policy**
    - Action: Chọn **Allow**
    ![image.png](/images/5/5.1/image%208.png)
6. Xem lại và Tạo
    - Xem lại tất cả các cài đặt để đảm bảo chúng khớp với yêu cầu của bạn
    - Nhấp **Create** để bắt đầu tạo domain
    ![image.png](/images/5/5.1/image%209.png)
    - Chờ cho trạng thái domain thay đổi thành **Active** (quá trình này có thể mất 15-20 phút)
    ![image.png](/images/5/5.1/image%2010.png)
    - Sao chép **OpenSearch Dashboards URL** (không bao gồm `https://` và `/_dashboards`)
    ![image.png](/images/5/5.1/image%2011.png)
    ![image.png](/images/5/5.1/image%2012.png)