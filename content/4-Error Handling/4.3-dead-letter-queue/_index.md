---
  title : "Using Dead Letter Queue (DLQ) to Store Failed Events"
  date : "`r Sys.Date()`"
  weight : 3
  chapter : false
  pre : " <b> 4.3. </b> "
---

In real-time data processing systems, when a Lambda function repeatedly encounters errors (e.g., invalid data or an unavailable destination service), improper handling could lead to lost data or a bottleneck in the entire processing flow.  
AWS provides **Dead Letter Queue (DLQ)** to store events that fail to be processed successfully, allowing you to analyze and reprocess them later.

### How it works

+ When Lambda fails to process an event after the maximum retry attempts, the event is sent to a DLQ (usually an SQS queue or an SNS topic).

+ DLQ separates failed events from the main processing stream, preventing them from affecting valid events.

### How to configure DLQ for Lambda
1. Open **AWS Lambda Console** → select the function you want to configure.

2. Go to the **Configuration** tab → **Asynchronous invocation**.

3. In the **Dead-letter queue** section, select:

    + A pre-created **SQS queue** or **SNS topic**.

4. Save the configuration.

### Example scenario
Suppose Lambda reads data from a DynamoDB Stream but encounters a record missing a required field:

+ Lambda retries according to the configuration.  
+ If it still fails, that record is sent to an **SQS DLQ**.  
+ You can create another Lambda to read from the DLQ to manually process the record or send alerts.

**Benefits of DLQ:**

+ **No data loss:** Every failed record is retained.  
+ **Easy reprocessing:** You can rerun the logic or fix the data.  
+ **Improved stability:** Prevents issues from spreading to other valid events.
