---
title : "Tạo Dashboard"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 8.2 </b> "
---

{{% notice note %}}
Trong bước này, bạn sẽ tạo một bảng điều khiển trong OpenSearch Dashboards để trực quan hóa dữ liệu VPC Flow Logs của mình. Xây dựng một bảng điều khiển giúp bạn dễ dàng giám sát và phân tích các mẫu lưu lượng mạng, xác định các bất thường và có được những hiểu biết sâu sắc hơn về hoạt động mạng của VPC thông qua các biểu đồ và số liệu thống kê trực quan.
{{% /notice %}}

#### Tạo Trực quan hóa và Dashboard
1. **Tạo Mẫu chỉ mục mới**
    - Trong thanh bên trái, nhấp vào **Dashboards Management**
    ![image.png](image.png)
    - Nhấp vào **Index patterns**
    - Nhấp **Create index pattern**
    ![image.png](image%201.png)
    - **Index pattern name:** Nhập `vpc-flow-logs*`
    - Nhấp **Next step**
    ![image.png](image%202.png)
    - **Time field:** Chọn **start**
    - Nhấp **Create index pattern**
    ![image.png](image%203.png)
    ![image.png](image%204.png)
2. **Tạo Biểu đồ tròn cho Lưu lượng truy cập theo IP nguồn**
    - Trong thanh bên trái, nhấp vào **Visualize**
    ![image.png](image%205.png)
    - Nhấp **Create visualization**
    ![image.png](image%206.png)
    - Chọn **Pie** làm loại trực quan hóa
    ![image.png](image%207.png)
    - Chọn mẫu chỉ mục của bạn
    ![image.png](image%208.png)
    - Dưới **Buckets**, nhấp **Add →** **Split slices**
    ![image.png](image%209.png)
    - **Aggregation:** Chọn **Terms**
    - **Field:** Chọn **srcaddr** (địa chỉ IP nguồn)
    - **Size:** 10
    - Nhấp **Update** để xem trực quan hóa
    ![image.png](image%2010.png)
    - Nhấp **Save** và đặt tên là `Top Source IPs`
    ![image.png](image%2011.png)
    ![image.png](image%2012.png)
3. **Tạo Biểu đồ cột cho Lưu lượng truy cập theo Cổng đích**
    - Quay lại **Visualizations List**
    ![image.png](image%2013.png)
    - Nhấp **Create visualization**
    ![image.png](image%2014.png)
    - Chọn **Vertical bar** làm loại trực quan hóa
    ![image.png](image%2015.png)
    - Chọn mẫu chỉ mục của bạn
    ![image.png](image%2016.png)
    - Dưới **Buckets**, nhấp **Add** → **X-axis**
    ![image.png](image%2017.png)
    - **Aggregation:** Chọn **Terms**
    - **Field:** Chọn **dstport** (cổng đích)
    - **Size:** 10 (top 10 cổng đích)
    - Nhấp **Update** để xem trực quan hóa
    ![image.png](image%2018.png)
    - Nhấp **Save** và đặt tên là `Top Destination Ports`
    ![image.png](image%2019.png)
    ![image.png](image%2020.png)
4. **Tạo Biểu đồ đường cho Lưu lượng truy cập theo thời gian**
    - Quay lại **Visualizations List**
    ![image.png](image%2021.png)
    - Nhấp **Create visualization**
    ![image.png](image%2022.png)
    - Chọn **Line** làm loại trực quan hóa
    ![image.png](image%2023.png)
    - Chọn mẫu chỉ mục của bạn
    ![image.png](image%2024.png)
    - Dưới **Buckets**, nhấp **Add → X-axis**
    ![image.png](image%2025.png)
    - **Aggregation:** Chọn **Date Histogram**
    - **Field:** Chọn **start**
    - **Interval:** Chọn **Auto**
    - Nhấp **Update** để xem trực quan hóa
    ![image.png](image%2026.png)
    - Nhấp **Save** và đặt tên là `Traffic Over Time`
    ![image.png](image%2027.png)
    ![image.png](image%2028.png)
5. **Tạo Dashboard mới**
    - Trong thanh bên trái, nhấp vào **Dashboard**
    ![image.png](image%2029.png)
    - Nhấp **Create new dashboard**
    ![image.png](image%2030.png)
    - Nhấp **Add** ở góc trên bên phải
    ![image.png](image%2031.png)
    - Chọn tất cả các trực quan hóa bạn đã tạo:
        - **Top Source IPs**
        - **Top Destination Ports**
        - **Traffic Over Time**
    ![image.png](image%2032.png)
    - Sắp xếp các trực quan hóa bằng cách kéo và thay đổi kích thước chúng
- Nhấp **Save** ở góc trên bên phải
    ![image.png](image%2033.png)
- Đặt tên là `VPC Flow Logs Dashboard`
    ![image.png](image%2034.png)