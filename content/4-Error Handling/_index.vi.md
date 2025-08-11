---
title : "Xử lý lỗi"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---

Trong các hệ thống xử lý dữ liệu thời gian thực, lỗi là điều khó tránh khỏi. Chúng có thể xuất hiện do dữ liệu đầu vào không hợp lệ, sự cố mạng, thiếu quyền truy cập, hoặc những tình huống bất ngờ trong logic xử lý. Nếu không được xử lý đúng cách, các lỗi này có thể làm gián đoạn quy trình, gây mất dữ liệu hoặc tạo ra kết quả không nhất quán.

Trong đề tài này, việc xử lý lỗi đặc biệt quan trọng vì hàm Lambda làm việc trực tiếp với dữ liệu từ DynamoDB Stream. Chỉ một bản ghi lỗi không được xử lý đúng cách cũng có thể khiến hệ thống lặp lại xử lý hoặc chặn các sự kiện tiếp theo.

Để đảm bảo hệ thống ổn định và đáng tin cậy, AWS cung cấp nhiều cơ chế xử lý lỗi như:

+ Ghi log với CloudWatch – Lưu lại chi tiết lỗi để phân tích và khắc phục.

+ Cơ chế retry và backoff – Tự động thử xử lý lại sự kiện lỗi với khoảng trễ tăng dần.

+ Dead Letter Queue (DLQ) – Lưu trữ các sự kiện lỗi nhiều lần để xử lý thủ công sau này.

+ Xử lý ngoại lệ tùy chỉnh – Kiểm tra, lọc, và chuyển đổi dữ liệu nhằm tránh lỗi không cần thiết.

Nhờ áp dụng các phương pháp trên, hệ thống có thể phục hồi sau lỗi, duy trì tính nhất quán dữ liệu và giảm chi phí vận hành.

### Nội dung:

 - [Xử lý ngoại lệ trong Lambda](4.1-exception-handling-in-lambda/) 
 - [Ghi Log lỗi với CloudWatch](4.2-log-errors-with-cloudwatch/)
 - [Sử dụng Dead Letter Queue (DLQ) để lưu lỗi](4.3-dead-letter-queue/)
 - [Tự động cảnh báo khi có lỗi bằng CloudWatch](4.4-error-using-cloudwatch-alarm/)