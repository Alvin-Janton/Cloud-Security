
# Build a Security Monitoring System

---

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-monitoring_reghtjy)

---

## Introducing Today's Project!

In this project, I will create a secrets monitoring system to check for any potential intrusions into my account and alert me if it finds anything. To do this project I'm going to use a combination of tools consisting of, AWS S3, SecrestManager, CloudWatch, CloudTrail, CLI, and SNS

### Tools and concepts

Services I used were SecretsManager, CloudTrail, CloudWatch, and SNS. Key concepts I learnt include how to monitor logs using CloudTrail and CloudWatch, how to create metrics using CloudWatch, how to create alarms and send notifications using CloudWatch alarms, and SNS.

### Project reflection

This project took me approximately two hours to do. The most challenging part was configuring the CloudWatch metric. It was most rewarding to see the successful notifications sent to my email.

---

## Create a Secret

Secrets Manager is a service that securely stores sensitive information, such as login credentials, API keys, security tokens, or database passwords. 

To set up for my project, I created a secret called "TopSecretInfo" that contains a key and value that I created to act as sensitive data.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-monitoring_o5p6q7r8)

---

## Set Up CloudTrail

CloudTrail is a security monitoring service that tracks activity on your account, including the actions taken and who accessed specific resources. I set up CloudTrail to monitor my secret and output the logs into an S3 bucket.

CloudTrail events include types like management events, admin actions like creating or deleting resources. Data events, the operations conducted by resources like S3 or Lambda. Insight events, unusual actions taken in the environment. Network events, track network activity.

### Read vs Write Activity

Read API activity involves simply looking at the secret, but not changing or viewing it. Write API activity involves changes made to the secret or any API calls to view that data. For this project, we need both "Read" and "Write" to properly monitor my resource.

---

## Verifying CloudTrail

I retrieved the secret in two ways: First, by going to SecretsManager and using the interface to reveal it. Second, using the AWS CloudShell CLI and running a command to see the secret.

To analyze my CloudTrail events, I visited the CloudTrail event logs and searched for "Event source", "secretsmanager.amazonaws.com". I found my three attempts to access the secret at the top of the list. This tells me that CloudTrails is successfully logging my actions.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-monitoring_s8t9u0v1)

---

## CloudWatch Metrics

CloudWatch Logs is a service that logs data from a variety of resources across the AWS environment. It's important for monitoring because it can alert you to intrusions, bugs, or crashes by setting up automatic alerts in case of an event.

CloudTrail's Event History is useful for logging and finding logs on one specific event or resource quickly. CloudWatch logs are better for finding data about events across the entire AWS environment.

A CloudWatch metric is a program that will take an action when its event case is triggered. When setting up a metric, the metric value represents the amount that the metric will increase in count if it is triggered. The default value is used when the metric is not triggered.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-monitoring_a9b0c1d2)

---

## CloudWatch Alarm

A CloudWatch alarm is a system that you set the baseline for activity in your environment, either through static or anomaly-based detection. I set my CloudWatch alarm threshold to greater/equal to 1, so the alarm will trigger when someone accesses my secret.

I created an SNS topic along the way. An SNS topic is a simple notification service that is used to send messages to people through email or text messages. My SNS topic is set up to send a notification to my email whenever the threshold limit is triggered.

AWS requires email confirmation because they want to make sure their sending messages to the correct email. This helps prevent confusion resulting from typos.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-monitoring_fsdghstt)

---

## Troubleshooting Notification Errors

To test my monitoring system, I exposed my secret value and waited for an alert message from CloudWatch. The results were that I got no message from CloudWatch, which indicates that my alert wasn't configured properly.

When troubleshooting the notification issues, I first checked to see if CloudTrail was logging events properly. Next, I checked to make sure CloudTrail was sending logs to CloudWatch. Third, I checked that the metric filter was properly filtering events. Finally, I checked the CloudWatch metric configurations and saw that the statistic was set to Average and not Sum. \

I initially didn't receive an email before because my CloudWatch metric threshold was set to Average and not Sum. This meant that for my alert to be triggered, the threshold would have to be passed multiple times just for it to send one alarm. Setting it to Sum means that it would add every count of the secret being exposed.

---

## Success!

To validate that CloudWatch metrics were successfully sending alerts. I checked my CloudWatch alerts tab to see if the alert was in alarm mode. I received an email notification that my secret had been accessed.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-monitoring_ageraergearge)

---

## Comparing CloudWatch with CloudTrail Notifications

In a project extension, I updated my CloudTrail configurations to also send me SNS messages. I did this because I wanted to compare the alerts sent from CloudTrail and the alerts sent from CloudWatch to see what information is sent, how quickly, and the relevancy. 

After enabling CloudTrail SNS notifications, my inbox was flooded with notifications describing multiple actions that were taken in my environment. In terms of the usefulness of these emails, I thought they were irrelevant and difficult to understand.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-monitoring_d7e8f9g0)

---

---
