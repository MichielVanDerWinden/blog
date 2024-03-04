---
title: "Golang: Optimizing AWS Lambda cold starts"
slug: "golang-lambda-optimize-slow-start"
date: 2024-03-04T08:12:13+02:00
draft: false
categories: ["aws", "development", "golang", "serverless"]
---

Golang is an amazing programming language; it's easy to learn, has great performance and out of the box it contains loads of quality of life improvements compared to other high-level languages. It's also a nice fit for AWS Lambda as it compiles all your code into a single binary and boots up really quickly. There's just one downside: dependency injection is done _automagically_ and this can very negatively impact your AWS Lambda boot times. Let's see what we can do!

<!--more--> 

## The issue
When I started working with Golang in AWS Lambda, I quickly ran into some latency issues regarding cold starts. Each of my Lambda invocations would take several seconds before responding, but each time it would only be during the very first run of a new Lambda instance. As I've been working with Lambda for years now, I quickly looked into everything my Lamdba was loading in during initialization. This is when I realised that Golang has a couple of "hidden features" that I didn't pick up on, one of which is how it handles initialization of all your (external) libraries and code.

By default, Golang will run the `init()` block of each and every one of your imported resources. This means that, starting at the top (our `main()` function in the AWS Lambda), it'll go through each of the imported resources, and run `init()`. But each of those resources also imports other resources, resulting in a cascade of `init()` calls. As long as you're only initializing some variables, it'll be just fine - the compiler will probably work some magic to make sure it does as little as necessary for the program to still run. But when you're working with (external) services that, among others, require setting up connections, calling out to AWS' secrets manager and running short (but still tangeable) setup processes, it can quickly result in slowly starting applications that'll only get up to steam when everything's cached properly.

Knowing what the issue was, I started looking into solutions I'd known from my days of Java development (mostly using [Spring Boot](https://spring.io/projects/spring-boot) which I still love as a framework to this day). I'd been search for ways of doing [dependency injection](https://en.wikipedia.org/wiki/Dependency_injection) and initializing my code more optimally, slowly coming to the conclusion that Golang works because they're only providing you with the bare bones of a programming language whilst giving you the option of adding bells and whistles yourself. This made me rethink my approach, decide to create a working example and write this blog post to give my two cents about how to approach this issue in the most simple way I could think of.

## Working example
Whilst reading through this blog post, I'd like to recommend cloning my working example repository for yourself and seeing what kind of difference the approach can make. [The example can be found here](https://github.com/MichielVanDerWinden/golang-lambda-cold-boot-tests). If you've found something that doesn't work, shouldn't be there or is just plain wrong, please open an issue and let me know. I've been working with Golang on and off for the past 2 years but there's much to learn, still 😉

## Testing two approaches
I've created two different code sets that work in nearly the same way. My first code set will be called `default` whilst the other code set is called `optimized`. Don't fool yourself with the nomenclature; the optimized code set is far from it; all I've done is optimize for this one single issue. Still, it's an easy way to differentiate the two.

The main difference lies in how I handle the `init()` blocks of the utility classes that set up and invoke (external) libraries. My naive (`default`) approach puts all initialization in the `init()` block:
```go
// src/default/pkg/aws/dynamodb/dynamodb.go
func init() {
	config = aws_common.GetAwsConfiguration()
	time.Sleep(time.Second)
	sess, _ := aws_common.GetSession(config)
	dynamodbSvc = dynamodb.New(sess)
}
```

Whilst my optimized solution only gets the general configuration object in its `init()` block and moves the initialization to a `getService()` method:
```go
// src/optimized/pkg/aws/dynamodb/dynamodb.go
func init() {
	config = aws_common.GetAwsConfiguration()
}

func getService() (*dynamodb.DynamoDB, error) {
	if dynamodbSvc == nil {
		time.Sleep(time.Second)
		sess, err := aws_common.GetSession(config)
		if err != nil {
			return nil, err
		}
		dynamodbSvc = dynamodb.New(sess)
	}
	return dynamodbSvc, nil
}
```
> Note: The `time.Sleep(time.Second)` clauses have been added to these code snippets to "emulate" a heavy initialization step - only using external AWS libraries and connections wasn't enough to create a tangible latency difference which was necessary to visualize the concept properly.

The `default` solution initializes all code paths automatically through the import statements made in the `src/default/main.go` file, whilst the `optimized` solution initializes the heavier parts of the code only when it is actually being hit by an invocation. This minor difference in approaches automatically should result in cutting down on Lambda cold start latency in code sets that have clear, distinct code paths that are to be taken for different inputs.

## Test results
Part of having a hypothesis means you'll also have to test to see if you're correct. If you've cloned my working example and have it up and running for yourself in AWS you've probably already tested both code sets as well. I found that the results spoke for themselves:

- Cold boot `src/default`:
    - Min: 4.15s
    - Avg: 4.21s
    - Max: 4.25s

- Cold boot `src/optimized`:
    - Min: 2.08s
    - Avg: 2.12s
    - Max: 2.22s

On average, I found a 2 second difference in my simple use case with three distinct code paths. Seeing as Lambda is heavily focusing on being used for automating tasks and giving you the freedom of putting more than one use case in a single Lambda, this can impact workflows quite heavily in the long run. For now, I'm happy to see that my changes have made a tangible effect and it's something I'll keep in mind in any future (personal) projects.

## Conclusion
I think it's always fun to see what kind of impact you can make on (your own) code with minor tweaks and taking a second look at things you've never really given much thought previously. I've felt kind of spoiled never having had these kinds of issues until working with a language as Golang - when working in Java I've always just opted for lazy initialization of my dependencies and it worked out of the box. Golang, in contrast, doesn't give you any opinionated solutions and instead hands you the reins to make it your own; something I really like and made me enjoy working with it even more lately.