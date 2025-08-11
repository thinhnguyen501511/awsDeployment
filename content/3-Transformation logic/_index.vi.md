---
title : "Logic biến đổi dữ liệu"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

Trong một hệ thống xử lý dữ liệu thời gian thực, việc tiếp nhận dữ liệu từ nguồn (như DynamoDB Stream) mới chỉ là bước khởi đầu. Để tạo ra giá trị từ dòng dữ liệu này, chúng ta cần thực hiện quá trình chuyển đổi (transformation) – biến đổi dữ liệu thô thành định dạng phù hợp với mục đích xử lý, lưu trữ hoặc hiển thị.

Lambda function chính là nơi đảm nhận vai trò này. Mỗi khi có thay đổi trên bảng DynamoDB, một bản ghi sự kiện sẽ được gửi vào hàm Lambda. Tại đây, dữ liệu sẽ được trích xuất, phân tích và xử lý theo logic nghiệp vụ cụ thể. Đây là bước then chốt giúp hệ thống trở nên thông minh, linh hoạt và có thể mở rộng trong các tình huống thực tế.

### Nội dung

 - [Xử lý dữ liệu trong Lambda](3.1-create-s3-uploadimage/) 
 - [Tổng hợp dữ liệu](3.2-Create-RDS/)
 - [Ghi log và giám sát xử lý với CloudWatch](3.3-log-and-monitor-with-cloudwatch/)