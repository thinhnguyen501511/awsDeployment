---
title : "Processing Data in Lambda"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 3.1. </b> "
---

In a real-time processing system, receiving and transforming data from an event stream is a crucial step to ensure that the data is analyzed and used for the right purposes. **AWS DynamoDB Stream** allows you to monitor every change in a table, and **AWS Lambda** acts as the "listener" that processes the data immediately when a change occurs.

In this section, we will implement the **transformation logic** inside the Lambda function. Data from the DynamoDB Stream will be retrieved, decoded, and transformed according to specific business requirements, laying the foundation for subsequent processing steps such as aggregation, storage, analysis, or sending to other systems.

1. Go to the [Lambda Function](https://ap-southeast-1.console.aws.amazon.com/lambda/home?region=ap-southeast-1#/functions) you created:
  + Select the function you created, for example: **DynamoStreamProcessor**
  + Scroll down to **Code source**
  
![Lambda](/images/2.prerequisite/Lambda4.png)

  + Paste the following code:
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

        // Example transformation: calculate order value (assuming each item costs 10)
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
  + Explanation:
    + `event.Records`: A list of events from DynamoDB (each change may send multiple records).

    + `record.eventName`: Specifies the type of change (INSERT, MODIFY, REMOVE).

    + `record.dynamodb.NewImage`: The new data after the change.

    + `transformed` variable: The place where you implement your data transformation logic.

### Testing the Data
To verify that the Lambda function is working according to the logic you wrote, we will create new data in the DynamoDB table and check whether the Lambda function is triggered.

1. Create a new record in the DynamoDB table
  + Go to AWS Console → DynamoDB → select the table you created (**OrdersTable**)  
![Lambda](/images/2.prerequisite/Lambda10.png)

  + Select **Explore table items**  
![Lambda](/images/2.prerequisite/Lambda11.png)

  + Click **Create item**  
![Lambda](/images/2.prerequisite/Lambda12.png)

  + Choose **JSON view**  
  + Add a new record  
  + Click **Create item**  
![Lambda](/images/2.prerequisite/Lambda13.png)

2. **Check the Lambda execution results**
  + Go to AWS Console > CloudWatch
  + In the left menu, choose: Logs → Log groups
  + Find the log group by your Lambda function name: **/aws/lambda/DynamoStreamProcessor**
  + Click on that log group.  
![Lambda](/images/2.prerequisite/Lambda14.png)

  + Select the most recent log stream – corresponding to the time you created the item in DynamoDB.  
![Lambda](/images/2.prerequisite/Lambda15.png)

  + You will see multiple log lines similar to this:  
![Lambda](/images/2.prerequisite/Lambda16.png)

  + Meaning:
    + 📥 **Event Name**: Indicates whether the action was INSERT, MODIFY, or REMOVE.

    + 🟢 **New Order Received**: Data was successfully read from the DynamoDB stream.

    + 🔁 **Transformed Order**: The data was successfully processed according to the logic you wrote in the Lambda function.

    + **REPORT**: Summary of processing time, memory usage, etc.
