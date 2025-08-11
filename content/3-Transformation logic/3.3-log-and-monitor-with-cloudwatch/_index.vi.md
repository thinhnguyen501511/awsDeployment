---
title : "Ghi log và giám sát xử lý với CloudWatch"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3.3. </b> "
---

Trong quá trình vận hành hệ thống, việc ghi log đóng vai trò quan trọng để theo dõi, phân tích và xử lý sự cố. AWS cung cấp dịch vụ Amazon CloudWatch cho phép thu thập, lưu trữ và giám sát log từ các dịch vụ khác như AWS Lambda, DynamoDB, v.v.

Khi Lambda thực hiện xử lý dữ liệu từ DynamoDB Stream, toàn bộ thông tin được lập trình để ghi log lại thông qua các lệnh console.log() (hoặc tương đương) trong mã nguồn. Các log này bao gồm:

+ Thông tin sự kiện nhận được (Event Name, ID đơn hàng, sản phẩm, số lượng, v.v.)

+ Dữ liệu sau khi đã biến đổi (Transformed Order).

+ Thời gian bắt đầu, kết thúc xử lý và thông tin hiệu suất (thời gian chạy, dung lượng bộ nhớ sử dụng).

+ Minh chứng log hiển thị trên CloudWatch như hình dưới:



Việc ghi log giúp:

+ Theo dõi quá trình xử lý của Lambda theo thời gian thực.

+ Phân tích lỗi nhanh chóng khi có sự cố.

+ Đánh giá hiệu năng của hàm Lambda và tối ưu chi phí vận hành.

Nhờ CloudWatch, nhóm có thể đảm bảo hệ thống xử lý dữ liệu hoạt động ổn định, minh bạch và dễ bảo trì.



