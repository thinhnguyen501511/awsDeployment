---
title: "Create Lambda and Attach to DynamoDB Stream"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 2.3. </b> "
---

After creating the DynamoDB table and enabling the Stream feature, the next step is to build a Lambda function to process the events recorded from that Stream.  
AWS Lambda allows you to write code that executes in response to data changes in DynamoDB — such as when a new record is added, updated, or deleted.

In this step, we will create a Lambda function using the appropriate programming language (e.g., Python or Node.js), then configure it to be automatically triggered by events from the DynamoDB Stream.  
This enables the system to process real-time data without managing servers and scale easily when traffic increases.

+ **Benefits:**

  + **Real-time processing:** Data inserted or updated in DynamoDB is processed immediately via Lambda.
  + **No infrastructure management:** Lambda is a serverless service, so you don’t need to operate any servers.
  + **Seamless integration:** Connecting DynamoDB and Lambda via Streams is natively supported by AWS with a simple setup.

Once created, you can implement custom logic such as sending notifications, logging, synchronizing with other services, or executing domain-specific business operations.

---

#### Create Lambda Function

1. Go to [Create Lambda Function](https://ap-southeast-1.console.aws.amazon.com/lambda/home?region=ap-southeast-1#/begin)  
   + Click **Lambda**.  
   + Click **Create a function**.  

![Lambda](/images/2.prerequisite/Lambda1.png)  
![Lambda](/images/2.prerequisite/Lambda2.png)  

+ Select:  
   + **Author from scratch**  
   + Function name: **DynamoStreamProcessor**  
   + Runtime: **Node.js 22.x**  
   + Architecture: **x86_64**  
   + **Use an existing role** → Select the previously created **LambdaDynamoDBStreamRole**  

![Lambda](/images/2.prerequisite/Lambda3.png)

---

#### Attach DynamoDB Stream Trigger to the Lambda Function

After creating the Lambda function and enabling DynamoDB Streams for the table, the next step is to configure Lambda so that it is automatically triggered whenever the DynamoDB table has data changes (insert, update, delete).  
This connects the DynamoDB table (with Streams enabled) to Lambda for processing real-time data whenever there are changes.

1. Open the Lambda function you just created:  
   + Go to **Lambda**.  
   + Select the newly created function: **DynamoStreamProcessor**.  

![Lambda](/images/2.prerequisite/Lambda4.png)

2. Click **Add trigger**.  

![Lambda](/images/2.prerequisite/Lambda5.png)

3. Choose the service: **DynamoDB**.  

![Lambda](/images/2.prerequisite/Lambda6.png)

4. Configure the trigger:  
   + **Table:** `OrdersTable` (or the name of your created table)  
   + **Batch size:** Keep the default value `100`  
   + **Starting position:** Select **LATEST** (only receive new data)  

   Then click **Add**.  

![Lambda](/images/2.prerequisite/Lambda7.png)

5. After completion:  

![Lambda](/images/2.prerequisite/Lambda8.png)
