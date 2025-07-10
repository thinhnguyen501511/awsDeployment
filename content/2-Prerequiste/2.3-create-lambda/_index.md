---
title : "Create Lambda and Attach to DynamoDB Stream"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---

After setting up the DynamoDB table and enabling the Stream feature, the next step is to create a Lambda function to process events emitted by the stream. AWS Lambda allows you to run custom code in response to changes in DynamoDB — such as inserting, updating, or deleting items — without managing any servers.

In this step, we will create a Lambda function (e.g., in Python or Node.js), and configure it to be automatically triggered by events from the DynamoDB Stream. This enables real-time data processing in a fully managed and scalable environment.

+ Benefits:
   + Real-time processing: Changes in DynamoDB (insert, update, delete) are immediately captured and handled by Lambda.

   + Serverless infrastructure: No need to provision or manage any servers — AWS handles the infrastructure.

   + Seamless integration: Connecting Lambda to DynamoDB Streams is supported natively by AWS, making the setup quick and straightforward.

Once the function is created, you can define your own logic such as sending notifications, logging, syncing to other services, or applying business rules based on the data change.


#### Create IAM role 

1. Go to [Create Iam Role](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles/create)
   + Click **Iam**.
   + Click **Create Role**.
   + Click **AWS service**, then click **ec2** to confirm.

![Iamrole1](/images/2.prerequisite/IAMrole1.png)

![Iamrole1](/images/2.prerequisite/IAMrole2.png)

![Iamrole1](/images/2.prerequisite/IAMrole3.png)

2. Go to [Add permissionsn ](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles/create?trustedEntityType=AWS_SERVICE&selectedService=EC2&selectedUseCase=EC2)
   + Click **AmazonEC2FullAccess**.
   + Click **AmazonS3FullAccess**.
   + Click **AmazonRDSFullAccess**

![Add permissions1](/images/2.prerequisite/IAMrole4.png)

![Add permissions2](/images/2.prerequisite/IAMrole5.png)

![Add permissions3](/images/2.prerequisite/IAMrole6.png)

1. Go to [Name, review, and create ](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles/details/phi1234?section=permissions)
   + Name **data-streaming-system-role**..
   + Click **Create Role**

![role1](/images/2.prerequisite/IAMrole7.png)
![role2](/images/2.prerequisite/IAMrole8.png)



### Content
  - [Create EC2](../2.2-create-ec2/)