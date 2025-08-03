---
title : "Tạo S3 Bucket"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

{{% notice note %}}
Trong phần này, bạn sẽ tạo một Amazon S3 (Simple Storage Service) bucket. S3 bucket này là một thành phần quan trọng trong kiến trúc dự án của chúng ta vì nó sẽ đóng vai trò là đích lưu trữ chính cho dữ liệu được xử lý bởi Kinesis Firehose. S3 cung cấp khả năng lưu trữ đối tượng có độ bền cao, khả năng mở rộng và bảo mật, khiến nó trở thành lựa chọn lý tưởng để lưu trữ dữ liệu thô hoặc đã xử lý một cách đáng tin cậy trước khi phân tích thêm hoặc lưu trữ dài hạn.
{{% /notice %}}

#### Tạo S3 Bucket
1. Đăng nhập vào AWS Management Console
    - Trong thanh tìm kiếm, gõ **S3**
    - Chọn **S3** từ danh sách dịch vụ
    ![image.png](../../images/4/image.png)
2. Trong giao diện **S3**, chọn **Create bucket**
    ![image.png](../../images/4/image%201.png)
3. Trong giao diện **Create bucket**
    - **Bucket type:** Chọn **General purpose**
    - **Bucket name**: Gõ `nsm-flow-logs-YYYYMMDD` (thay thế YYYYMMDD bằng ngày hôm nay để đảm bảo tính duy nhất)
    ![image.png](../../images/4/image%202.png)
4. Nhấp **Create bucket**
    ![image.png](../../images/4/image%203.png)
    ![image.png](../../images/4/image%204.png)
#### Tạo Cấu trúc Thư mục để Lưu trữ Dữ liệu có Tổ chức
1. Chọn bucket mới tạo của bạn
    ![image.png](../../images/4/image%205.png)
2. Cuộn xuống và nhấp **Create folder**
    ![image.png](../../images/4/image%206.png)
3. Tạo các thư mục sau:
    - `flow-logs` (cho dữ liệu VPC Flow Logs)
    ![image.png](../../images/4/image%207.png)
    - `athena-results` (để lưu trữ kết quả truy vấn Athena)
    ![image.png](../../images/4/image%208.png)
4. Xác minh hai thư mục đã được tạo thành công
    ![image.png](../../images/4/image%209.png)
#### Cấu hình Bucket Policy cho Firehose Access
1. Chuyển đến tab **Permissions**
2. Cuộn xuống **Bucket policy** và nhấp **Edit**
    ![image.png](../../images/4/image%2010.png)
3. Sao chép và dán policy sau, thay thế các phần giữ chỗ:
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "AllowFirehoseDelivery",
                "Effect": "Allow",
                "Principal": {
                    "Service": "firehose.amazonaws.com"
                },
                "Action": [
                    "s3:AbortMultipartUpload",
                    "s3:GetBucketLocation",
                    "s3:GetObject",
                    "s3:ListBucket",
                    "s3:ListBucketMultipartUploads",
                    "s3:PutObject"
                ],
                "Resource": [
                    "arn:aws:s3:::nsm-flow-logs-YYYYMMDD",
                    "arn:aws:s3:::nsm-flow-logs-YYYYMMDD/*"
                ],
                "Condition": {
                    "StringEquals": {
                        "aws:SourceAccount": "YOUR-ACCOUNT-ID"
                    },
                    "ArnLike": {
                        "aws:SourceArn": "arn:aws:firehose:us-east-1:YOUR-ACCOUNT-ID:deliverystream/*"
                    }
                }
            },
            {
                "Sid": "AllowAthenaAccess",
                "Effect": "Allow",
                "Principal": {
                    "Service": "athena.amazonaws.com"
                },
                "Action": [
                    "s3:GetBucketLocation",
                    "s3:GetObject",
                    "s3:ListBucket",
                    "s3:ListBucketMultipartUploads",
                    "s3:ListMultipartUploadParts",
                    "s3:AbortMultipartUpload",
                    "s3:PutObject"
                ],
                "Resource": [
                    "arn:aws:s3:::nsm-flow-logs-YYYYMMDD",
                    "arn:aws:s3:::nsm-flow-logs-YYYYMMDD/*"
                ]
            }
        ]
    }
    ```
    Thay thế:
    - `nsm-flow-logs-YYYYMMDD` bằng tên bucket thực tế của bạn (4 vị trí)
    - `YOUR-ACCOUNT-ID` bằng ID tài khoản AWS của bạn (tìm thấy ở góc trên bên phải của AWS console)
    - Đảm bảo khu vực phù hợp với thiết lập của bạn (us-east-1 trong ví dụ này)
    ![image.png](../../images/4/image%2011.png)
4. Nhấp **Save changes**
    ![image.png](../../images/4/image%2012.png)