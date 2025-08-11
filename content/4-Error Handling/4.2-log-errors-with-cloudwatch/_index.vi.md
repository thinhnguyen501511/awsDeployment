---
  title : "Ghi Log lỗi với CloudWatch"
  date : "`r Sys.Date()`"
  weight : 2
  chapter : false
  pre : " <b> 4.2. </b> "
---


Khi hệ thống gặp lỗi, việc ghi lại thông tin chi tiết của lỗi là bước quan trọng để hỗ trợ phân tích nguyên nhân và khắc phục sự cố. AWS CloudWatch là dịch vụ giám sát và thu thập log mặc định cho Lambda, giúp bạn dễ dàng theo dõi toàn bộ quá trình xử lý, bao gồm cả khi xảy ra lỗi.

#### Cách Ghi Log Lỗi

Trong mã nguồn Lambda, bạn có thể sử dụng:

+ console.error() để ghi log lỗi.

+ console.warn() để cảnh báo.

+ console.log() cho thông tin chung.

**Ví dụ:**
```
try {
  // Logic xử lý dữ liệu
} catch (error) {
  console.error("❌ Error processing record:", error);
  console.error("📄 Stack trace:", error.stack);
}
```

**Theo dõi log trên CloudWatch**
1. Mở AWS Management Console.

2. Chọn CloudWatch → Log groups.

3. Tìm log group theo tên hàm Lambda, ví dụ: /aws/lambda/DynamoStreamProcessor.

4. Chọn log stream mới nhất để xem chi tiết lỗi.

**Ý nghĩa của việc ghi log lỗi**
+ Phân tích nhanh nguyên nhân sự cố: Xác định lỗi thuộc về dữ liệu đầu vào, kết nối dịch vụ hay logic xử lý.

+ Theo dõi tần suất lỗi: Xác định xem lỗi xảy ra lẻ tẻ hay liên tục.

+ Hỗ trợ cảnh báo tự động: Có thể kết hợp CloudWatch Alarm để gửi email/SMS khi xuất hiện số lượng lỗi vượt ngưỡng.