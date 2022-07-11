## Horizontal vs Vertical Scaling Overview
Vertical scaling 
- Is it highly available?
- Which is appropiate for the situation: horizontal or vertical?
- Is it cost effective?
- Would switching databases fix the problem?


- **What do we scale?**
	We have to decide what sort of resource we're going to scale. How we define the template?
- **Where do we scale?**
	When applying the model, where does it go? Should we scale out database? Or Webservers?
- **When do we scale?**
	How do we know we need more? CloudWatch alarms can tell us when it's time to add more resources


## What are Launch Templates / Configurations?
A launch template specifies all of the needed settings that go into buildinf out an EC2 instance. It is a collection of settings that you can configure so you don't have to walk though the EC2 wizard over and over

| Templates                 | Configurations                |
| ------------------------- | ----------------------------- |
| More tha just autoscaling | Only for autoscaling          |
| Support versioning        | Immutable                     |
| More granularity          | Limited configuration options |
| AWS Recommended           | Don't use them                              |

> ### What makes a template?
> On the exam, it's critical to understand what goes into a Launch Template. You need to know that it includes the AMI, EC2-Instance size, security groups, and portentially networking information

Networking information -> we cannot use the launch template into an auto scaling group -> If we specify a VPC in the launch template, that launch template cannot be used in an auto scaling group becuase the auto scaling group has to specify the VPC
- Launch template
	- The most up to date and flexible way to create a template
- Launch configurations
	- The older version. It's not "wrong" to use them, but if possible use templates
- User-Data
	- User-data is included in the template or configuration
- Change
	- Can be versioned, configurations are immutable
- Networking
	- Configs don't include networking information. Templates could

## Scaling EC2 instances with Auto Scaling
An Auto Scaling group contains a collection of EC2 instances that are treated as a collective group for purposes of **scalling** and **management**

Spot instances with Auto Scaling groups

It's important to remember Auto Scaling is vital to creating a highly available application

Remembder to select answers that spread resources out over multiple Availability Zones and utilize load ballancers

- Networking
	Auto scaling groups will contain the location of where your instances will live
- Remember ELB
	It's vital to select a load balncer for the instances to live behind
- Limits
	Min, max, and desired are the 3 most important settings
- Notifications
	SNS can act as notification tool
- Balancing
	Auto Scaling will balance your EC2 instances across the Availability Zones


## Diving Deeper into Auto Scaling Policies
1. Warm Up
	1. Stops instances from being placed behind the load balancer, failing the health check, and being terminated
2. Cooldown
	1. Pauses Auto Scaling for a set amount of time Help to void runaway scaling events
3. Avoid Thrashing
	1. You want to create instances quickly and spin thme down slowly


- Scale Out Aggressively
	- Get ahead of the workload
- Scale in Conservatively
	- Once the instances are up, slowly roll them back when not needed
- Provisioning
	- Keep an eye on privisioning times. Bake those AMIs to minimize it
- Costs
	- Use EC2 RIs for minimum count of EC2 instances
- CloudWatch
	- Your no. 1 for alerting auto scaling that you need more or less of something 


## Scaling Relational Databases
### Scaling vs Refactoring
You'll be given scenarios and, unless otherwise specified, refactoring and changing to DynamoDB is a viable scaling choice
It won't work that easily in the real world, but in the exam, switching databse types can solve the problem

- Read replicas
	- Readf heavy workload = Read replicas
- Careful with storage
	- RDS storage only scales up it won't scale back down
- Vertical scaling 
	- Don't shy away from this scaling type
- Multi-AZ
	- Unless it's a dev environment, turn this on
- Aurora Everything
	- Whenever possible, use Aurora if the situation calls for a relational database


## Scaling non-relational databases
Keep cost in mind rather than performance when scaling DynamoDB
COST PERSPECTIVE
**Predictable workload?** Pick provisioned capacity
**Sporadic?** Pick on-demand

- Access Patterns
	- Know if it's predicatble or unpredictable
- Design Matterns
	- Avoid hot keys will also lead to better performance
- Switching 
	- You can switch, but only once per 24 hours per table 
- Cost
	- Keep cost in mind when considering which type of table to pick

- **Auto Scaling is only for EC2.** No other service can be scaled using auto scaling. Other services might have a built-in option, but they aren't included in Auto scaling groups
- **Get ahead of the workload**. Whenever possible, favor solutions that are predictive rather than reactive
- **Bake AMIs to reduce build times.** You can avoid long provisioning times by putting everything in an AMI. This is better than using user data whenever possible

- Spread out. Make sure you're spreading your auto scaling groups over mutliple Availability Zones
- Steady state groups allow you te create a situation where the failure of a legacy codebase or resource that can't be scaled can automatically recover from failure
- ELBs are essential. Make sure you enable health checks from load balancers - otherwise, instnaces won't be terminated and replaced when they fail health checks 
