On the exam, avoid answers that include tight coupling - such as an EC2 instance that is directly communicating to another EC2 instance
While tight coupling is simpler from an architecture perspective, it doesn't offer any meaningful benefits over loose coupling

- Always loosely couple
	- Even when not specifically asked, loose coupling is the answer
- Never tightly couple
	- Don't select answers that include instance-to-instance communication
- Internal and External
	- Every level of an application should be loosely coupled
- One Size
	- Doesn't fit all

## Messaging with SQS
Simple Queue Service is a messaging queue that allows asynchronous processing of work. One resource will write a message to an SQS queue, and then another resource will retrieve that message from SQS
**long poling** 
short poling 

#### SQS Settings
1. Delivery Delay
	Default is 0; can be set up to 15 minutes
2. Message Size
	Messages can be up to 256 KB of text in any format
3. Encyption
	Messages are encrypted in transit by default, but you can add at-rest 
4. Message Retention
	Default is 4 days; can be set between 1 minute and 14 days
5. Long vs Short
	Long polling isn't the default, but it should be
6. Queue Depth 
	This can be a trigger for autoscalling

- What does that do?
	- It's imperative that you know  what all the settings do
- Troubleshooting
	- You'll need to pinpoint the issues
- Size
	- Meesages are 256 KN of text in any format 
- Nothing last forever
	- Messages can only live up to 14 days max
- Polling
	- It's important to know the difference between long and short polling

## Sidelining Messages with Dead-Letter Queues 
### Dead-Letter Queues
If the scenario laid out mentions problems with a message in SQS, immediately think about DLQs and visibility timeout
It's important to set up a CloudWatch alarm to monitor queue depth
- Make sure you set up an alarm and alert on queue depth
- DLQs are just SQS queues that are set to recieve the reject messages
- Messages will be held up to 14 days 
- You can create SQS DLQ for SNS topics

## Ordered Messages witH SQS FIFO

| Standard                                 | FIFO                    |
| ---------------------------------------- | ----------------------- |
| Best effort ordering                     | Guaranteed orderint     |
| Duplicate messages                       | No message duplication  |
| Nearly unlimited transactions per second | 300 messages per second |

message ordering -> FIFO
- FIFO queues do not have the same level of performance
- You can order messages with SQS standard, but it's on you to do it
- This ensures messages are processed obe by one 
- It cost more since AWS must spend compute power to deduplicate messages

## Delivering Messages with SNS
SNS is a **push-based messasing** service. It will proactively deliver messags to the endpoints subscribed to it. This can be used to alert a system or a person

#### SNS Settings
- Subscribers
	- Kinesis Data Firehose, SQS, Lambda, email, HTTP, SMS, platform application endpoint
- Message Size
	- 256 KB text
- DLQ Support
	- Messages that fail to be delivered can be stored in an SQS DLQ
- FIFO or Standard
- Encyption
- Access Policy

Anytime you see a need for someone to know an AWS event happened, SNS will be the service to deliver that notification
- Push
	- Anytime you see this word, think SNS
- CloudWatch
	- SNS and CloudWatch are best friends and the easiest way to alert you that something happened
- Where does it go?
	- You'll need to know all the subscriber optioms
- No Do-Overs
	- SNS will only retry HTTP(S) endpoints, but nothing else

## Fronting Applications with API Gateway
API Gateway -> is a fully managed service that allows you to easily publish, create, maintain, monitor, and secure your API. It allows you to put a safe "front door" on your application

> APIs Arte the front door
> API Gateway is a secure and safe front door for yout application
> It is preferred method to get API calls into your application and AWS environment
> You should favor answers that include API Gateway over those that hardcode access and secret keys

- API
	- Anytime the exam talks about creating or managing an API, think API Gateway
- DDoS
	- You can front API Gateway with a web application firewall (WAF)
- Versioning
	- API Gateway supports versioning of your API
- No baking
	- Using API Gateway stops you from baking credentials into your code


1. Is it a synchronous (ELB) or asynchronous (SQS) workload?  
2. What type of decoupling makes sense?
3. Does the order of messages matter?
4. What type of application load will you see?

- SQS can duplicate messages. This only once in a while, so if it's happening consistently check for a misoconfigured visibility timeout, or the developer is failing to make the delete API call
- Queues aren't bidirectional. If tou need communication to return to the instance that sent the message, you'll need a second queue
- Know the defaults. It's important to understand the standard values for all the SQS settings
- Nothing lasts forever. Messages stored in SQS can only persis up to 14 days
- Does order matter? If message ordering is important, make sure to select SQS FIFO
- Proactive notifications = SNS. Anytime a question asks email, text, or any type of push-based notification, think SNS
- CloudWatch love SNS. Scenearios that talk about getting about a notification from a CloudWatch alarm should immediately male you look for SNS in the answer
- API Gateway doesn't require an in-depth understanding. You only need to know it acts as a secure front door to external communication coming into your evironment

https://docs.aws.amazon.com/wellarchitected/latest/high-performance-computing-lens/loosely-coupled-scenarios.html
