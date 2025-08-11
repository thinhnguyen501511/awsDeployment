---
  title : "Sử dụng Dead Letter Queue (DLQ) để lưu lỗi"
  date : "`r Sys.Date()`"
  weight : 3
  chapter : false
  pre : " <b> 4.3. </b> "
---


Trong các hệ thống xử lý dữ liệu thời gian thực, khi Lambda gặp lỗi liên tục (ví dụ dữ liệu không hợp lệ hoặc dịch vụ đích không khả dụng), nếu không xử lý khéo, dữ liệu lỗi sẽ bị mất hoặc làm nghẽn toàn bộ luồng xử lý. AWS hỗ trợ Dead Letter Queue (DLQ) để lưu trữ những sự kiện không xử lý thành công, giúp bạn phân tích và xử lý lại sau.

### Nguyên lý hoạt động

+ Khi Lambda không xử lý được sự kiện sau số lần retry tối đa, sự kiện đó sẽ được gửi vào DLQ (thường là SQS hoặc SNS).

+ DLQ giúp tách dữ liệu lỗi ra khỏi luồng chính, tránh ảnh hưởng tới các sự kiện hợp lệ.

### Cách cấu hình DLQ cho Lambda
1. Mở AWS Lambda Console → chọn function cần cấu hình.

2. Chuyển đến tab Configuration → Asynchronous invocation.

3. Ở phần Dead-letter queue, chọn:

    + SQS queue hoặc SNS topic đã tạo trước đó.

4. Lưu cấu hình.

### Ví dụ kịch bản
Giả sử Lambda đọc dữ liệu từ DynamoDB Stream nhưng gặp một bản ghi bị thiếu trường bắt buộc:

+ Lambda sẽ retry theo cấu hình.

+ Nếu vẫn thất bại, bản ghi đó được gửi vào SQS DLQ.

+ Bạn có thể tạo một Lambda khác đọc từ DLQ để xử lý thủ công hoặc gửi cảnh báo.

Lợi ích của DLQ:

+ Không mất dữ liệu lỗi: Mọi bản ghi thất bại đều được lưu lại.

+ Dễ dàng xử lý lại: Có thể chạy lại logic hoặc chỉnh sửa dữ liệu.

+ Tăng độ ổn định: Ngăn sự cố lan rộng sang các sự kiện khác.