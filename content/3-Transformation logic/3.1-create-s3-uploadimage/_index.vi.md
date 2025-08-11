---
title : "Xử lý dữ liệu trong Lambda "
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 3.1. </b> "
---

Trong một hệ thống xử lý thời gian thực, việc tiếp nhận và chuyển đổi dữ liệu từ luồng sự kiện (stream) là bước quan trọng nhằm đảm bảo dữ liệu được phân tích và sử dụng đúng mục đích. AWS DynamoDB Stream cho phép theo dõi mọi thay đổi trong bảng dữ liệu, và AWS Lambda đóng vai trò là "người nghe" (listener) thực hiện xử lý ngay khi có thay đổi xảy ra.

Trong phần này, ta sẽ hiện thực hóa transformation logic – logic biến đổi dữ liệu – trong Lambda function. Dữ liệu từ DynamoDB Stream sẽ được truy xuất, giải mã và biến đổi theo yêu cầu nghiệp vụ cụ thể, giúp tạo tiền đề cho các bước xử lý tiếp theo như tổng hợp, lưu trữ, phân tích hoặc gửi đi các hệ thống khác.

1. Đi tới [Lambda Function](https://ap-southeast-1.console.aws.amazon.com/lambda/home?region=ap-southeast-1#/functions) đã tạo:
  + Chọn function bạn đã tạo, ví dụ: **DynamoStreamProcessor**
  + Kéo xuống phần **Code source**
  
![Lambda](/images/2.prerequisite/Lambda4.png)

  + Gán đoạn code vào như sau:
  ```
  export const handler = async (event) => {
  for (const record of event.Records) {
    console.log('Event Name:', record.eventName);

    const newImage = record.dynamodb?.NewImage;
    if (newImage) {
      const orderId = newImage.OrderID?.S;
      const product = newImage.Product?.S;
      const quantity = newImage.Quantity?.N;

      console.log(`New Order Received - ID: ${orderId}, Product: ${product}, Quantity: ${quantity}`);

      // Ví dụ transform: tính giá trị đơn hàng (giả định giá mỗi món là 10)
      const transformed = {
        orderId,
        product,
        totalCost: Number(quantity) * 10,
      };

      console.log('Transformed Order:', transformed);
    }
  }

  return { statusCode: 200, body: 'Stream processed successfully' };
};
```

![Lambda](/images/2.prerequisite/Lambda9.1.png)
  + Giải thích:
    + event.Records: Là danh sách các sự kiện từ DynamoDB (mỗi lần thay đổi có thể gửi nhiều record).

    + record.eventName: Xác định loại thay đổi (INSERT, MODIFY, REMOVE).

    + record.dynamodb.NewImage: Dữ liệu mới sau khi thay đổi.

    + Biến transformed: Là nơi bạn thực hiện logic biến đổi dữ liệu.

### Kiểm Thử Dữ Liệu
Để xác nhận rằng Lambda hoạt động đúng logic bạn đã viết, ta sẽ thử tạo dữ liệu mới vào bảng DynamoDB và xem Lambda có kích hoạt không.
1. Tạo bản ghi mới trong bảng DynamoDB
  + Vào AWS Console → DynamoDB → chọn bảng bạn đã tạo (**OrdersTable**)
![Lambda](/images/2.prerequisite/Lambda10.png)

  + Chọn **Explore table items**
![Lambda](/images/2.prerequisite/Lambda11.png)

  + Chọn **Create item**
![Lambda](/images/2.prerequisite/Lambda12.png)

  + Chọn **JSON view**
  + Thêm bản ghi mới
  + Chọn **Create item**
![Lambda](/images/2.prerequisite/Lambda13.png)


2. **Kiểm tra kết quả thực thi của Lambda**
  + Vào AWS Console > CloudWatch
  + Chọn menu bên trái: Logs → Log groups
  + Tìm log group theo tên hàm Lambda: **/aws/lambda/DynamoStreamProcessor**
  + Nhấn vào log group đó.
![Lambda](/images/2.prerequisite/Lambda14.png)

  + Chọn log stream có thời gian gần nhất – tương ứng với lần bạn tạo item trong DynamoDB.
![Lambda](/images/2.prerequisite/Lambda15.png)

  + Bạn sẽ thấy nhiều dòng log tương tự sau:
![Lambda](/images/2.prerequisite/Lambda16.png)

  + Ý nghĩa:
    + 📥 Event Name: Cho biết đây là thao tác INSERT, MODIFY, hay REMOVE

    + 🟢 New Order Received: Đã đọc được dữ liệu từ DynamoDB stream

    + 🔁 Transformed Order: Đã xử lý thành công theo logic bạn viết trong Lambda

    + REPORT: Tổng thời gian xử lý, bộ nhớ dùng, v.v.




