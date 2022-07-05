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
