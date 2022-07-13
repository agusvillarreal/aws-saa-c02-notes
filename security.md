## DDoS Overview
A distributed Denial of Service (DDoS) attack is an atack that attempts to mae your website ir application unavailable to your end users 

- Common DDoS attacks include layer 4 attacks such as SYN floods or NTP amplification attacks
- Common Layer 7 attacks include floods of GET/POST requests

## Logging API calls with CloudTrail
You can identify which users and accounts called AWS, the source IP address from which the calls were made, and when the call occureed

- Metadata
- Identity
- Time
- Source IP

> Remember that CloudTrail is basically jsut CCTV for your AWS account. It logs all API calls made to your AWS account and stores these logs in S3

## Protectiong Applications with Shield
Free DDoS Protection
> ### Shield Protects Against Layer 3 and Layer 4 only
> Remember whhat Shield is at a high level and that it's used to protect against DDoS. If you see a scenario question talking about DDoS mitigation or protection against Layer 3 and Layer 4 attacks, think AWS Shield
> Advanced costs 3,000 USD a month but will give you a dedicated 24/7 DDoS Response Team

## Filtering Traffic with AWS WAF
AWS WAF is a web application firewall that lets you monitor the HTTP and HTTPS requests that are forwarded to Amazon CloudFront or an Application Load Balancer
also lets you control access to your content
> Operates at Layer 7

In the exam, you will get scenario-based questions asking hwo to block Layer 7 attacks. Always think of WAF whenever you hear the term Layer 7. WAF can block Layer 7 DDoS attacks as well as things like SQL injections and cross-site scripting

If you need to block access to specific countries or IP addresses, you can also achieve this using AWS WAF

## Guarding your Network with GuardDuty
Is a treat detection service that uses machine learning to continuously monitor for malicious behavior

- Uses AI to learn what normal behavior looks like in your account and to alert you any abnormal or malicious behavior
- Updates a database of known malicious domains using external feeds from third parties
- Monitor CloudTrail logs, VPC Flow Logs, and DNS logs
- Findings appear in the GuardDuty dashboard. CloudWatch Events can be used to trigger a Lambda function to address a threat

## Monitoring S3 Buckets with Macie
Macie uses machine learning and pattern matching to discover sensitive data stored in S3
- Uses AI to analyze data in S3 and helps identify PII, PHI, and financial data
- Great for HIPAA and GDPR compliance as well as preventing identity theft
- Macie alerts can be sent to Amazon EventBridge and integrated with your event management systems
- Automate remediation actions using other AWS services, such as Step Functions

## Securing Operating Systems with Inspector
Amazon Inspector is an automated security assessment service that helps improve the security and compliance of applications deployed on AWS
1. Create assessment target
2. Install agents on EC2 instances
3. Create assessment template
4. Perform assessment run
5. Review findings against rules

> Going into the exam, remember what inspector is: it's used to perform vulnerability scans on both EC2 instances and VPCs
> These are called host assessments and network assessments. You can run these assessments once or, alternatively, run them weekly

## Managing Encryption with Key Management Service and CloudHSM
KMS is a managed service that makes it easy for you to create and control the encryption keys used to encrypt your data

#### CMK
A customer master key (CMK) is a logical representation of a master key. The CMK includes metadata, such as the key ID, creation date, description and key state

> **Policies attached to an IAM identity are called identity-based policies (or IAM policies), and policies attached to other kinds of resources are called resource-based policies**

### CloudHSM
HSM -> Hardware Security Model
AWS CloudHSM is a cloud-based HSM that enables you to easily generate and use your own encryption keys on the AWS Cloud

| KMS                                   | CloudHSM                                  |
| ------------------------------------- | ----------------------------------------- |
| Shared tenancy of underlying hardware | Dedicated HSM to you                      |
| Automatic key rotation                | Full control of underlying hadware        |
| Automatic key generation              | Full control of users, groups, keys, etc. |
| .                                     | No automatic key rotation                 | 

### 3 ways to generate a CMK
1. AWS creates the CMK for you. The key material for a CMK is generated within HSMs managed by AWS
2. Import key material from your own key management infrastructure and associate it with a CMK
3. Have the key material generated and used in an AWS CloudHSM cluster as part of the custom key store feature in AWS KMS

### 3 ways to control permissions
- Use the key policy: controlling access this way means the full scope of access to the CMK is defined in a single document 
- Use IAM policies in combination with the key policy: Controlling access this way enables you to manage all the permissions for you IAM identities in IAM
- Use grants in combination with the key policy: Controlling access this way enables you to allow access to the CMK in the key policy, as well as allow users to delegate their access to others

## Storing you secrets in Secrets Manager
Secret manager is a service that securely sotres, encypts, and rotates your databse credentials and other secrets
> If you enable rotation, Secrets Manager immediately rotates the secret once to test the configuration

- Applications use the Secrets Manager API
- Rotating credentials is super easy - but be careful
- When enabled, Secrets Manager will rotate credentials immediately
- Make sure all your application instances are configured to use Secrets Manager before enabling credential rotation

## Parameter store
Parameter Store is a capability of AWS Systems Manager that provides secure, hierarchical storage for configuration data management and secrets management

free
MINIMIZE COST -> Parameter store
> If you need mora than 10,000 parameters, key rotaion, or the ability to generate passwords using CloudFormation, use Secrets Manager

## Temporarily Sharing S3 obects Using presigned URLs or Cookies
#### Access 
Anyone who receives the presigned URL can then access the object. For example, if you have a video in your bucket and both the bucket and the object are private, you can share the video with others by generating a presigned URL

> If you see a scenario question where you need to share private files in your S3 buckets,  think presigned URLs

## Advanced IAM policy Documents
- A policy document is a list of statements
- Each statement matches an AWS API request

- Not explicity allowed == implicity denied
- Explicty deny > everything else
- Only attached policies have effect
- AWS joins all applicable policies
- AWS managed vs customer managed 

## Certificate manager
AWS Certificate Manager allows you to create, manage, and deploy public and private **SSL certificates** for use with other AWS services

- Supported Services: AWS Certificate Manager integrates with Elastic Load Balancing, CloudFront, and API Gateway
- Benefits: AWS Certificate Manager is a free service that saves time and money. Automatically renew your SSL certificates and rotate the old certificates with new certificates with supported AWS services
