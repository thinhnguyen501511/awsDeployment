---
title: "Session Management"
date: "`r Sys.Date()`" 
weight: 1 
chapter: false
---
# DynamoDB Triggers & Stream Processing with Lambda


### Overall
In this project, you will explore and implement a real-time data processing system using DynamoDB Streams and AWS Lambda. Whenever there is a change in the DynamoDB table (insert, update, delete), the event will be recorded in the stream and immediately trigger a Lambda function for processing. The system will perform data transformation, aggregation, error handling, and log the results to services such as S3, RDS, or send them to monitoring systems.

The main goal is to build a fully serverless architecture that ensures automatic scalability, high performance, cost optimization, and easy maintenance. You will also implement techniques such as performance monitoring, test framework design, and error operation procedures to complete a modern and practical stream data processing system.


![Clean](/images/6.clean/sodoaws.png)

### Content
1. [Introduction](1-introduce/)
2. [Preparation](2-prerequiste/)
3. [Data Transformation Logic](3-transformation-logic/)
4. [Error Handling](4-Error-Handling/)
5. [Clean Up Resources](5-cleanup/)


