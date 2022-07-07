## Route 53 Overview
DNS -> DNS is used to convert-human-friendly domain names into an Internet Protocol (IP) address
IPV4 and IPV6

#### Top-Level Domain
If we look at common domain names (e.g, google.com, bbc.co.uk, and acloud.guru), you will notice a string of characters separated by dots (periods)
The last word in a domain name represents the top-level domain. The second word in a domain name is known as a second-level domain name (this is optional, though, and depends on the domain name)

Start of Authorite
The SOA record stores information about:
- The name if teh server that supplied the data for the zone
- The administrator of the zone
- The current version of the data file
- The default number of seconds for the time-to-live on resource records

NS name server
Ns records are used by top-level domain servers to direct traffic to the content DNS server that contains the authoritative DNS records

### DNS RECORDS
#### A Record
An A (or address) record is the fundamental type of DNS record.
The A record is used by a computer to translate the name of the domain to an IP address

#### TTL
The length that a DNS record is cached on either the resolving server or the user's own local PC is equal to the value of the time to live (TTL) in seconds
The lower the time to live, the faster changes to DNS records take to propagate throughout the internet

#### CNAME
A CNAME (canonical name) can be used to resolve one domain name to another. For example, you may have a mobile website with the domain name http://m.acloud.guru that is used for when users browse to your domain name on their mobile devices

#### Alias record 
Alias recored are used to map resoruce record sets in your hosted zone to load balancers, CloudFront distributions, or S3 buckets that are configured as websites
Alias record work like a CNAME record in that you can map one DNS name to another _target_ DNS name
Mapping resources in AWS

| CNAME                                                     | A Record/Alias                                       |
| --------------------------------------------------------- | ---------------------------------------------------- |
| Cannot be used for naked domain names (zone apex record). | Can be used for a naked domain name zone apex record |

### 7 Routing Polices Available with Route 53
1. Simple Routing
2. Weighted Routing
3. Latency-Based Routing
4. Failover Routing
5. Geolocation Routing
6. Geoproximity Routing (Traffic Flow Only)
7. Multivalue Answer Routing


alias record vs cname -> alias record (AWS)
1. SOA Records
2. CNAME Records
3. NS Records
4. A records

## Simple Routing Policy
If you choose the simple routing policy, can only have **one record with multiple IP addresses**. If you specify **multiple value in a record**, Route 53 returns **all values** to the user in a **random order**

## Using a Weighted Routing Policy
The amount (percentage) traffic to specific Regions usign route 53

### Health checks
- You can health checks on individual record sets
- If a record set fails a health check, it will be removed from Route 53 until it **passes** the health check
- You can set SNS notification to alert you about failed health checks

## Failover Routing Policy
Failover routing policies are used when you want to create an **active/passive** set up
_Health check monitors the health of your end points_

In this example Route53 will send the traffic to AP-SOUTHEAST-2 because it has detected a failure in EU-WEST-2

## Geolocation Routing Policy
Lets you choose where your traffic will be sent based on based on the geographic location of your users 
Users in  different part of the world, and where do you want to send them
Location of your users, regulatory

## Geoproximity Routing Policy
You can use Route 53 traffic flow to build a routing system that uses a combination of:
- Geographic location
- Latency
- and availability to route traffic
from your users to your cloud or on-premises endpoint
Lets Amazon Route 53 route traffic to your resources based on the geographic location of your users and your resources
You can also optionally choose to route more traffic or less to a given resource by specifying a value, known as a bias. A bias expands or shrinks the size of the geographic region from which traffic is routed to a resource
Traffic flow

## Using a Latency Routing Policy
Lowest latency option

## Multivalue Answer Routing Policy 
return multiple values
any record, check health of each resource
