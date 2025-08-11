---
title : "Tạo DynamoDB Table và Bật DynamoDB Stream"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre: " <b> 2.2. </b> "
---

### Tạo DynamoDB


Để xử lý dữ liệu theo thời gian thực(real-time) trong hệ thống Serverless, chúng ta cần một cơ chế để lắng nghe các thay đổi xảy ra trong cơ sở dữ liệu. DynamoDB Stream chính là công cụ hỗ trợ cho mục tiêu đó. Ở bước này, chúng ta sẽ tạo một bảng DynamoDB để lưu trữ dữ liệu và bật tính năng Stream, nhằm cho phép các dịch vụ như AWS Lambda tự động kích hoạt mỗi khi có thay đổi (thêm, sửa, xóa) trong bảng.

Việc bật DynamoDB Stream sẽ giúp bạn xây dựng một luồng xử lý dữ liệu realtime mạnh mẽ, chẳng hạn như ghi log, đồng bộ dữ liệu, tính toán thống kê hoặc chuyển đổi dữ liệu sang hệ thống khác. Đây là nền tảng quan trọng trong kiến trúc hướng sự kiện (event-driven architecture).

1. Đi tới [DynamoDB ](https://us-east-1.console.aws.amazon.com/dynamodbv2/home?region=us-east-1#create-table)

   + Nhấp vào **DynamoDB**.
   + Nhấp vào **Tables**, sau đó Nhấp vào **Create table** 

![role](/images/2.prerequisite/Dynamo1.png)


2. Trong tạo bảng:
    + Đặt tên bảng **OrdersTable**
    + Đặt tên Partition key : **OrderID**
    + Chọn **Customize settings**    

![role1](/images/2.prerequisite/Dynamo2.png)


  + Sau đó chọn **Create table**
![role1](/images/2.prerequisite/Dynamo3.png)

3. Bật DynamoDB Stream
    + Nhấp vào Table vừa tạo
    + Chọn **Exports and Streams**
![role1](/images/2.prerequisite/Dynamo4.png)

  + Tại DynamoDB stream details, Chọn **Turn on**
![role1](/images/2.prerequisite/Dynamo5.png)

  + Chọn **New and old images** 
  + Nhấp vào **Turn on stream**
![role1](/images/2.prerequisite/Dynamo6.png)


