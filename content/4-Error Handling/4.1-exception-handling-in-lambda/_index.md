---
  title : "Exception Handling in Lambda"
  date : "`r Sys.Date()`"
  weight : 1
  chapter : false
  pre : " <b> 4.1. </b> "
---

In Lambda functions that process data from DynamoDB Streams, errors are inevitable—especially when the data is malformed, missing required fields, or encounters issues connecting to other services. Without proper exception handling, the entire process may stop or repeat unnecessarily.

Some principles for handling exceptions in Lambda:

+ Wrap your logic with `try...catch` (Node.js) or `try...except` (Python) to capture runtime errors.

+ Log detailed error information to assist debugging.

+ Avoid completely swallowing errors — return information or rethrow them so the system can retry if necessary.

+ Classify errors: temporary errors can be retried; permanent errors (data-related) should be sent to a Dead Letter Queue (DLQ) for manual processing.

Example in Node.js:
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

      // Write data to another table or send it to another system...
      
    } catch (err) {
      console.error("Error processing record:", err);
      // You may send the failed data to a DLQ or another service for later processing
    }
  }

  return { statusCode: 200, body: 'Processing completed' };
};
```

**Notes:**

+ console.error() will log the message as an error in CloudWatch, making it easier to filter and analyze.

+ If you want Lambda to automatically retry, you can rethrow the error instead of swallowing it inside catch.

+ For permanent data errors, configure a DLQ to store and process them manually.