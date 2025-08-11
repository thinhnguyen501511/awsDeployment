---
  title : "Automatic Error Alerts with CloudWatch Alarm"
  date : "`r Sys.Date()`"
  weight : 4
  chapter : false
  pre : " <b> 4.4. </b> "
---

Logging errors or storing them in a DLQ is not enough if the operations team is not notified in time.  
To proactively detect incidents, AWS provides **CloudWatch Alarm** combined with **SNS** to send alerts via email, SMS, or chat systems like Slack.

### How it works
+ **CloudWatch Metrics** records the number of errors or failed Lambda executions.
+ **CloudWatch Alarm** monitors these metrics.
+ When a predefined threshold is exceeded, the Alarm triggers an action to send a notification via **SNS**.

### Steps to set up alerts

1. **Create an SNS Topic for notifications**
    + Open the **SNS Console** → *Create topic* → choose **Standard**.
    + Name the topic, create it, then **Create subscription** to register an email or SMS endpoint.
    + Confirm the subscription via the email received.

2. **Create a CloudWatch Alarm**
    + Open **CloudWatch Console** → *Alarms* → *Create alarm*.
    + Select **Lambda metrics** → *Errors* or *DeadLetterErrors*.
    + Set the threshold, e.g., more than 3 errors in 5 minutes.
    + In **Actions**, select the SNS Topic created earlier.

3. **Save and activate the alarm**

### Example scenario
+ If Lambda fails 5 consecutive times within 10 minutes, **CloudWatch Alarm** will immediately send an email to the operations team.
+ The team can then check logs or the DLQ to find and resolve the issue.

**Benefits:**
+ **Quick response:** Reduce the time to detect incidents.
+ **Lower risk of data loss:** Take early action when errors occur in bulk.
+ **Automated monitoring:** No need to manually check logs.
