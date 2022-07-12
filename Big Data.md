## Exploring Large Redshift Databases
Redshift is a fully managed, petabyte-scale data warehouse service in the cloud. It's a very large relartional database traditionally used in big data applications

> It's Big
> Redshift won't be featured in too much depth on the exam, but it's still good to know the basics
> Keep in mind it's for BI applications, it's relational, and it can store up to 16 PB of data

- Not standard
	- Make sure you don't use Redshift in place of RDS
- It's Big
	- Redshift can support a lot of data: up to 16 PB
- Relational
	- Redshift is a relational database
Backups are kept for 1 day by default, but this can be raised up to 35 days at most.

## Processing Data with EMR (Elastic MapReduce)
ETL ->
EMR is a managed big data platform that allows you to process vast amounts of data using open-source tools, such as Spark, Hive, HBase, Flink, and Presto

>It's an Open-Source Cluster
>EMR is a managed fleet of EC2 instances running open-source tools
>It's similar to the other open-source managed architecture in that it gets the fleet up and running quickly, but the technology isn't propietary to AWS

- EC2 Rules Apply
	- You can use RIs and Spot Instancesd to reduce your costs
- High level
	- Understanding EMR is used to process and move data is enough for the exam
- VPC
	- The architecture lives inside a VPC

## Streaming Data with Kinesis
Kinesis allows you to ingest, proces, and analyze real-time streaming data. You an think of it as a huge data highway connected to your AWS account

|            | Data Streams                                                        | Data Firehouse                                                                  |
| ---------- | ------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| Purpose    | Real-time streaming for ingesting data                              | Data transfer tool to get information to S3, Redshift, Elasticsearch, or Splunk |
| Speed      | Real time                                                           | Near real time (within 60 seconds)                                              |
| Difficulty | You're responsible for creating the consumer and scaling the stream | Plug and play with AWS architecture                                             |

#### When your looking for a message broker, which do we pick?
| SQS                                                                                                                                 | Kinesis                                                                                                                             |
| ----------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| SQS is a messaging broker that is simple to use and doesn't require much configuration. It doesn't offer real-time message delivery | Kinesis is a bit more complicated to configure and is mostly used in big data applications. It does provide real-time communication |

> Real time? Kinesis
> There are very few services in AWS that offer "real-time" processing. Kinesis is one of the few services that offers this speed
> If you're faced with a question that asks for real-time processing or streaming of data, look for an answer that includes Kinesis

- Transforming Data
	- Data analytics is the easiest way to process data going thorugh Kinesis using SQL
- Scaling
	- Data Streams does not automatically scale. Data Firehouses does

## Amazon Athena and AWS Glue
Athena is an interactive query service that makes it easy to analyze data in S3 using SQL. This allows you to directly query data in your S3 bucket without loading it into a database

Glue is serverless data integration service that makes it easy to discover, prepare, and combine data. It allows you to perform ETL workloads without managing underlying servers

> ### Serverless SQL
> If you're ever faced with a scenario that's looking for a serverless SQL solution, Athena is your best choice. It's the only service that allows you to directly query your data that's stored in S3
> This is a common big data sceneario on the exam
- Serverless
	- Both solutions are fully manaed serverless services
- Overview
	- Knowing the 3,000-foot view of these services is good enough for this exam
- Better Together
	- While Athena can work by itself, Glue can design a schema for your data

## Visualizing Data with QuickSight
Amazon QuickSight is a fully managed business intelligence (BI) data visualization service. It allows you to easily create dasboards and share them within your company

>Looking at your data
>If you're give a scenario on the exam that talks about sharing your data, interpreting that data, or anything related to business inteliigence, look for an answer that includes QuickSight

- Visualize
	- Need to look at your data? Use QuickSight to do it
- Overview
	- Knowing the 3,00 foot view of these services is good enough  for the exam
- Business intelligence
	- If this phrase comes up, start looking for QuickSight

## Analyzing Data with Elasticsearch
Amazon ElasticSearch Service is a fully managed version of the open-source application Elasticsearch. It allows you to quickly search over your stored data and analyze the data you get back. It's commnly used as aprt of an Elalasticsearch, Logstash, Kibana (ELK) stack

> Elasticsearch love logs
> If your're given a scenario on the exam that talks about creating a third-party logging solutionm there's a good chance Elasticsearch will be involved. Be on the lookout for an Elasticsearch, Logstash, Kibana (ELK) stack

- Open Source
	- Why do it yourself? Elasticsearch managed service
- Overview
	- Knowing the 3,000-foot view of these services is good enough for this exam
- Distractor 
	- Elasticsearch will most likely be a distractor on the exam

1. What kind of database works?
2. How much data do you have?
3. Is serverless a requirement?
4. How do we optimize cost?

- While Redshift is a relational database, it's not a replacement for RDS in traditional applications
- Redshift only supports single-AZ deployments. You can create multiple clusters in different AZs, but they're technically separate deployments. It's not highly available by default
- EMR is made up of EC2 instances. This means you can employ your standard EC2 instance cost-saving measures
- Kinesis is the only service with a real time response. If the questions for ar real time solution to processing or moving data, look for an answer that includes Kinesis
- SQS and Kinesis can both be queues. Each has its pros and cons. SQS is easier and simpler, and Kinesis is faster and can store data up to a year
- Serverless SQL means Athena. Anytime serverless SQL or querying data that is stored in S3 comes up, think Athena
- Glue is serverless ETL. It can help create that schema for your data when paired with Athena
- Creating a dashboard? QuickSight is going to be your go-to tool for visualizing data
- Elasticsearch escels when it's combined with Logstash and Kibana. This creates an ELK stack and is a very common way to search over your server logs.
