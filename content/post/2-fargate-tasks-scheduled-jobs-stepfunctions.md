---
title: "Running scheduled jobs using Fargate and Step Functions"
slug: "scheduled-jobs-fargate-stepfunctions"
date: 2023-10-22T11:30:11+02:00
draft: false
categories: ["aws", "devops", "fargate", "serverless", "stepfunctions"]
---

Running a scheduled job is easily done using Lambda and EventBridge. But what happens when your scheduled job is taking more than 15 minutes to complete? And what about monitoring and observability of the status of your scheduled task? ECS Fargate and Step Functions come to the rescue!

<!--more--> 