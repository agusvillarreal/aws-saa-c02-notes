## Caching Overview
Caching -> 

## CloudFront
Edge Location
CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally. It helps reduce latency and provide higher transfer speeds using AWS edge locations

- Security
- Global Distribution
- Endpoint Support
- Expiring Content

> Every sort of external customer perfomance issue can be solved

## Caching Your Data with ElastiCache and DAX
ElastiCache -> Is a managed version of 2 open-source technologies: Memcached and Redis. Neither of these tools are specific to AWS, but by using ElastiCache you avoid a lot of common issues you might encounter

| Memcached                        | Redis                              |
| -------------------------------- | ---------------------------------- |
| Simple database caching solution | Supported as a caching solution    |
| Not a databse by itself          | Functions as a standalone database |
| No failver or Multi-AZ support   | Failover and Multi-AZ support      |
| No backups                       | Supports backups                                   |

### DAX
Dynamo Accelerator

1. In-Memory Cache 
2. Location -> inside VPC
3. You're in control -> node size
DAX -> DynamnoDB
ElastiCache -> RDS, Redis, DB of its own
favor answers that include database caching solution

## Global accelerator
Global accelerator is a networking service that sends your use'rs traffic through AWS's global network infrastrcuture. It can increase perfomance and help deal with IP caching

1. Masks Complex Architecture
2. Speeds Things Up
3. Weighted Pools

IP caching -> Global Accelerator
