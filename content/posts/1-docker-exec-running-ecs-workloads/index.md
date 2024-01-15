---
title: "Using docker exec when running ECS workloads"
slug: "docker-exec-ecs-workloads"
date: 2024-01-07T10:54:34+02:00
draft: false
categories: ["aws", "devops", "docker", "serverless"]
---

Tasks running in ECS can sometimes run into issues that can't be fixed or debugged without direct access to the container as-is. To this end, AWS allows using `ecs exec` in the same manner as you would use `docker exec` locally. This works fine when running ECS on Fargate, but I've ran into trouble multiple times when using the EC2 backend. 

<!--more--> 

## Using ECS in the wild
I've been using ECS (especially Fargate) for containerized workloads for years now, and I've found it to be one of the simplest, most powerful services I've used to date. Whenever a customer wants to easily deploy, scale and manage a containerized workload they often think about kubernetes (and rightly so - kubernetes is great!) but after requesting some more information I often find that having the overhead and management tasks of a k8s cluster isn't the right fit from both a complexity and pricing standpoint.

With ECS I've been able to give most customers the same flexibility, usability and extensibility that a simple kubernetes cluster would've given them, without the complexity of managing the entire cluster. Some customers will eventually move on to a kubernetes cluster, but ECS gives us the base platform that maintains the workloads of the customer until they're ready for said journey.

## Issues happen, though
When running your tasks on ECS, you'll find that a lot of management is being done for you. This is great as it takes a lot of maintenance tasks off your hands; most updates are done in the background, scaling happens _automagically_ and your tasks can automatically access loads of AWS services if you've set up the permissions correctly. 

But, as all things _managed_ are bound to go, stuff *can* (and *will*) go wrong when you least expect it, leaving you unable to dig deeper into the running cluster, service or task itself. You'll have to dig through CloudWatch logs, your monitoring and observability tools and hope to find the information you need to fix your problem or give you a proper setup for testing the issue locally (or even better: on a production-like environment).

If after going through all your logs and monitoring, you've still not found the issue, AWS has got you covered. You're actually able to access your container using the `aws ecs exec` command. A simple example:

```bash
aws ecs execute-command
    --region ${AWS_REGION} 
    --cluster ${CLUSTER_NAME} 
    --task ${TASK_ID}
    --container ${CONTAINER_NAME}
    --command "sh" 
    --interactive
```

This command opens a shell to the given container, and allows you access to all files and executables available in the container whilst running.

## ECS with an EC2 backend
This worked flawlessly for our Fargate tasks, and most EC2 instances seem to play ball as well. But one of our tasks just didn't want to allow `ecs exec` - it kept throwing `TargetNotConnectedException` exceptions. I triple checked all our settings; IAM Execution Role, IAM Task Role, ECS Service setup - all seemed to be correctly set up for `ecs exec` to work, but it just... didn't.

In the end I logged into the EC2 instance, hoping to find anything out of the ordinary when a realization suddenly came to me - ECS EC2 instances run docker the same way you'd do on any other, ordinary EC2 instance. This meant I was able to log into the docker image using `docker exec` and found the issue within seconds. Sometimes the easiest solution is also the correct solution. Something to keep in mind for the future!