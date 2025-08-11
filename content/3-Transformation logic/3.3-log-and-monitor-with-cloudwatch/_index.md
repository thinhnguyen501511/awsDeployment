---
title : "Logging and Monitoring Processing with CloudWatch"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3.3. </b> "
---

During system operation, logging plays a crucial role in tracking, analyzing, and troubleshooting issues. AWS provides the Amazon CloudWatch service, which allows collecting, storing, and monitoring logs from other services such as AWS Lambda, DynamoDB, and more.

When Lambda processes data from a DynamoDB Stream, all relevant information is programmed to be logged via `console.log()` statements (or equivalent) in the source code. These logs include:

+ Information about the received event (Event Name, Order ID, Product, Quantity, etc.)

+ Data after transformation (Transformed Order).

+ Processing start and end times, along with performance metrics (execution time, memory usage).

+ Example log output displayed in CloudWatch as shown in the figure below:

Logging helps to:

+ Track Lambda's processing in real-time.

+ Quickly analyze errors when issues occur.

+ Evaluate the performance of the Lambda function and optimize operational costs.

Thanks to CloudWatch, the team can ensure that the data processing system operates stably, transparently, and is easy to maintain.
