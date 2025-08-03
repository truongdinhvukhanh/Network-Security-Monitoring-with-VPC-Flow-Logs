---
title : "Truy vấn nhật ký với Athena"
date : "`r Sys.Date()`"
weight : 9
chapter : false
pre : " <b> 9. </b> "
---

{{% notice note %}}
Trong phần này, bạn sẽ sử dụng **Amazon Athena** để truy vấn các **VPC Flow Logs** được lưu trữ trong **S3 bucket** của bạn. Athena là một dịch vụ truy vấn tương tác giúp dễ dàng phân tích dữ liệu trực tiếp trong Amazon S3 bằng cách sử dụng SQL tiêu chuẩn. Bước này trình bày cách thực hiện phân tích đặc biệt hiệu quả trên dữ liệu nhật ký luồng thô của bạn, cung cấp một phương pháp thay thế hoặc bổ sung cho OpenSearch để điều tra chuyên sâu và báo cáo tùy chỉnh về lưu lượng mạng của bạn.
{{% /notice %}}

#### Truy vấn VPC Flow Logs bằng Amazon Athena
1. Cấu hình Vị trí Kết quả Truy vấn Athena
    - Điều hướng đến [Athena Console](https://console.aws.amazon.com/athena/)
    - **Thiết lập lần đầu**: Nếu đây là lần đầu tiên của bạn, hãy nhấp vào **"Explore the query editor"**
    - Nhấp vào tab **Settings** ở trên cùng
    - Nhấp **Manage**
    ![image.png](../images/9/image.png)
    - Nhập vị trí S3: `s3://nsm-flow-logs-YYYYMMDD/athena-results/`

    (thay thế **nsm-flow-logs-YYYYMMDD** bằng tên bucket thực tế của bạn)
    - Nhấp **Save**
    ![image.png](../images/9/image%201.png)
2. Tạo Cơ sở dữ liệu
    - Trong **Query Editor** của Athena, chạy lệnh này:
    ```sql
    CREATE DATABASE IF NOT EXISTS vpc_flow_logs_db;
    ```
    ![image.png](../images/9/image%202.png)
    ![image.png](../images/9/image%203.png)

3. Tạo Bảng VPC Flow Logs
    - Chạy lệnh này
    ```sql
    CREATE EXTERNAL TABLE vpc_flow_logs_db.vpc_flow_logs (
      version int,
      account_id string,
      interface_id string,
      srcaddr string,
      dstaddr string,
      srcport int,
      dstport int,
      protocol int,
      packets bigint,
      bytes bigint,
      windowstart bigint,
      windowend bigint,
      action string,
      flowlogstatus string
    )
    ROW FORMAT DELIMITED
    FIELDS TERMINATED BY ' '
    LOCATION 's3://nsm-flow-logs-20250727/flow-logs/'
    TBLPROPERTIES (
      'skip.header.line.count'='0'
    );
    ```
    ![image.png](../images/9/image%204.png)
4. Xác minh việc tạo bảng
    ```sql
    SHOW TABLES;
    ```
    ![image.png](../images/9/image%205.png)
5. Kiểm tra với các truy vấn mẫu
    - Khám phá dữ liệu cơ bản
        ```sql
        -- Xem 10 bản ghi đầu tiên để hiểu cấu trúc dữ liệu của bạn
        SELECT *
        FROM vpc_flow_logs
        LIMIT 10;
        ```
    ![image.png](../images/9/image%206.png)
    - Đếm tổng số bản ghi
        ```sql
        -- Đếm tổng số bản ghi nhật ký luồng
        SELECT COUNT(*) as total_records
        FROM vpc_flow_logs;
        ```
    ![image.png](../images/9/image%207.png)
    - Kiểm tra chất lượng dữ liệu
        ```sql
        -- Kiểm tra các hành động khác nhau trong nhật ký của bạn
        SELECT
            action,
            COUNT(*) as count
        FROM vpc_flow_logs
        GROUP BY action;
        ```
    ![image.png](../images/9/image%208.png)
6. Các truy vấn ví dụ để phân tích
    - Phân tích lưu lượng SSH (Cổng 22)
        ```sql
        -- Tìm các lần thử kết nối SSH
        SELECT
            srcaddr,
            dstaddr,
            action,
            packets,
            bytes,
            from_unixtime(windowstart) as start_time,
            from_unixtime(windowend) as end_time
        FROM vpc_flow_logs
        WHERE dstport = 22
        ORDER BY windowstart DESC
        LIMIT 20;
        ```
    ![image.png](../images/9/image%209.png)
    - Phân tích các kết nối bị từ chối
        ```sql
        -- Phân tích các kết nối bị từ chối
        SELECT
            srcaddr,
            dstaddr,
            dstport,
            COUNT(*) as rejected_count
        FROM vpc_flow_logs
        WHERE action = 'REJECT'
        GROUP BY srcaddr, dstaddr, dstport
        ORDER BY rejected_count DESC
        LIMIT 15;
        ```
    ![image.png](../images/9/image%2010.png)
7. Xem kết quả truy vấn trong S3
    - Điều hướng đến [https://s3.console.aws.amazon.com/](https://s3.console.aws.amazon.com/)
    - Điều hướng đến bucket: `nsm-flow-logs-YYYY-MM-DD`
    ![image.png](../images/9/image%2011.png)
    - Mở thư mục: `athena-results/`
    ![image.png](../images/9/image%2012.png)
    ![image.png](../images/9/image%2013.png)