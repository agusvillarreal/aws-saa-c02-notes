## Serverless Overview
> Let's go Serverless
> On the exam, focus on answers that move away from unmanaged architecture like EC2
> It's almost always better to select an answer on the text that uses Lambda or containers rather than a traditional operating system

## Computing with Lambda
AWS Lambda is a serverless compute service that lets you run code without provisioning or managing the underlying servers. It's like you're running code without computers

1. Runtime: You'll need to pick from an available runtime or bring your own. This is the environment your code will run in
2. Permission: If your Lambda function needs to make an AWS API call, you'll need to attach a role 
3. Networking: You can (optinally) define the VPC, subnet, and security group your functions are a part of
4. Resources: Defining the amount of available memory will allocate how much CPU and RAM your code gets
5. Trigger: What's going to alert your Lambda function to start? Defining a trigger will kick Lambda off if that event occurs

> Lambdas is the answer 
> One ofthe most common ways you're going to see Lambda used is to add features to AWS

If you need to automatically remove entries from a security group, start and stop instances, or do anything else that isn't built in, the answer is most likely going to be use Lambda to achieve that
- Limitations
	- Know the limitations and general use cases for the service
- How does it start?
	- It's good to know the common triggers for lambda
- Microservices
	- Lambda excels in running small and lightweight functions
- Ecosystem
	- Lambdas plays a major role in the AWS ecosystem. It's easily integrated with many services
- Networking
	- Lambda can run inside or outside a VPC

## Container Overview
Container is a standard unit of software that packages up code and all its dependencies, so the aplication runs quickly and reliably from one computing environment to another

Dockerfile: Text document that contains all the commands or instructions taht will be used to build an image
Image: Immutable file taht contains the code, libraries, dependencies, and configuration files needed to run an application
Registry: Stores Docker images for distributrion. They can be both provate and public
Container: A running copy of the image that has been created

> Containers are more flexible
> On the exam, containers are generally seen as more flexible
> They're easier to run on-site and move around to different environments
> If you see a scenario that talks about any of these situations, pick an answer an answer that includes containers

- High level 
	- You won't have to dice into the specifics of a Dockerfile
- Ease of Use
	- Containers help you easily migrate from on-premise to AWS
- Dev vs Prod
	- Dev is prod, and prod is dev (but it's a good thing with containers)

## Running Containers in ECS or EKS
| ECS                                                                                                               | EKS |
| ----------------------------------------------------------------------------------------------------------------- | --- |
| Propietary AWS container management solution. Best used when you're all in on AWS an looking for something simple | Aws-managed version of open-soure Kubernetes container management solution. Best used when you're not all in on AWS. More work to configure and integrate with AWS     |

> ECS is preferred
> Ecs and containers go hand in hand on the exam. If you see a containers mentioned you should think ECS
> The only exception to this if the question is asking about open source, Kubernetes, or running the container on-premises. In this situation, you'd want to select

- Preference
	- Generally, favor using AWS-designed services over third party
- Open Source
	- Anytime you see open source or Kubernetes, think EKS
- High Level
- Length
	- Great for one-off or long-running applications

## Removing servers with Fargate
AWS Faragte is a serverless compute engine for containers that works with both Amazon Elastic Container Service (ECS) and Amazon Elastic Kubernetes service (EKS) 

| EC2                                     | Fargate                                       |
| --------------------------------------- | --------------------------------------------- |
| You are responsibnle for underlying     | No operating system access                    |
| EC2 pricing model                       | Pay based on resources allocated and time ran |
| **Long-running containers**                 | Short-running tasks                           |
| Multiple containers share the same host | Isolated environments                                              |

#### Fargate
- Select Fargate when you have more consistent workloads
- Allows Docker use across the organization and a greater level of control by developers
#### Lambda
- Great for unpredictable or incosistent workloads
- Perfect for applications that can be expreseed as a single function

more than you consume and the longer it takes the more you bill

> Know the Use Cases
> Your best friend in the exam is knowing when to use Lambda vs Fargate vs EC2
> It will serve you well to be able to walk through a quick use case of each one of those before you sit down to take the test

## Amazon EventBridge (CloudWatch Events)
Amazon EventBridge is a serverless event bus. It allows you to pass events from a source to an endpoint. Essentially, it's the glue that holds your serverless application together

CloudWatch Events (EventBridge) is a common trigger for Lambda

> EventBridge is the glue
> Don you want to trigger an action based on something that happened in AWS? EventBridge can do that for you
> EventBridge holds together a serverless application and Lambda functions. Any API call that happens in AWS can alert a Lambda function, or a variety of different endpoints, that something has happened

1. Is the application right for containers?
2. Do you need those servers?
3. 

