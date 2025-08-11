---
title : "Data Aggregation"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 3.2. </b> "
---

In real-time data processing systems, merely recording individual events is not enough.  
A common real-world requirement is to aggregate data to provide generalized insights, enabling faster analysis and decision-making.

In this project, whenever a new order is recorded in the **OrdersTable**, the system not only processes that event but also updates the total quantity of each product ordered. This offers a more intuitive view of consumer trends in real time without having to run batch jobs at the end of the day like traditional systems.

To achieve this, we implement the aggregation logic directly inside the Lambda function using **DynamoDB UpdateItem** with the **ADD** expression. This ensures high performance and strong consistency. All changes are recorded instantly, matching the characteristics of modern serverless event-driven architectures.

---

1. **Create a new aggregation table** [Create Table](https://ap-southeast-1.console.aws.amazon.com/dynamodbv2/home?region=ap-southeast-1#tables)

   + Go to **DynamoDB > Tables > Create Table**

![Create](/images/3.s3/Lambda3.2.1.png)

+ Enter the following details:

   + **Table name:** AggregateTable

   + **Partition key:** product (String type)

   + Click **Create Table**

---

2. **Update Lambda to write data into the table**
   + Reopen the Lambda function that processes the stream.
   + Add write permissions to **AggregateTable**:
      + Go to **Configuration > Permissions > Rolename** (e.g., **LambdaDynamoDBStreamRole**)

![Create S3](/images/3.s3/Lambda3.2.2.png)

   + In the IAM Role page, choose **Add permissions > Attach policies**

![Create S3](/images/3.s3/Lambda3.2.3.png)

   + Attach the **AmazonDynamoDBFullAccess** policy (or a custom policy allowing only `PutItem` and `UpdateItem` on the **AggregateTable**).

   + Then go back to the Lambda function and update the code as follows:

```javascript
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

      console.log(`📊 Total quantity after aggregation: ${newTotal}`);
      console.log(`✅ Successfully aggregated into AggregateTable for product ${product}`);
    } catch (err) {
      console.error("❌ Error updating AggregateTable:", err);
    }
  }

  return {
    statusCode: 200,
    body: "OK"
  };
};
```
![Create S3](/images/3.s3/Lambda3.2.5.png)

3. Test the functionality:

   + Go to OrdersTable > Items > Create Item
   + Create a new item with OrderID, Product, Quantity

![Create S3](/images/3.s3/Lambda3.2.6.png)

   + Select **JSON view**
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

   + Wait 1–2 seconds → Open AggregateTable, choose Scan > Run

![Create S3](/images/3.s3/Lambda3.2.9.png)

   + Verify that the totalQuantity column has been correctly updated for the corresponding Product.

![Create S3](/images/3.s3/Lambda3.2.10.png)
