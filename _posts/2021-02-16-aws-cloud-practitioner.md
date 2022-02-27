---
title: "AWS Cloud Practitioner"
excerpt: "For CLF-C01 AWS Certified Cloud Practitioner"
last_modified_at: 2021-02-16
toc: true
toc_label: "Content"
toc_sticky: true
categories:
  - Cheatsheets
tags:
  - AWS
  - Cloud
---

## Key points
- Region -> Availability Zones -> Edge Locations
- Standard reserved instances can be sold in the Marketplace, convertible reserved instances can be exchanged with a different configuration
- Internet gateway at VPC to connect to public
- Network ACL (access control list): stateless at subnet, default allow all
- Security groups: stateful at instances, default deny all

<br>

## Cloud computing advantages
1. Capital expense -> variable expense
2. Massive economies of scale
3. Stop guessing capacity
4. Increase speed and agility
5. Stop paying and maintaining data centres
6. Go global in minutes

<br>

## AWS values
1. Agility: fast deployment
2. Elasticity: on demand
3. Availability: multiple AZ
4. Flexibility: variety of products
5. Security: shared responsibility model

<br>

## Well architected framework pillars
1. Operational Excellence
2. Security
3. Reliability
4. Performance Efficiency
5. Cost Optimisation

<br>

## Support plans
1. Free
2. Developer: business hours email
3. Business: 24x7 email, phone and chat, full Trusted Advisor
4. Enterprise: dedicated TAM (technical account manager), Concierge support team, SLA < 15 mins for critical cases

<br>

## AWS products
### Analytics
- Amazon Athena: SQL query over S3
- Amazon EMR: Hadoop framework
- Amazon CloudSearch: search solution
- Amazon Elasticsearch Service: real time search
- Amazon Kinesis: real time data, usually media related
- Amazon Redshift: data warehouse
- Amazon QuickSight: interactive dashboard of business insights
- AWS Data Pipeline: move data across AWS and on-prem
- AWS Glue: ETL (extract, transform, load)
- AWS Lake Formation: secure data lake
- Amazon MSK (managed streaming for Kafka): Apache Kafka

<br>

### Application integration
- AWS Step Functions: state machine of Lambda functions
- Amazon MQ: message broker for ActiveMQ
- Amazon SQS (simple queue service): put in queue and wait for pull
- Amazon SNS (simple notification service): push notification
- Amazon SWF (simple workflow): task oriented flow

<br>

### Cost management
- AWS Cost Explorer: predict cost
- AWS Budgets: set alerts
- AWS Cost & Usage Report: granular cost details
- Reserved Instance (RI) Reporting: manage reserved instances cost
- AWS TCO (total cost of ownership): cost for migrating to cloud
- AWS Simple Monthly Calculator: predict cost without account

<br>

### Business applications
- Alexa for Business: book meeting rooms etc
- Amazon WorkDocs: Google Doc
- Amazon WorkMail: Gmail with calendar
- Amazon Chime: video conferencing

<br>

### Compute
- Amazon EC2 (elastic compute cloud): VM
    - On demand: pay by second based on hourly rate
    - Reserved: 75% discount, 3-year convertible cheapest
    - Spot: 90% discount, short and interruptible
    - Dedicated: isolated hardware
- Amazon EC2 Auto Scaling: adjust number of EC2
- Amazon ECR (elastic container registry): manage Docker containers
- Amazon ECS (elastic container service): orchestration for Docker containers
- Amazon EKS (elastic kubernetes service): manage k8s containers
- Amazon Lightsail: user friendly deployment for small applications
- AWS Batch: manage batch jobs
- AWS Elastic Beanstalk: package deploy (application + capacity etc)
- AWS Fargate: serverless container
- AWS Lambda: serverless code run, charged by running time
- AWS Serverless Application Repository: deploy code snippets
- AWS Outposts: hybrid API
- VMware Cloud on AWS: vSphere on AWS

<br>

### Customer engagement
- Amazon Connect: customer support centre
- Amazon SES (simple email service): send professional email

<br>

### Database
- Amazon Aurora: serverless MySQL and PostgreSQL, auto scaling
- Amazon RDS (relational database service): common DB with patching and backup
- Amazon DynamoDB: serverless key-value DB, no SQL
- Amazon ElastiCache: cache frequent query results
- Amazon Neptune: graph DB (usually for social media)
- Amazon QLDB (quantum ledger database): serverless ledger DB
- Amazon Timestream: serverless time series DB (usually for IoT)
- Amazon DocumentDB: serverless document DB with MongoDB

<br>

### Desktop and app streaming
- Amazon WorkSpaces: VDI
- Amazon AppStream: desktop application delivery

<br>

### Developer
- AWS CodeCommit: GitHub, version control
- CodeBuild: serverless compilation of source code, test and produce software package for deployment
- CodeDeploy: automate deployment, avoid downtime
- CodePipeline: automate updates with testing
- AWS CodeStar: orchestration of above
- Amazon Corretto: OpenJDK (Java development kit)
- AWS Cloud9: IDE
- AWS X-Ray: analyse and debug applications

<br>

### Machine learning
- SageMaker: serverless all in one ML for newbie
- Amazon Comprehend: NLP
- Amazon Lex: Alexa speech recognition
- Amazon Polly: text to speech
- Amazon Rekognition: image recognition
- Amazon Translate: translation
- Amazon Transcribe: speech to text
- Amazon Elastic Inference: EC2 + SageMaker for deep learning
- Amazon Forecast: forecasting
- Amazon Textract: text and data extraction from scanned documents
- Amazon Personalize: individual recommendations for users
- Amazon Deep Learning AMIs: EC2 AMI for deep learning
- AWS DeepLens: pre trained deep learning models
- AWS DeepRacer: race car for reinforcement learning
- AWS Inferentia: ML inference chip

<br>

### Management and governance
- Amazon CloudWatch: usage and alarms
- AWS Auto Scaling: adjust capacity
- AWS Control Tower: set up initial environment
- AWS Systems Manager: manage AWS products with insights dashboard
- AWS CloudFormation: deploy AWS products with template
- AWS CloudTrail: AWS API call log
- AWS Config: change management
- AWS OpsWorks: configuration management with Chef and Puppet
- AWS Service Catalog: organisation's IT services
- AWS Trusted Advisor: identify and suggest improvements
    1. Cost
    2. Performance
    3. Security
    4. Fault tolerance
    5. Optimise
- AWS Personal Health Dashboard: affects from AWS service outage
- AWS Managed Services: ongoing management of AWS infrastructure
- AWS Console Mobile Application: manage AWS products status on the go
- AWS License Manager: manage licenses
- AWS Well-Architected Tool: review workloads

<br>

### Migration and transfer
- AWS Migration Hub: track migration progress
- AWS Application Discovery Service: plan migration projects
- AWS Database Migration Service: migrate DB to AWS
- AWS SMS (server migration service): agentless migration of workloads to AWS
- AWS Snowball: petabyte-scale hardware data transport
- AWS Snowball Edge: data migration and edge computing
- AWS Snowmobile: exabyte-scale 100 PB truck
- AWS DataSync: data transfer between on-prem and S3 and EFS
- AWS Transfer for SFTP: S3 through SFTP

<br>

### Mobile services
- AWS Amplify: mobile application backend
- Amazon Cognito: application login
- Amazon Pinpoint: campaign emails and notifications
- AWS Device Farm: test on various devices
- AWS AppSync: serverless application backend

<br>

### Networking and content delivery
- Amazon VPC (virtual private cloud): logically isolated section of AWS cloud
- Amazon CloudFront: CDN
- Amazon Route 53: DNS
- AWS PrivateLink: private connection between VPC and on-prem
- AWS Direct Connect: fibre direct connection
- AWS Global Accelerator: find optimal path to reach resources
- Amazon API Gateway: serverless API
- AWS Transit Gateway: connect multiple VPC and on-prem networks
- AWS App Mesh: manage microservices on AWS
- AWS Cloud Map: cloud resource discovery service
- Elastic Load Balancing: distribute traffic
    - ALB (application): layer 7 (request level, HTTP)
    - NLB (network): layer 4 (connection level, IP)
    - CLB (classic): both levels (for old EC2-Classic)

<br>

### Security
- AWS Security Hub: alerts and compliance
- Amazon Cloud Directory: AD
- AWS IAM (identity and access management): users, roles, groups
- Amazon GuardDuty: threat detection
- Amazon Inspector: vulnerability report
- Amazon Macie: sensitive data supported by ML
- AWS Artifact: on demand compliance report
- AWS Certificate Manager: SSL and TLS certificates
- AWS CloudHSM: hardware security module encryption keys
- AWS Directory Service: Microsoft AD integration
- AWS Firewall Manager: centralised WAF rules
- AWS KMS (key management service): manage encryption keys
- AWS Organizations: policies, consolidate billing
- AWS Secrets Manager: manage secrets
- AWS Shield: DDoS protection
- AWS SSO (single sign-on)
- AWS WAF

<br>

### Storage
- Amazon S3 (simple storage service): object storage, not file system, 99.999999999% durability
- Amazon EBS (elastic block store): persistent instance storage
- Amazon EFS (elastic file system): shared Linux file system
- Amazon FSx for Lustre: serverless file system for compute-intensive workloads
- Amazon FSx for Windows File Server: serverless Windows file system
- Amazon S3 Glacier: data archiving, slow retrieval
- AWS Storage Gateway: hybrid storage

<br>

### Others
- Amazon Sumerian: VR, AR, 3D applications
- Amazon Managed Blockchain: Fabric and Ethereum
- Amazon GameLift: serverless game servers
- Amazon Lumberyard: 3D game engine
- AWS IoT Core: manage IoT devices (connection and communication)
- AWS Partner Device Catalog: find compatible device and hardware for IoT solutions
- Amazon Elastic Transcoder: media transcoder
- AWS Elemental MediaConvert: new video transcoder
- AWS RoboMaker: manage robotics applications
- AWS Ground Station: serverless satellite operations

<br>

## Study resources
- AWS official training: <https://www.aws.training/Details/eLearning?id=60697>
- AWS overview whitepaper: <https://docs.aws.amazon.com/whitepapers/latest/aws-overview/aws-overview.pdf>
- Cloud practitioner full course: <https://www.youtube.com/watch?v=3hLmDS179YE>
- AWS services overview: <https://www.youtube.com/watch?v=TkT4iFRkaZk>
- Exam dump: <https://www.examtopics.com/exams/amazon/aws-certified-cloud-practitioner>

<br>

## Exam
- Study time: 12 hours
- Exam time: 27 minutes
- Result: 881 / 1000 PASS
- Note: mainly testing on the understanding of different AWS products, a lot of questions were shown in the exam dump
