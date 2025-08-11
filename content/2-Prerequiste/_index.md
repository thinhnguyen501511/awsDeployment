---
title : "Preparation"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2. </b> "
---
To deploy a real-time data processing system using DynamoDB Triggers and AWS Lambda, you need to perform several essential preparation steps to ensure the proper permissions and environment setup on AWS.  
In this preparation phase, we will create an IAM Role to grant AWS Lambda the necessary permissions to access services such as DynamoDB, CloudWatch Logs, and other services that support data processing, storage, and monitoring.  
After configuring the IAM Role, we will proceed to create a DynamoDB table and set up a streaming trigger with AWS Lambda.

### Contents
  - [Create IAM Role](2.1-create-iam-role/)
  - [Create DynamoDB Table and Enable DynamoDB Stream](2.2-create-dynamo/)
  - [Create Lambda and Attach to DynamoDB Stream](2.3-create-lambda/)
