## VPC Overview
VPC virtual center in the cloud
Default  VPC
Logically isolated part of AWS cloud

### What can we do with a VPC
- Launch Instances
	- Launch instances into a subnet of your choosing
- Custom IP Addresses
	- Assign custom IP address ranges in each subnet
- Route Table
	- Configure route tbaels between subnets
- Internet Gateway
	- Create internet gateway and attach it to our VPC
- More Control 
	- Much better security control over your AWS resources
- Access Control List
	- Subnet network access control list

Consists of internet gateways (or virtual private gateways) route tables, network access control lists, subnets, and security groups
1 subnet is always in 1 availability zone


## NAT Gateway
You can use a network address translation (NAT) gateway to enable instances in a private subnet to connect to the internet or other AWS services while preventing the internet from initiating a connection witht those instances
- Redudant inside the Availability Zone
- Starts at 5 Gbps and scales currently to 45 Gbps
- No need to patch
- Not asscociated with security groups
- Automatically assigned a public IP address


High Availability with NAT Gateway
If you have resources in multiple Availability zones and they share a NAT gateway, in the event the NAT gateway's Availability Zone is down, resources in the other Availability Zones lose internet access

## Protecting Your Resources with Security Groups
Security groups are stateful - if you send a request from youfr instance, the response traffic for that request is allowed to flow in regardless of inbound security group rules 
> Responses to allowed inbound traffic are allowed to flow out, regardless of outbound rules

## Controlling Subnet Traffic with Newtwork ACLs
A network access control list (ACL) is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets
- **Default Network ACLs:** Your VPC automatically comes with a default network ACL, and by default it allows alll outbound and inbound traffic
- **Custom Network ACLs**: You can create custom netkork ACLs. By default, each custom newtwork ACL denies all inbound and outbound traffic until you add rules
- **Subnet associations**: Each subnet in your VPC must be associated with a network ACL. If you don't explicity associate a subnet with a network ACL, the subnet is automatically associated with the default network ACL
- **Block IP Addresses:** Block IP address using network ACLs, not security groups

- You can associate a network ACL with multiple subnets; however, a subnet can be associated with **only 1 network ACL** at a time. When you associate a network ACL with a subnet, the previous association is removed
- Network ACLs contain a **numbered list of rules** that are evaluated in order, starting with the **lowest** numbered rule
- Network ACLs have **separate** inbound and outbound rules, and each rule can either **allow or deny traffic**
- Network ACLs are **stateless**; responses to allowed inbound traffic are subject to the rules for outbound traffic (and vice versa)

## Private Communication Using VPC endpoints
VPC Endpoints -> provately connect to your VPC to supported AWS services
**Endpoints Are virtual devices**
They are horizontally scaled, redudant, and highly available VPC components that allow communication between instances in your VPC and services _without imposing availability risks or bandwidth constraints on your network traffic_

- Use case: When you want to connect AWS services without leaving the Amazzon internal network
- 2 types of VPC Endpoints: Interface endpoints and gateway endpoints
- Gateway Endpoints: Support S3 and DynamoDB

## Building Solutions across VPCs with Peering
VPC Peering -> Allows you to connect 1 VPC with another via a direct network route using private IP addresses
- Instances behave as if they were on the same private network
- You can peer VPCs with other AWS accounts as well as with other VPCs in the same account
- Transitive peering is not supported. 
- This must always be in a hub-and-spoke model
- You can peer between regions
- No overlapping CIDR address ranges

## Network Privacy with AWS PrivateLink
If you see a question asking about peering VPCs to tens, hundreds, or thousands of customer VPCs, think of AWS PrivateLinks
Doesn't require VPC peering, no route tables, NAT gateways, internet gateways, etc.
RequIres a Network Load Balancer on the service VPC and an ENI on the customer VPC

## Securing Your Network with VPN CloudHub
If you have multiple sites, each with its own VPN connection, you can use AWS VPN CloudHub to connect those sites together. It's similar to VPC peering in that it works on a hub-and-spoke model
AWS VPN CloudHub is low cost and easy to manage. Though it operates over the public internet, all traffic between the customer gateway and the AWS VPN CloudHub is encrypted

## Connecting On-Premises with Direct Connect 
AWS Direct Connect is a cloud service solution that makes it easy to establish a dedicated network connection from your premises to AWS
- Direct Connect directly connects your data center to AWS
- Useful for high-throughput workloads (e.g., lots of network traffic)
- Helpful when you need a stable and reliable secure connection
- VPN dropping out, reduce newtwork cost, throughput

## Simplifying Networks with Transit Gateway
- You can use route tables to limit how VPCs talk to one another
- Works with Direct Connect as well as VPN connections
- Supports IP multicast
- Simplifying network Topology

