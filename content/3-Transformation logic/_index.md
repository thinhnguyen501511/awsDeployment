---
title : "Data Transformation Logic"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

In a real-time data processing system, receiving data from a source (such as DynamoDB Streams) is only the first step. To create value from this data stream, we need to perform a **transformation process**—converting raw data into a format suitable for processing, storage, or display.

The **Lambda function** plays the central role in this process. Whenever a change occurs in the DynamoDB table, an event record will be sent to the Lambda function. Here, the data is extracted, analyzed, and processed according to specific business logic. This is a crucial step that makes the system intelligent, flexible, and scalable in real-world scenarios.

### Contents

- [Processing Data in Lambda](3.1-create-s3-uploadimage/)  
- [Data Aggregation](3.2-Create-RDS/)  
- [Logging and Monitoring with CloudWatch](3.3-log-and-monitor-with-cloudwatch/)
