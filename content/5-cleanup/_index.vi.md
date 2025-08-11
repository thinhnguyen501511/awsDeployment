---
title : "Dọn dẹp tài nguyên"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : "<b>5. </b>"
---


Sau khi hoàn tất thử nghiệm hoặc triển khai, việc dọn dẹp tài nguyên AWS là rất quan trọng để:
+ Tránh phát sinh chi phí không cần thiết.
+ Giảm rủi ro bảo mật từ các dịch vụ hoặc quyền không còn sử dụng.
+ Giữ cho tài khoản AWS gọn gàng và dễ quản lý.

**Dưới đây là hướng dẫn chi tiết các bước xóa từng loại tài nguyên đã sử dụng trong dự án.**


#### Xoá Lambda Function.

1. Truy cập vào [Lambda](https://ap-southeast-1.console.aws.amazon.com/lambda/home?region=ap-southeast-1#/functions)
   + Chọn các **Function** cần xoá.
   + Chọn **Action** --> Chọn **Delete**
   + Nhập **confirm** --> Chọn **Delete**
   




### Xóa DynamoDB Table và Stream.

1. Truy cập vào [DynamoDB](https://ap-southeast-1.console.aws.amazon.com/dynamodbv2/home?region=ap-southeast-1#tables)
   + Chọn các Tables đã tạo
   + Chọn **Delete**
   + Nhập **confirm** --> **Delete**




#### Xóa SQS/SNS (DLQ)
**Nếu dự án có sử dụng Dead Letter Queue (DLQ):**
1. Mở **SQS** (nếu DLQ là SQS queue):
   + Chọn queue cần xóa.
   + Chọn **Delete** và xác nhận.
2. Mở **SNS** (nếu DLQ là SNS topic):
   + Chọn topic cần xóa.
   + Chọn **Delete** và xác nhận.



#### Xóa Log Group trong CloudWatch
1. Truy cập vào [CloudWatch](https://ap-southeast-1.console.aws.amazon.com/cloudwatch/home?region=ap-southeast-1#home:)
2. Chọn **Log groups**.
3. Tìm log group theo tên hàm Lambda, ví dụ: `/aws/lambda/DynamoStreamProcessor`.
4. Chọn log group → **Actions → Delete log group**.
5. Chọn **Delete** để xác nhận xóa.




#### Xóa IAM Role
1. Truy cập [Roles](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles)
2. Chọn role đã cấp quyền cho Lambda hoặc các dịch vụ khác trong dự án.
3. Chọn **Delete**
4. Nhập **delete** --> Chọn **Delete** để xoá.

