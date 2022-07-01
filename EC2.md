# EC2 
## Overview
Elastic compute Cloud
Secure, resizable, compute capacity in the cloud -> virtual servers in the cloud
Select the capacity you need right now
Grow and shrink when you need
Pay for what you use
Wait minutes, not months

- On-Demand -> Pay by the hour, or the second, depending on the type of instance you run
	1. Flexible
	2. Short term
	3. Testing the Water (developed or being tested)
- Reserved -> Reserved capacity for 1 or 3 years. Up to 72% discount on the hourly charge. Great if you have known, fixed requirements
	- Predictable usage
	- Specific capacity requirements
	- Pay up Front
	- Standard RIs
	- Convertible RIs
	- Scheduled RIs
- Spot -> Purchase unused capacity at a discount of up to 90% . Prices fluctuate with supply and demand. Great for applications with flexible start and end times
	- Application that have flexible start and end times
	- Application that are only feasible at very low compute prices
	- Users with an urgent need for large amounts of additional computing capacity
	- Image rendering
	- Genomic Sequencing
	- Algorithmic trading engines
- Dedicated -> A physical EC2 server dedicated for your use. Great if you have server-bound licenses to reuse or compliance requirements
	- Compliance: Regulatory requirements that may not support multi-tenant virtualization
	- Licensing: Great for licencisng that does not support mult-tenancy 
	- On-Demand
	- Reserved
Estimate the cost you will use -> pricing calculator

## AWS Command Line
you can interact with AWS with the command line
`aws <service>`
Least privilege -> Always give your users the **minimun amount** of access required to do their job
Use groups -> **Create IAM groups** and assign your users to groups. Group permissions are assigned using IAM policy documents. Your users will **automatically inherit** the permissions of the group

1. Secret access key: You will only see this once If you lose it, you can delete the access key ID and secret access key and regenerate them. You will need to run aws configure again.
2. Don't Share Key Pairs: Each developer should have their own access key ID and secret access key. Just like passwords, they should not be shared
3. Supoort Linux, Windows, MacOS: You can install the CLI on your Mac, Linux, or Windows PC. You can also use it on EC2 instances

## Using Roles
IAM role -> identity specific permission, a role is intended to be assumable by anyone who needs it
Are temporary. temporary security credentials
1. The Preferred Option -> Roles are preferred from a security perspective
2. Avoid Hard-Coding Your Credentials -> Roles allow you to provide access without the use of access key IDs and secret access keys
3. Policies -> Policies control a role's permissions
4. Updates -> You can update a policy attached to a role, and it will take immediate effect
5. Attaching and Detaching -> You can attach and detach roles to running EC2 instances without having to stop or terminate those instances
Roles > access keys

## Security Groups and Bootstrap Scripts
Linux -> SSH Port 22
Windows -> RDP Port 3389
WEB -> HTTP Port 80
WEB S -> HTTPS Port 443
Security group are virtual firewalls for your EC2 instance. By default, everything is blocked
**Bootstrap Scripts** -> A script that runs when the instace first runs. It passes user data to the EC2 instance and can be used to install applications (like web servers and databases), as well as do updates and more
```bash
#!/bin/bash
yum install httpd -y
#installs apache
yum service httpd start
#starts apache
```
Adding these tasks at boot time **adds to the amount of time it takes to boot the instance**. However, it allows you to **automate the installation** of applications
1. Change to security groups take effect immediately
2. You can have any number of EC2 instances within a security group
3. You can have multipe security groups attached to EC2 instances
4. All inbound traffic is blocked by default 
5. All outbound traffic is allowed

## EC2 Metadata and user data
Metada is simply data about your EC2 instance
Using the `curl` command, we can query metadata about our EC2 instance
> `curl http://169.254.169.245/latest/meta-data/local-ipv4`

> `curl http://169.254.169.245/latest/meta-data/local-ipv4` > myIP.txt

Technically, this is within an internal private address range. This means it is not a valid external address (you could not assign this address to an interface card to actually communicate with). The Internet Assigned Numbers Authority (IANA) has reserved 169.254.0.0-169.254.255.255 for Automatic Private IP Addressing. This is much like an interfaces loopback address (127.0.0.1).

For this reason, there is no conflict in having this ip address assigned to multiple instances at the same time. Conversely, as a trick exam question, if you wanted to check the user data for an instance from your work computer, you could NOT simply put this address into a web browser. As I just said above, it's an internal address only. This means you would have to ssh into this instance, and then from within that ssh connection you could curl this internal address to receive user data metadata. This is another concept that messes many people up

- User data is simply bootstrap scripts
- Metadata is data about your EC2 instances
- You can use bootstrap scripts (user data) to access metadata
User data or bootstrap scripts to access meta data

By default, user data is only run one time and will not automatically be updated when you restart an instance.

## Networking with EC2
Enhanced networking:
**Elastic Network Adapter** (ENA) -> Supports network speeds of up to 100 Gbps for supported instance types
Intel 82599 Virtual Function (VF) Interface -> Supports network speeds of up to 10 Gbps for supported instance types. Typically used on older instances

### For different scenarios on the exam, choose the correct networking device
1. ENI
	- For basic networking. Perhaps you need a separate management network from your production network or a separate logging network, and you need to do this at low cost. In this scenario, use multiple ENIs for each network, ec2 instance
2. Enhanced networking
	- For when you need speeds between 10 Gbps and 100 Gbps. Anywhere you need reliable, high throuhgput
3. EFA
	- For when you need to accelerate High Performance Computing (HPC) and machine learning applications or if you need to do an OS-bypass. If you see a scenario question mentioning HPC or ML and asking what network adapter you want, choose EFA 

## Optimizing with EC2 placement groups
- Cluster Placement Groups: Low network latency, high network throughput
- Spread Placement Groups: Individual critical EC2 instances (dedicated hardware)
- Partition Placement Groups: Multiple EC2 instances; HDFS, HBase, and Cassandra
- A **cluster placement group** can't span multiple Availability Zones, whereas a spread placement group and partition placement group can
- Only **certain types of instances** can be launched iin a placement group (compute optimized, GPU, memory optimized, storage optimized)
- **AWS recommends homogenous instances** within cluster placement groups
- **You can't merge placement groups**
- You can **move an existing instances into a placement group**. Before you move the instance, the instance must be in the stopped state. You can move or remove an instance using the AWS CLI or a AWS SDK, but you can't do it via the console yet

## Solving Licensing Issues with Dedicated Hosts
Special licensing requirements
An **Amazon EC2 Dedicated Host** is a **physical server** with EC2 instance capacity fully dedicated to your use. Dedicated Hosts allow you to **use your existing** per-socket, per-core, or per-VM software **licenses**, including Windows Server, Microsoft SQL Server, and SUSE Linux Enterprise Server

## Timing Workloads with Spot Instances and Spot Fleets
Unused capacity, 90% discount 
Scenarios -> stateless, fault-tolerant or flexible applications -> Big data, containerized workloads, CI/CD, high-performance computing (HPC), and other test and development workloads
High performance computing
- Spot instances sae up to 90% of the cost of On-Demand instances
- Useful for any type of computing where you don't need persistent storage
- You can block Spot Instances from terminating by using a Spot block
- A spot Fleet is a collection of Spot Instances and (optionally) On-Demand instances
