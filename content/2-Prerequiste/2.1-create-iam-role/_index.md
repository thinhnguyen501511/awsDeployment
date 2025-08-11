---
title : "Create IAM Role for AWS Lambda"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 2.1. </b> "
---

This section provides step-by-step instructions to create an IAM Role for the architecture described in the diagram.  
This IAM Role will allow the Lambda function to read from DynamoDB Streams and write logs to CloudWatch.

Once you complete this step, the architecture will look as follows:

#### Create IAM Role

1. Go to [Create IAM Role](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles/create)  
   + Click **IAM**.  
   + Click **Create Role**.  
   + Select **AWS Service**, then choose **Lambda** as the trusted entity.

![Iamrole1](/images/2.prerequisite/Iamrole.png)

![Iamrole1](/images/2.prerequisite/Iamrole11.png)

![Iamrole1](/images/2.prerequisite/Iamrole22.png)

2. Go to [Add Permissions](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles/create?trustedEntityType=AWS_SERVICE&selectedService=Lambda&selectedUseCase=Lambda)  
   + Select **AWSLambdaBasicExecutionRole**.  
   + Select **AmazonDynamoDBFullAccess**.

![Add permissions1](/images/2.prerequisite/Iamrole33.png)

![Add permissions2](/images/2.prerequisite/Iamrole44.png)

3. Click **Next**.

4. Go to [Name, Review, and Create](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles/create?trustedEntityType=AWS_SERVICE&selectedService=Lambda&selectedUseCase=Lambda)  
   + Enter the name **data-streaming-system-role**.  
   + Click **Create Role**.

![role1](/images/2.prerequisite/Iamrole55.png)  
![role2](/images/2.prerequisite/Iamrole66.png)

### Contents
  - [Create DynamoDB](../2.2-create-dynam/)
