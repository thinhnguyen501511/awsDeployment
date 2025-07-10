---
title : "Chuẩn Bị"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2. </b> "
---
Để triển khai hệ thống xử lý dữ liệu thời gian thực sử dụng DynamoDB Triggers và AWS Lambda, bạn cần thực hiện một số bước chuẩn bị quan trọng nhằm đảm bảo quyền truy cập và môi trường triển khai phù hợp trên AWS. Trong phần chuẩn bị này, chúng ta sẽ tiến hành tạo IAM Role để cấp quyền cho Lambda có thể truy cập được vào các dịch vụ cần thiết như DynamoDB, CloudWatch Logs, cũng như các dịch vụ khác phục vụ mục đích xử lý, lưu trữ và giám sát dữ liệu. Sau khi cấu hình IAM xong, chúng ta sẽ tiếp tục tạo bảng DynamoDB và xây dựng hệ thống streaming trigger bằng Lambda.

### Nội Dung
  - [Tạo IAM Role](2.1-create-iam-role/)
  - [Tạo DynamoDB Table và bật DynamoDB Stream](2.2-create-dynamo/)
  - [Tạo Lambda và gắn với DynamoDB Stream](2.3-create-lambda/)

