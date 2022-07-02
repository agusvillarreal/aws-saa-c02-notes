## Relational Database Service (RDS) Overview
RDS is generally used for onliune transaction processing (OTLP) workloads
| OLTP                                                                                                                       | OLAP                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Processes data from transactions in real time (e.g., customer orders, banking transactions, payments, and booking systems) | Processes complex queies to analyze historical data (e.g., analyzing net profit figures from the past 3 years and sales forecasting) |
| OLTP is all about data processing and completing large numbers of small transactions in real time                          | OLAP is all about data analysis using large amounts of data, as well as comlex queries that take a long time to complete             | 

OLTP -> RDS
OLAP -> Redshift
1. RDS Database Types
	-  SQL Server, Oracle, MySQL, PostgreSQL, MariaDB and Amazon Aurora
2. RDS Is for OLTP Workloads
	- Great for processing lots of small transactions, like customer orders, banking transactions, payments and booking systems
3. Not Suitable for OLAP Workloads
	- Use Redshift for data warehousing and OLAP tasks, like analyzing large amounts of data, reporting, and sales forecasting

## Increasing Read Performance with Read Replicas
Read replica, improve performance
read-only copy of your primary database

Multi-AZ disaster recovery

cross-region or in the same AZ
Each read replica has its own DNS endpoint
Read replicas can be promoted to be their own databases
This breaks the replication

1. Scaling Read Performance
2. Requires Automatic Backup
3. Multiple Read Replicas Are Supported

> Note: Amazon RDS read replicas complement Multi-AZ deployments. The main purpose of read replicas is scalability, whereas the main purpose for Multi-AZ deployments is availability. However, you may use a read replica for disaster recovery of the source DB instance either in the same AWS Region or in the another Region. Check the resources section of this lecture for more details

| Multi-Az                                                                            | Read Replica                                                                        |
| ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| An exact copy of your prodcution database in another Availability Zone              | A read-only copy of your primary database in the same AZ, cross-AZ, or cross-region |
| Used for disaster recovery                                                          | Used to increase or scale read perfomance                                                                                   |
| In the event of a failure, RDS will automatically fail over to the standby instance | Great for read-heavy workloads and takes the load off your primary database for read-only workloads (e.g., business intelligence reporting jobs)                                                                                    |

## What is Amazon Aurora
MySQL and PostgreSQL - compaible relational database engine that combines the speed and availability of high-end commercial databases with the simplicity and cost-effectiveness of open-source databases

#### Aurora Serverless Use Cases
Aurora Serverless provides a relatively simple, cost-effective option for infrequent, intermitten, or unpredictable workloads. An Aurora Serverless DB cluster automatically starts up, shuts down, and scales capacity up and down based on your application's needs

- 2 copies of your data are contaiined in each Availability zone, with a minimum if 3 Availability Zones. 6 copies of your data
- You can share Aurora snapshots with other AWS accounts
- 3 types of replicas available: Aurora replicas, MySQL replicas, and PostgreSQL replicas. Automated failover is only available with Aurora replicas
- Aurora has automated backups turned on by default. You can share these snapshots with other AWS accounts
- Use Aurora Serverless if you want a simple, cost-effective option for infrequent, intermittent, or unpredictable workloads
