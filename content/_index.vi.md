---
title : "Session Management"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
# DynamoDB Triggers và Stream Processing với Lambda

### Tổng thể
Trong dự án này, bạn sẽ tìm hiểu và triển khai một hệ thống xử lý dữ liệu thời gian thực sử dụng DynamoDB Streams và AWS Lambda. Mỗi khi có thay đổi trong bảng DynamoDB (insert, update, delete), sự kiện sẽ được ghi nhận vào stream và kích hoạt hàm Lambda để xử lý ngay lập tức. Hệ thống thực hiện các thao tác biến đổi dữ liệu (transformation), tổng hợp (aggregation), xử lý lỗi (error handling) và ghi nhận kết quả về các dịch vụ như S3, RDS, hoặc gửi đến hệ thống giám sát.

Mục tiêu chính là xây dựng một kiến trúc serverless hoàn toàn, đảm bảo khả năng mở rộng tự động, hiệu suất cao, tối ưu chi phí, và dễ dàng bảo trì. Bạn cũng sẽ triển khai các kỹ thuật như theo dõi hiệu suất (monitoring), thiết kế framework kiểm thử, và quy trình vận hành lỗi nhằm hoàn thiện hệ thống xử lý luồng dữ liệu hiện đại và thực tế.

<!-- ![ConnectPrivate](/images/workshop2aws.png) -->
![Clean](/images/6.clean/sodoaws.png)
### Nội dung

1. [Giới thiệu](1-introduce/)
2. [Yêu cầu chuẩn bị](2-prerequiste/)
3. [Biến đổi Logic](3-Setting-Up-Environment-ec2-s3-docker/)
4. [Xử lý lỗi](4-Error-Handling/)
5. [Dọn dẹp tài nguyên](5-cleanup/)
