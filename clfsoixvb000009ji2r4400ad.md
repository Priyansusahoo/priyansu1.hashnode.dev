---
title: "AWS Lambda: Getting started with Serverless Computing"
datePublished: Tue Mar 28 2023 19:57:08 GMT+0000 (Coordinated Universal Time)
cuid: clfsoixvb000009ji2r4400ad
slug: aws-lambda-getting-started-with-serverless-computing
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1680032201763/0c42de0b-3e05-41bd-96c9-a78010cc24c0.png
tags: aws, serverless, aws-lambda, learning-in-public, wemakedevs

---

### Introduction

Before we get started with AWS Lambda and how it works. Let's look into how applications are currently deployed.

**Deploying an Application:** So, as a developer, after you write your code you are going to have to deploy your application. So you're going to have to either get a physical server in a data center or you can make use of AWS EC2. So that you can create a virtual machine but either way you're going to need some sort of server to run your application. And you have to install some operating system like Linux or another OS and then you're going to have to perform a couple of different things. You're going to have to install all of the necessary dependencies, packages, and libraries that your application will actually need to run, you have to secure your server, so it's going to be things like setting up the firewall and then you're gonna have to get your code copied over and up and running on the server.

So, now at this point you finally got your code running on the server but your code running on a server but you're not quite done yet. Over time you're going to have to perform routine upgrades on your server so that they are running the latest & supported versions and on top of that, you're going to have to perform fixes and patches for various vulnerabilities that pop up.

And in addition to that, you also need the infrastructure that's running your code to be dynamic and what it means is with an increase in traffic you need to automatically scale up and not manually spin up new instances. And as traffic reduces you need to dynamically reduce the number of instances you're running. So you don't have to pay for extra resources you may not be using.

***Now, as a developer is this something you need to worry about?***

No, of course not, as a developer the only thing you care about is writing code.

***So, What are your options?***

If you don't want to perform any of these tasks you can obviously outsource these tasks to either the Infrastructure team or Ops team that actually hands and manages all of the underlying infrastructure so that you can focus on running code but you have to keep in mind that's also going to cost a lot of money.

Now, wouldn't it be easier if as a developer all you need to do was just take your code and then just upload it to AWS, and AWS would handle the rest? And this would be an ideal scenario and that's why ***AWS lambda*** was created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680016257704/2a37a543-e0ec-4c5f-96bc-9ae77b33582d.png align="center")

It was really so that you as a developer the only thing you have to worry about is writing code and once you're done you just upload it to AWS and AWS handles the rest.

### What is AWS Lambda?

* AWS Lambda is a "serverless" computing service that lets you run code without provisioning or managing servers.
    
* AWS manages the server maintenance, scaling, capacity provisioning, and logging.
    

### Serverless?

**Does serverless mean there are no servers?**

**No**, to run an application there will always need to be a server.

But what it really means is that let's say that you upload your code to AWS and AWS stores the code someplace in an S3 bucket.

What really is happening under the hood is that AWS has this lambda service reserve pool. So, it's nothing more than just a whole bunch of servers just sitting in a pool waiting to be used and so when a certain event occurs and his event can be anything, it's an event that's going to cause your code to run.

What happens is, AWS Lambda will actually pull a couple of these servers from the reserve pool it will take your lambda function and it will deploy it onto those servers, and then it will take the event or the request and send that out to the server so that they can then run the code and eventually those ec2 instances get returned back to the reserve pool.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680018400800/c9539d75-6a0b-44db-a688-b4cbeab64c39.png align="center")

What I want to highlight here is that there's always a server running the code but the thing is you as the customer don't touch any server, you don't have to log into any server, and you don't have to run any commands. You upload the code ad AWS handles the underlying servers. So from your perspective, you don't see any servers and so that's why it's called serverless.

### AWS Lambda Use Cases

1. **Used in file processing**:
    
    Example: Let's say that we upload an image or video to an S3 bucket we could set up a lambda function to automatically run every time a file is uploaded and perform some sort of operation like resizing an image or converting a video from one format to another.
    
    *Diagram:*
    
    *(Resizing an image)*
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680020720729/3533a3a2-0ce1-4d16-bcd1-2935e4f1f13a.png align="center")
    
2. **Stream Processing with lambda functions.**
    
3. **Design web Applications using Lambda functions.**
    
4. **Design mobile / Web backends using Lambda functions.**
    
5. **Also, building an entire API using lambda function.**
    

### Lambda Concepts

1. **Lambda Function**: The *lambda function* is just the code that you want to run and it's called a lambda function because it actually is nothing more than a function in your specific programming language. Example of a Lambda function written in javascript:
    
    ```javascript
    exports.handler = async funtion
    (event, context){
        console.log("EVENT: \n" + 
    JSON.stringify(event, null, 2));
        return context.logStreamName;
    };
    ```
    
2. **Trigger:** So a trigger is responsible for determining when your code runs. So you provide AWS with your code but then you have to tell AWS when you want the code to run and so there are a lot of different triggers that you can use.
    
    * One is you can set up a trigger so that every time a file gets uploaded to S3 your code will run.
        
    * You can set up a trigger so that anytime there's a request to an API gateway your code will run.
        
    * You can set up a trigger so that anytime there's an update to a database like dynomoDB then your lambda function will run.
        
        So there's a wide variety of triggers available on AWS.
        
3. **Events:** An event is just information about triggers. So when a trigger happens and let's say we've set up a trigger to upload files in s3 we're going to have to provide our function with some information about the trigger or the event that caused the trigger and so if it's uploading of a file to s3 we're going to have to give information like what was the name of the file that was uploaded. So our function can have that information and perform some operations. In this event which once again is nothing more than the information about the trigger which is going to be passed into our function as a parameter and so now you have access to that event and all the different properties in your code and then you can perform the necessary operation.
    

### Benefits of Lambda

1. **There are "No Servers to manage":**
    
    * And so you have no need for an infrastructure team in this case because all you'll ever have to do is just upload your code to the AWS lambda page.
        
    * And you'll never have to worry about upgrading or maintaining or patching your servers because once again AWS manages all of that. So they're doing this on their end.
        
2. **Auto Scaling to handle traffic spikes:**
    
    * So Lambda scales up automatically for you so you don't have to configure anything out of the box and so if you need more servers during high traffic times, Lambda will have these functions that can run on any number of servers and you can scale a limitless amount of resources. And on top of that, if you find that traffic starts to reduce you don't ever have to worry about servers just sitting there doing nothing, Lambda will essentially scale back down.
        
3. **Pay for what you use:**
    
    * So the great part about lambda is that you pay for what you use. You pay per invocation which means every time your code runs you pay a price.
        
    * And by doing like that you don't ever have to worry about the extra costs that you might pay for servers during low-traffic hours. Because if your code is not running you're not getting charged.
        

### Drawbacks of Lambda

1. **Cold Start:** The serverless architecture executes functions on temporarily created containers. Let’s consider a simple function such as a client registering their details. As soon as the client submits his or her information to the Lambda function, AWS will create a temporary container, deploy all the dependencies involved, and run the required code. Once the request is completed, the container is destroyed. Now, if there is another request after some time, the same process would be followed.
    
    The drawback lies in the time taken by Lambda to create this temporary container. This is usually between 100 milliseconds to 2 minutes and is known as a cold start. However, there is a workaround that we recently implemented in our application. All you need to do is ping your Lambda every 5 minutes to make sure the container is not destroyed. This way only the first request will take some time to process, all the subsequent ones would be processed much faster without any delay.
    
2. **Computational Restrictions:** The functions which require a lot of processing cannot be handled by AWS Lambda. However, there is a workaround here as well. You can create a queuing process to break up your work into a series of smaller functions and execute them simultaneously using AWS Lambda.
    
3. **Issues with working in a Virtual Private Cloud:** Many clients use a Virtual Private Cloud (VPC) for an extra layer of security. Using Lambda with any such function can entail some additional delay over and above the cold start mentioned above. This too can be dealt with using a warm start.
    

Summing up, there are a lot of cases AWS Lambda functions would thrive in. Lambda is especially effective in tasks that are self-contained and run for a short period such as processing operations (i.e. formatting an image), the functions that are used to support static websites (for example if you want to capture emails), automation tasks where an entire server is not required at all times (for example data backups).

If you guys have any suggestions, feel free to connect with me:

* **priyansusahoo1@gmail.com /** [**Twitter**](https://twitter.com/Priyansu2000) **/** [**Linkedln**](https://www.linkedin.com/in/priyansu1/)