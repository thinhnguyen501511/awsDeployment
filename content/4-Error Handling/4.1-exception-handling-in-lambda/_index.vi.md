---
  title : "Xử lý ngoại lệ trong Lambda"
  date : "`r Sys.Date()`"
  weight : 1
  chapter : false
  pre : " <b> 4.1. </b> "
---


Trong các hàm Lambda xử lý dữ liệu từ DynamoDB Stream, việc phát sinh lỗi là điều không thể tránh khỏi, đặc biệt khi dữ liệu không đúng định dạng, thiếu trường bắt buộc hoặc gặp sự cố khi kết nối với dịch vụ khác. Nếu không xử lý ngoại lệ đúng cách, toàn bộ tiến trình có thể bị dừng hoặc lặp lại nhiều lần không cần thiết.

Một số nguyên tắc xử lý ngoại lệ trong Lambda:

+ Bao bọc logic bằng try...catch (Node.js) hoặc try...except (Python) để bắt các lỗi runtime.

+ Ghi log chi tiết lỗi để hỗ trợ debug.

+ Không nuốt lỗi hoàn toàn — cần trả về thông tin hoặc throw tiếp để hệ thống có thể retry nếu cần.

+ Phân loại lỗi: lỗi tạm thời (temporary error) có thể retry, lỗi dữ liệu (permanent error) thì nên đưa vào Dead Letter Queue để xử lý thủ công.

Ví dụ với Node.js:
```
export const handler = async (event) => {
  for (const record of event.Records) {
    try {
      console.log('Event Name:', record.eventName);

      const newImage = record.dynamodb?.NewImage;
      if (!newImage) {
        throw new Error("Missing NewImage in record");
      }

      const orderId = newImage.OrderID?.S;
      const product = newImage.Product?.S;
      const quantity = parseInt(newImage.Quantity?.N);

      if (!orderId || !product || isNaN(quantity)) {
        throw new Error(`Invalid data: ${JSON.stringify(newImage)}`);
      }

      const transformed = {
        orderId,
        product,
        totalCost: quantity * 10,
      };

      console.log('Transformed Order:', transformed);

      // Ghi dữ liệu vào bảng khác hoặc gửi đi hệ thống khác...
      
    } catch (err) {
      console.error("Error processing record:", err);
      // Có thể gửi dữ liệu lỗi vào DLQ hoặc service khác để xử lý sau
    }
  }

  return { statusCode: 200, body: 'Processing completed' };
};

```
Lưu ý:

+ console.error() sẽ ghi log dưới dạng lỗi trong CloudWatch, giúp dễ dàng lọc và phân tích.

+ Nếu muốn Lambda tự động retry, có thể throw lại lỗi thay vì nuốt trong catch.

+ Đối với dữ liệu lỗi vĩnh viễn (permanent error), nên cấu hình DLQ để lưu trữ và xử lý thủ công.