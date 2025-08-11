---
  title : "Tự động cảnh báo khi có lỗi bằng CloudWatch Alarm"
  date : "`r Sys.Date()`"
  weight : 4
  chapter : false
  pre : " <b> 4.4. </b> "
---

Việc ghi log hoặc lưu dữ liệu lỗi vào DLQ là chưa đủ nếu nhóm vận hành không được thông báo kịp thời. Để chủ động phát hiện sự cố, AWS cung cấp CloudWatch Alarm kết hợp với SNS để gửi cảnh báo qua email, SMS hoặc các hệ thống chat như Slack.

### Nguyên lý hoạt động
+ CloudWatch Metrics sẽ ghi nhận số lượng lỗi hoặc số lần Lambda thất bại.

+ CloudWatch Alarm sẽ theo dõi các metric này.

+ Khi vượt ngưỡng đã định, Alarm sẽ kích hoạt hành động gửi thông báo qua SNS.

**Cách thiết lập cảnh báo**
1. Tạo SNS Topic để nhận thông báo

    + Mở SNS Console → Create topic → chọn Standard.

    + Đặt tên, tạo topic, sau đó Create subscription để đăng ký email hoặc SMS nhận thông báo.

    + Xác nhận đăng ký qua email.

2. Tạo CloudWatch Alarm

    + Mở CloudWatch Console → Alarms → Create alarm.

    + Chọn Lambda metrics → Errors hoặc DeadLetterErrors.

    + Đặt ngưỡng ví dụ: > 3 lỗi trong 5 phút.

    + Chọn Actions → gửi tới SNS Topic vừa tạo.

3. Lưu và kích hoạt alarm

**Ví dụ tình huống**
+ Nếu Lambda thất bại 5 lần liên tiếp trong vòng 10 phút, CloudWatch Alarm sẽ gửi email tới nhóm vận hành ngay lập tức.

+ Nhóm có thể vào kiểm tra log hoặc DLQ để xử lý nguyên nhân.

**Lợi ích:**
Phản ứng nhanh: Giảm thời gian phát hiện sự cố.

Giảm rủi ro mất dữ liệu: Can thiệp sớm khi lỗi xuất hiện hàng loạt.

Tự động hóa giám sát: Không cần ngồi xem log thủ công.
