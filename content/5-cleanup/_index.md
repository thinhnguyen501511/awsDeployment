---
title : "Clean Up Resources"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : "<b>5. </b>"
---

After completing testing or deployment, cleaning up unused AWS resources is crucial to:  
+ Avoid unnecessary costs.  
+ Reduce security risks from unused services or permissions.  
+ Keep your AWS account organized and easier to manage.  

**Below is a detailed guide to delete each type of resource used in the project.**  

#### Delete Lambda Functions

1. Go to [Lambda](https://ap-southeast-1.console.aws.amazon.com/lambda/home?region=ap-southeast-1#/functions)  
   + Select the **Functions** you want to delete.  
   + Choose **Actions** → **Delete**.  
   + Type **confirm** → Select **Delete**.  

![Clean](/images/6.clean/cleanlambda1.png)  

![Clean](/images/6.clean/cleanlambda2.png)  

---

### Delete DynamoDB Tables and Streams

1. Go to [DynamoDB](https://ap-southeast-1.console.aws.amazon.com/dynamodbv2/home?region=ap-southeast-1#tables)  
   + Select the tables you created.  
   + Choose **Delete**.  
   + Type **confirm** → **Delete**.  

![Clean](/images/6.clean/cleanlambda3.png)  

![Clean](/images/6.clean/cleanlambda4.png)  

💡 **Note:** If the table has DynamoDB Streams enabled, deleting the table will also delete the associated stream and remove any related Lambda triggers.

---

#### Delete SQS/SNS (DLQ)

**If your project used a Dead Letter Queue (DLQ):**  
1. Open **SQS** (if DLQ is an SQS queue):  
   + Select the queue you want to delete.  
   + Click **Delete** and confirm.  
2. Open **SNS** (if DLQ is an SNS topic):  
   + Select the topic you want to delete.  
   + Click **Delete** and confirm.  

---

#### Delete CloudWatch Log Groups

1. Go to [CloudWatch](https://ap-southeast-1.console.aws.amazon.com/cloudwatch/home?region=ap-southeast-1#home:)  
2. Choose **Log groups**.  
3. Find the log group matching your Lambda function name, e.g., `/aws/lambda/DynamoStreamProcessor`.  
4. Select the log group → **Actions → Delete log group**.  
5. Click **Delete** to confirm.  

![Clean](/images/6.clean/cleanlambda5.png)  

![Clean](/images/6.clean/cleanlambda6.png)  

---

#### Delete IAM Roles

1. Go to [IAM Roles](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles)  
2. Select the role(s) used by your Lambda or other services in the project.  
3. Click **Delete**.  
4. Type **delete** → Click **Delete** to confirm.  

![Clean](/images/6.clean/cleanlambda7.png)  

![Clean](/images/6.clean/cleanlambda8.png)  
