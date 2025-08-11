---
title : "Tạo Lambda và gắn với DynamoDB Stream"
ngày : "`r Sys.Date()`"
trọng lượng : 1
chương : false
pre: " <b> 2.3. </b> "
---

Sau khi đã tạo bảng DynamoDB và bật chức năng Stream, bước tiếp theo là xây dựng hàm Lambda để xử lý các sự kiện được ghi nhận từ Stream đó. AWS Lambda cho phép bạn viết mã thực thi phản ứng ngay khi dữ liệu trong DynamoDB thay đổi — chẳng hạn như khi có một bản ghi mới được thêm vào, bị cập nhật, hoặc bị xóa.

Trong bước này, chúng ta sẽ tạo một hàm Lambda sử dụng ngôn ngữ lập trình phù hợp (ví dụ: Python hoặc Node.js), sau đó cấu hình để hàm này được tự động kích hoạt bởi sự kiện từ DynamoDB Stream. Việc này giúp hệ thống có thể xử lý dữ liệu thời gian thực mà không cần quản lý máy chủ, đồng thời dễ dàng mở rộng khi lưu lượng tăng cao.

+ Lợi ích:
   + Xử lý thời gian thực: dữ liệu được cập nhật hoặc thêm mới vào DynamoDB sẽ được xử lý ngay lập tức qua Lambda.

   + Không cần quản lý hạ tầng: Lambda là dịch vụ serverless nên bạn không cần vận hành máy chủ nào.

   + Tích hợp mượt mà: việc kết nối DynamoDB và Lambda qua Stream được hỗ trợ trực tiếp bởi AWS với thao tác đơn giản.

Sau khi tạo xong, bạn có thể viết logic xử lý như: gửi thông báo, ghi log, đồng bộ với dịch vụ khác, hoặc thực hiện các nghiệp vụ đặc thù.

#### Tạo Lambda Function

1. Đi tới [Tạo Lambda Function](https://ap-southeast-1.console.aws.amazon.com/lambda/home?region=ap-southeast-1#/begin)
   + Nhấp vào **Lambda**.
   + Nhấp vào **Create a function**.

![Lambda](/images/2.prerequisite/Lambda1.png)

![Lambda](/images/2.prerequisite/Lambda2.png)

+ Chọn :
   + Chọn **Author from scratch**
   + Function name: **DynamoStreamProcessor**
   + Runtime: **Node.js 22.x**
   + Chọn **x86_64**
   + Chọn **Use an existing role** > Chọn đúng **LambdaDynamoDBStreamRole** đã tạo trước đó

![Lambda](/images/2.prerequisite/Lambda3.png)

#### Gắn DynamoDB Stream Trigger vào Lambda function
Sau khi đã tạo xong hàm Lambda và bật DynamoDB Streams cho bảng dữ liệu, bước tiếp theo là cấu hình để Lambda tự động được kích hoạt (trigger) mỗi khi bảng DynamoDB có thay đổi dữ liệu (thêm, sửa, xóa).
+ Nối bảng DynamoDB đã bật Stream với Lambda để xử lý real-time data mỗi khi có thay đổi trên bảng.

1. Mở Lambda Function vừa tạo:
   + Vào **Lambda**.
   + Chọn function vừa tạo tên: **DynamoStreamProcessor**.
![Lambda](/images/2.prerequisite/Lambda4.png)

   + Chọn **Add trigger**
![Lambda](/images/2.prerequisite/Lambda5.png)

   + Chọn dịch vụ: **DynamoDB**
![Lambda](/images/2.prerequisite/Lambda6.png)

   + Chọn:

      + Table: OrdersTable (hoặc tên bảng bạn đã tạo)

      + Batch size: Giữ mặc định 100

      + Starting position: Chọn LATEST (chỉ nhận dữ liệu mới)
   + Sau đó chọn Add
   ![Lambda](/images/2.prerequisite/Lambda7.png)

   + Sau khi hoàn thành:
   ![Lambda](/images/2.prerequisite/Lambda8.png)
   
