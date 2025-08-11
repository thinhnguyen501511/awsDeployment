---
title : "Tổng hợp dữ liệu"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 3.2. </b> "
---

Trong các hệ thống xử lý dữ liệu thời gian thực, việc chỉ ghi nhận từng sự kiện riêng lẻ là chưa đủ. Một yêu cầu phổ biến trong thực tế là cần phải tổng hợp dữ liệu nhằm cung cấp thông tin mang tính khái quát, hỗ trợ cho việc phân tích và ra quyết định nhanh chóng.

Với đề tài này, mỗi khi có một đơn hàng mới được ghi nhận vào bảng OrdersTable, hệ thống không chỉ xử lý sự kiện đó mà còn cập nhật tổng số lượng của từng sản phẩm đã được đặt. Điều này mang lại cái nhìn trực quan hơn về xu hướng tiêu dùng theo thời gian thực mà không cần chạy batch job vào cuối ngày như các hệ thống truyền thống.

Để hiện thực điều này, ta triển khai thuật toán tổng hợp ngay bên trong hàm Lambda bằng cách sử dụng DynamoDB UpdateItem với biểu thức ADD, đảm bảo hiệu năng và tính nhất quán cao. Mọi thay đổi đều được ghi nhận tức thì, phù hợp với đặc trưng của các hệ thống serverless event-driven hiện đại.


1. Tạo bảng tổng hợp mới [Tạo bảng](https://ap-southeast-1.console.aws.amazon.com/dynamodbv2/home?region=ap-southeast-1#tables).

   + Truy cập DynamoDB > Tables > Create Table

![Create](/images/3.s3/Lambda3.2.1.png)

+ Nhập thông tin:

   + Table name: AggregateTable

   + Partition key: product (kiểu String)

   + Bấm Create Table

2. Cập nhật Lambda để ghi dữ liệu vào bảng
   + Mở lại hàm Lambda đã xử lý stream.
   + Thêm quyền ghi vào AggregateTable:
      + Vào Configuration > Permissions > Rolename (VD: **LambdaDynamoDBStreamRole**)

![Create S3](/images/3.s3/Lambda3.2.2.png)
   + Trong trang IAM Role, chọn Add permissions > Attach policies

![Create S3](/images/3.s3/Lambda3.2.3.png)
   + Gán quyền AmazonDynamoDBFullAccess (hoặc custom policy chỉ cho phép PutItem, UpdateItem trên bảng AggregateTable)

   + Sau đó quay lại Lambda functions cập nhật lại đoạn code như sau:

   ```bash
   import { DynamoDBClient, UpdateItemCommand } from "@aws-sdk/client-dynamodb";

const client = new DynamoDBClient({});

export const handler = async (event) => {
  for (const record of event.Records) {
    console.log("📥 Event Name:", record.eventName);

    const newImage = record.dynamodb?.NewImage;
    if (!newImage) continue;

    const orderId = newImage.OrderID?.S || "unknown";
    const product = newImage.Product?.S || "unknown";
    const quantity = parseInt(newImage.Quantity?.N || "0");

    console.log(`🛒 New Order Received - ID: ${orderId}, Product: ${product}, Quantity: ${quantity}`);

    const transformedOrder = {
      orderId,
      product,
      quantity
    };
    console.log("🔁 Transformed Order:", transformedOrder);

    const params = {
      TableName: "AggregateTable",
      Key: {
        Product: { S: product }
      },
      UpdateExpression: "SET totalQuantity = if_not_exists(totalQuantity, :zero) + :qty",
      ExpressionAttributeValues: {
        ":qty": { N: quantity.toString() },
        ":zero": { N: "0" }
      },
      ReturnValues: "UPDATED_NEW"
    };

    try {
      const result = await client.send(new UpdateItemCommand(params));
      const newTotal = result.Attributes?.totalQuantity?.N;

      console.log(`📊 Tổng số lượng sau cộng dồn: ${newTotal}`);
      console.log(`✅ Cộng dồn thành công vào AggregateTable cho sản phẩm ${product}`);
    } catch (err) {
      console.error("❌ Lỗi khi cập nhật AggregateTable:", err);
    }
  }

  return {
    statusCode: 200,
    body: "OK"
  };
};

```
![Create S3](/images/3.s3/Lambda3.2.5.png)

3. Kiểm tra hoạt động
   + Vào OrdersTable > Items > Create Item

   + Tạo item mới với OrderID, Product, Quantity

![Create S3](/images/3.s3/Lambda3.2.6.png)

   + Chọn **JSON view**
   ```
   {
  "OrderID": {
    "S": "order-1"
  },
  "Product": {
    "S": "Notebook"
  },
  "Quantity": {
    "N": "5"
  }
}
```
![Create S3](/images/3.s3/Lambda3.2.7.png)

![Create S3](/images/3.s3/Lambda3.2.8.png)

   + Chờ 1-2s → Mở AggregateTable, chọn Scan > Run

![Create S3](/images/3.s3/Lambda3.2.9.png)

   + Kiểm tra cột totalQuantity đã được cập nhật chính xác theo Product

![Create S3](/images/3.s3/Lambda3.2.10.png)


