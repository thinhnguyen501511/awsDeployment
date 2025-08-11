---
  title : "Logging Errors with CloudWatch"
  date : "`r Sys.Date()`"
  weight : 2
  chapter : false
  pre : " <b> 4.2. </b> "
---

When the system encounters an error, recording detailed information about it is a crucial step for root cause analysis and troubleshooting.  
AWS CloudWatch is the default logging and monitoring service for Lambda, allowing you to easily track the entire processing flow, including when errors occur.

#### How to Log Errors

In your Lambda source code, you can use:

+ `console.error()` to log errors.  
+ `console.warn()` to log warnings.  
+ `console.log()` for general information.

**Example:**
```
try {
  // Data processing logic
} catch (error) {
  console.error("❌ Error processing record:", error);
  console.error("📄 Stack trace:", error.stack);
}
```
**Viewing logs in CloudWatch**

1. Open AWS Management Console.

2. Go to CloudWatch → Log groups.

3. Find the log group by the Lambda function name, e.g. /aws/lambda/DynamoStreamProcessor.

4. Select the latest log stream to see detailed error information.

**Importance of logging errors**

+ Quickly identify root causes: Determine if the error is caused by input data, service connection issues, or processing logic.

+ Track error frequency: See whether the error happens sporadically or repeatedly.

+ Enable automatic alerts: You can integrate with CloudWatch Alarms to send email/SMS notifications when the number of errors exceeds a threshold.