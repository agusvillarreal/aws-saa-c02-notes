#solutionsarchitech
## Why do we automate?
> Lazy is a good thing
> Whenever possible, select an answer that doesn't include manual steps
> 
> AWS love to give you scenarios that allow you to replace a manual step with automated tools, so make sure what you're selecting automates the entire process and not just a portion of it

- Automate Everything
	- On the exam, automaion is always bettr than manual work
- Tools
	- You'll needto know the right tool for the job
- Benefits
	- Know that is more reliable and faster
- Immutable
	- Allows you to easily create and destroy your achitecture as needed

## CloudFormation
```yaml
AWSTemplateFormatVersion: 2010-09-09
Resources:
	InternetGateway:
		Type: 'AWS::EC2::InternetGateway'
		Properties:
			Tags:
				- Key: Application
				  Value: !Ref 'AWS::StackName'
				- Key: Network
				  Value: Public
	GatewayToInternet:
		Type: 'AWS::EC2:.VPCGatewayAttachment'
		Properties:
			VpcId: !Ref VPC
			InternetGatewayId: !Ref InternetGateway
```

1. WRITE CODE:
	1. CloudFormation is a declarative programming language. It supports either JSON or YAML formatting
2. DEPLOY YOUR TEMPLATE
	1. When you upload your template, CloudFormation will go through the process of making the needed AWS API calls on your behalf

> CloudFormation is perfect for creating immutable architecture

When you create resources using CloudFormation, you can easily pick that templrate up and run it anywhere you want -> Consistency

- Basics
	- You'll need to know the layout of a CloudFormation template and what the sections do
- Cross-region
	- Hard-coded values and resource IDs can be the reason templates fail to create
- Troubleshooting
	- If it finds an error, CloudFormation rolls back to the last known good state
- It's just API calls
	- CloudFormation makes the same API calls you make manually
- Immutable
	- CloudFormation can easily create and destroy your entire architecture

## Elastic Beanstalk
> Scenearios on the exam that are looking for simple one-stop solutions would benefit from elastic Beanstalk

The approach of bring your code and that's it means you have to do very little work to spin something up

- PaaS
	- Beanstalk handles it all There's very little you need to do
- Platform Types
	- Supports containers, Windows, and Linux applications. You don't have to memorize them all
- Hand Holding
	- It's great solution to start with, but in general it's only for simpler web applications
- Traditional
	- It's not serverless. Beanstalk its creating and managing standard EC2 architecture

## Systems Manager
Systems manager is a suite of tools designed to let you view, control, and automate both your AWS architecture and on-premises resources

- Automation Documents
- Run command
- Patch manager
- Parameter Store
- Hybrid Activations
- Session manager

> Systems manager will rarely be called out by name. Instead, the names of the features will be used

For example, using Automation documents to fix S3 bucket permissions or using Session Manager to connect to an instance

- On-Site Support
	- Systems Manager can manage both on-premises and cloud architecture
- Overview Required
	- Generally, knowing it can patch, update, and configure instances is good enough
- Unpaid SysAdmin
	- If an admin can do it, System Manager can as well
- Automation Documents
	- These are usable by AWS Config to enforce architecture state

1. Can you automate?
2. What kind of automation works in this scenario?
3. Is the automation repeatable?
4. How would this work cross-region or cross-account?

**parameters, mapping and resource**
stateless environmet, immutable architecture
never hard-coded IDs
Mappings and Parameter Store


simple solution to bundle and deploy application -> Elastic Beanstalk

Automation documents -> primary method EC2 instance
