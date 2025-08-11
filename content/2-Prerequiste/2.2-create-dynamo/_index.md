---
title: "Create DynamoDB Table and Enable DynamoDB Stream"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 2.2. </b> "
---

### Create DynamoDB

To process real-time data in a Serverless system, we need a mechanism to listen for changes happening in the database.  
DynamoDB Streams is the tool that supports this goal.  
In this step, we will create a DynamoDB table to store data and enable the Stream feature, allowing services such as AWS Lambda to be automatically triggered whenever there are changes (insert, update, delete) in the table.

Enabling DynamoDB Streams helps you build a powerful real-time data processing pipeline, such as logging, data synchronization, statistical calculations, or transforming data into another system.  
This is an essential foundation for event-driven architecture.

1. Go to [DynamoDB](https://us-east-1.console.aws.amazon.com/dynamodbv2/home?region=us-east-1#create-table)  

   + Click **DynamoDB**.  
   + Click **Tables**, then click **Create table**.  

![role](/images/2.prerequisite/Dynamo1.png)

2. In the table creation form:  
    + Set the table name to **OrdersTable**  
    + Set the partition key to **OrderID**  
    + Select **Customize settings**  

![role1](/images/2.prerequisite/Dynamo2.png)

   + Then click **Create table**.  

![role1](/images/2.prerequisite/Dynamo3.png)

3. Enable DynamoDB Stream  
    + Click on the table you just created.  
    + Select **Exports and Streams**.  

![role1](/images/2.prerequisite/Dynamo4.png)

   + In the *DynamoDB stream details* section, click **Turn on**.  

![role1](/images/2.prerequisite/Dynamo5.png)

   + Choose **New and old images**.  
   + Click **Turn on stream**.  

![role1](/images/2.prerequisite/Dynamo6.png)
