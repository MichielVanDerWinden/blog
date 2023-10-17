---
title: "Golang in AWS Lambda: Optimize those slow starts"
slug: "golang-lambda-optimize-slow-start"
date: 2023-11-08T10:08:14+02:00
draft: false
categories: ["aws", "development", "golang", "serverless"]
---

Golang is an amazing programming language; it's easy to learn, great performance and out of the box it contains loads of quality of life improvements compared to other high-level languages. It's also a nice fit for AWS Lambda as it compiles all your code into a single binary and boots up really quickly. There's just one downside: dependency injection is done _automagically_ and this can very negatively impact your AWS Lambda boot times. Let's fix this!

<!--more--> 