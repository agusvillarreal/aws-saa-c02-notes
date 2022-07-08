## CloudWatch Overview
CloudWatch is a monitoring and observability platform that was designed tyo give us insight into our AWS architecture. It allows us to monitor multiple levels of our applications and identify potential issues

> ### What Tool Do we use to Monitor?
> On tghe examn, cloudWatch
> You need to know the basic checks that are included out of the box, as well as what you're responsible for bringing to the table

- Alarms: There are no default alarms. 
- Default vs Custom
- Managed Services
- Standard vs Detailed

## Application Monitoring with CloudWatch Logs
1. Log Event: Thisis the record of what happened. It contains a timestamp and the data
2. Log Stream: A collection of log events from the same source create a log stream. Think of one continuous set of logs from a single instance
3. Log Group: This is a collection of log streams. Fro exmaple, youd group all your apache web server logs across hosts together 

> ### Logs Groups Go to CloudWatch Logs
> Except for situations where we don't need to process them. Then, they should straight to S3

- Go-To tool: generally, favor CloudWatch logs, unless the exman asks for a real time solution
- Alarms: CloudWatch alarms can be used to alert if the filter patterns are found 
- Agent Based: The CloudWatch agent must be installed and configured. It's not automatic
- SQL: If the examn mentions SQL, think CloudWatch Logs Insights

1. What is the best tool to monitor with?
2. Is that metric available by default?
3. Where can I find those logs?
4. Do I need to adjust my alarm threshold?

CloudWatch is the main tool for anything related (processing)
Other tools for monitoring, monitor best practices for AWS Config
System level, application level -> CloudWatch
Monitoring AWS standars and best practices -> AWS Config

- CloudWatch Logs is the place for logs: It's important to know EC2, on-premise, RDS, Lambda, and CloudTrail can all integrate with this service
- SQL -> Insights
- Kineses -> real time solutions, processing real time data

A period is the length of time associated with a specific Amazon CloudWatch statistic. Each statistic represents an aggregation of the metrics data collected for a specified period of time. Periods are defined in numbers of seconds, and valid values for period are 1, 5, 10, 30, or any multiple of 60. For example, to specify a period of six minutes, use 360 as the period value. You can adjust how the data is aggregated by varying the length of the period. A period can be as short as one second or as long as one day (86,400 seconds). The default value is 60 seconds.

## EventBridge
Event patterns have the same structure as the events they match. Amazon EventBridge (formerly called Amazon CloudWatch Events) use event patterns to select events and route them to targets. An event pattern either matches an event or it doesn't. Event patterns are represented as JSON objects with a structure that is similar to that of events
