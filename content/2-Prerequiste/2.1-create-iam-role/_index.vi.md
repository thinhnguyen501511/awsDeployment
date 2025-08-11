---
title : "Tạo IAM Role cho AWS Lambda"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 2.1. </b> "
---

Phần này hướng dẫn các bước để tạo một IAM Role cho kiến trúc được mô tả trong sơ đồ. IAM Role này sẽ cho phép Lambda function có quyền đọc DynamoDB Stream và ghi log ra CloudWatch.

Tổng quan kiến trúc sau khi bạn hoàn thành bước này sẽ như sau:


#### Tạo vai trò IAM

1. Đi tới [Tạo vai trò Iam](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles/create)
   + Nhấp vào **Iam**.
   + Nhấp vào **Tạo vai trò**.
   + Nhấp vào **Dịch vụ AWS**, sau đó Nhấp vào **Lambda** để xác nhận.


![Iamrole1](/images/2.prerequisite/Iamrole.png)

![Iamrole1](/images/2.prerequisite/Iamrole11.png)

![Iamrole1](/images/2.prerequisite/Iamrole22.png)

1. Đi tới [Thêm quyền](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles/create?trustedEntityType=AWS_SERVICE&selectedService=Lambda&selectedUseCase=Lambda)
   + Nhấp vào **AWSLambdaBasicExecutionRole**.
   + Nhấp vào **AmazonDynamoDBFullAccess**.

![Add permissions1](/images/2.prerequisite/Iamrole33.png)

![Add permissions2](/images/2.prerequisite/Iamrole44.png)

2. Đi tới [Tiếp theo]

3. Đi tới [Tên, đánh giá và tạo](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles/create?trustedEntityType=AWS_SERVICE&selectedService=Lambda&selectedUseCase=Lambda)
   + Tên **data-streaming-system-role**..
   + Bấm vào **Tạo vai trò**

![role1](/images/2.prerequisite/Iamrole55.png)
![role2](/images/2.prerequisite/Iamrole66.png)



### Nội dung
  - [Create DynamoDB](../2.2-create-dynam/)