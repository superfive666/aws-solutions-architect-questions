# CSAA Practice Test 1

### Question 10

You are working for a start-up company that develops mobile gaming applications using AWS resources. For creating AWS resources, the project team is using CloudFormation Templates. The Project Team is concerned about the changes made in EC2 instance properties by the Operations Team, apart from parameters specified in CloudFormation Templates. To observe changes in AWS EC2 instance, you advise using CloudFormation Drift Detection. After Drift detection, when you check drift status for all AWS EC2 instances, drift for certain property values with default values for resource properties is not displayed. What would you do to include these resource properties to be captured in CloudFormation Drift Detection?

- A: Run CloudFormation Drift Detection on individual stack resources instead of entire CloudFormation stack.
- B: Explicitly set the property value, which can be the same as the default value.
- C: Manually check these resources as this is not supported in CloudFormation Drift Detection.
- D: Assign Read permission to CloudFormation Drift Detection to determine drift.

#### *Answer: B*

AWS CloudFormation Drift Detection can be used to detect changes made to AWS resources outside the CloudFormation Templates. AWS CloudFormation Drift Detection only checks property values explicitly set by stack templates or by specifying template parameters. It does not determine drift for property values that are set by default. To determine drift for these resources, you can explicitly set property values that can be the same as that of the default value.

**Option A is incorrect.** If property values are assigned explicitly to these properties, running AWS CloudFormation Drift Detection would be detected in both individuals and the entire CloudFormation Stack.

**Option C is incorrect.** CloudFormation Drift Detection supports the AWS EC2 instance.

**Option D is incorrect.** Since for all other resources, CloudFormation Drift Detection has already determined drift, there is no other read permission to be granted further.

For more information on AWS CloudFormation Drift Detection, refer to [AWS CloudFormation Drift Detection](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-stack-drift.html)

### Question 11

You are responsible for performing a migration from your company's on-premise data to the AWS cloud. You have about 400 GB of data stored in an NFS. One requirement of this migration is to transfer some of this data to AWS EFS and the other part to S3. Which is the easiest to use and with the most cost-effective solution?

- A: Use AWS Storage gateway.
- B: Use S3 Transfer Acceleration.
- C: Use S3 DataSync.
- D: Use AWS Database Migration Service.

#### *Answer: C*

DataSync is a service used to transfer data between on-premise storage to AWS S3, EFS and FSx. It is cost-effective, easy to use, and can handle the transfer to EFS and S3. More details: [AWS S3 DataSync](https://aws.amazon.com/datasync/faqs/)

**Option A is incorrect.**  Storage Gateway is a hybrid cloud storage service to share and access data between your on-premise resources and AWS resources. It is not mainly designed to migrate data from On-Premise to AWS. Additionally, all three storage gateway patterns are backed by S3, not EFS. More details: [AWS Storage gateway](https://aws.amazon.com/storagegateway/faqs/)

**Option B is incorrect.**  S3 Transfer Acceleration is used to transfer data to S3 using Amazon CloudFront’s globally distributed edge locations, increasing data transfer speed. However, this option doesn't work to transfer data to AWS EFS. More details: [AWS S3](https://docs.aws.amazon.com/AmazonS3/latest/dev/transfer-acceleration.html)

**Option D is incorrect.** Because AWS Database Migration Service is used to migrate databases to AWS databases like Aurora, DynamoDB, etc. In this scenario, we don’t mention a database migration, and with this service, you can not transfer data to EFS nor S3. More details: [AWS DMS](https://aws.amazon.com/dms/)

### Question 12

A company hosts a popular web application that connects to an Amazon RDS MySQL DB instance running in a default VPC private subnet with NACL settings that was created by AWS as default. The web servers must be accessible only to customers on HTTPS connections, and the database must only be accessible to web servers in a public subnet. Which solution would meet these requirements without impacting other applications? (SELECT TWO)

- A: Create a network ACL on the Web Server's subnets, allow HTTPS port 443 inbound and specify the source as 0.0.0.0/0.
- B: Create a Web Server security group that allows HTTPS port 443 inbound traffic from anywhere (0.0.0.0/0) and apply it to the Web Servers.
- C: Create a DB Server security group that allows MySQL port 3306 inbound and specify the source as the Web Server security group.
- D: Create a network ACL on the DB subnet, allow MySQL port 3306 inbound for Web Servers and deny all outbound traffic.
- E: Create a DB Server security group that allows HTTPS port 443 inbound and specify the source as a Web Server security group.

#### *Answer: B & C*

1) To ensure that traffic can flow into your webserver from anywhere on secure traffic, you need to allow inbound security at 443.

2) And then, you need to ensure that traffic can flow from the webserver to the database server via the database security group.

### Question 13

You lead a team to develop a new web application in AWS EC2. The application will have a large number of users globally. For a great user experience, this application requires very low network latency and jitter. If the network speed is not fast enough, you will lose customers. Which tool would you choose to improve the application performance? (Select TWO.)

- A: AWS VPN
- B: AWS Global Accelerator
- C: Direct connect
- D: API Gateway
- E: CloudFront

#### *Answer: B & E*

This web application has global users and needs low latency. Both CloudFront and Global Accelerator can speed up the distribution of contents over the AWS global network.

**Option A is incorrect.** AWS VPN links on-premise network to AWS network. However, no on-premise services are mentioned in this question.

**Option B is correct.** AWS Global Accelerator works at the network layer and can direct traffic to optimal endpoints. For reference, check the link. [AWS Global Accelerator](https://docs.aws.amazon.com/global-accelerator/latest/dg/what-is-global-accelerator.html)

**Option C is incorrect.** Direct Connect links on-premise network to AWS network. However, no on-premise services are mentioned in this question.

**Option D is incorrect.** API Gateway is a regional service and cannot improve the application performance. API Gateway is suitable for serverless applications such as Lambda.

**Option E is correct.** Because CloudFront delivers content through edge locations, and users are routed to the edge location with the lowest time delay.

### Question 14

You are deploying an application on Amazon EC2 that must call AWS APIs. Which method would you use to allow the application access to the APIs securely?

- A: Pass API credentials to the instance using Instance userdata.
- B: Store API credentials as an object in Amazon S3.
- C: Embed the API credentials into your application.
- D: Assign IAM roles to the EC2 Instances.

#### *Answer: D*

You can use roles to delegate access to users, applications, or services that don't normally have access to your AWS resources. It is not a good practice to use IAM credentials for a production-based application. However, it is a good practice to use IAM Roles. [AWS IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)

### Question 15

A website runs on EC2 Instances behind an Application Load Balancer. The instances run in an Auto Scaling Group across multiple Availability Zones and deliver several static files stored on a shared Amazon EFS file system. The company needs to avoid serving the files from EC2 Instances every time a user requests these digital assets.

What should the company do to improve the user experience of the website?

- A: Move the digital assets to Amazon Glacier.
- B: Cache static content using CloudFront.
- C: Resize the images so that they are smaller.
- D: Use reserved EC2 Instances.

#### *Answer: B*

Amazon CloudFront is a web service that speeds up distribution of your static and dynamic web content, such as .html, .css, .js, and image files to your users. CloudFront delivers your content through a worldwide network of data centers called edge locations. When a user requests content that you're serving with CloudFront, the user is routed to the edge location that provides the lowest latency (time delay), so that the content is delivered with the best possible performance. If the content is already in the edge location with the lowest latency, CloudFront delivers it immediately. [AWS CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)

In addition, the glacier is not used for frequent retrievals. So Option A is not a good solution. Options C & D will also not help in this situation.

### Question 16

A Solutions Architect is designing a highly scalable system to track records. These records must remain available for immediate download for up to three months and then must be deleted. What is the most appropriate decision for this use case?

- A: Store the files in Amazon EBS and create a Lifecycle Policy to remove files after 3 months.
- B: Store the files in Amazon S3 and create a Lifecycle Policy to remove files after 3 months.
- C: Store the files in Amazon Glacier and create a Lifecycle Policy to remove files after 3 months.
- D: Store the files in Amazon EFS and create a Lifecycle Policy to remove files after 3 months.

#### *Answer: B*

Lifecycle configuration enables you to specify the Lifecycle Management of objects in a bucket. The configuration is a set of one or more rules, where each rule defines an action for Amazon S3 to apply to a group of objects. These actions can be classified as follows:

**Transition actions** – In which you define when the transition of the object occurs to another storage class. For example, you may choose to transition objects to the STANDARD_IA (IA, for infrequent access) storage class 30 days after creation or archive objects to the GLACIER storage class one year after creation.

**Expiration actions** – In which you specify when the objects will expire. Then Amazon S3 deletes the expired objects on your behalf.

[AWS S3 Lifecycle](https://docs.aws.amazon.com/AmazonS3/latest/dev/object-lifecycle-mgmt.html)

[AWS EFS Lifecycle](https://docs.aws.amazon.com/efs/latest/ug//lifecycle-management-efs.html)

**Option A is incorrect.** Since the records need to be stored in a highly scalable system.

**Option C is incorrect.** Since the records must be available for immediate download.

**Option D is incorrect.** Since EFS lifecycle management is used to migrate files that have not been accessed for a certain period of time to the Infrequent Access storage class. Files moved to this storage remain indefinitely and not get deleted. And due to this reason, this option is not correct.

### Question 17

A consulting firm repeatedly builds large architectures for their customers using AWS resources from several AWS services, including IAM, Amazon EC2, Amazon RDS, DynamoDB and Amazon VPC. The consultants have architecture diagrams for each of their architectures and are frustrated that they cannot use them to create their resources automatically.

Which service should provide immediate benefits to the organization?

- A: AWS Beanstalk
- B: AWS CloudFormation
- C: AWS CodeBuild
- D: AWS CodeDeploy

#### *Answer: B*

AWS Documentation mentions the following on AWS CloudFormation:

AWS CloudFormation is a service that helps you model and set up your Amazon Web Service resources so that you can spend less time managing those resources and more time focusing on your applications that run in AWS. You create a template that describes all the AWS resources that you want (like Amazon EC2 instances or Amazon RDS DB instances), and AWS CloudFormation takes care of provisioning and configuring those resources for you. [AWS CloudFormation user guide](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)

AWS Elastic Beanstalk is an easy-to-use service for deploying and scaling web applications and services developed with Java, .NET, PHP, Node.js etc. You can upload your code, and Elastic Beanstalk automatically handles the deployment, from capacity provisioning, load balancing, auto-scaling to application health monitoring.

In question mentioned that "A consulting firm **repeatedly builds large architectures for their customers using AWS resources from several AWS services including IAM, Amazon EC2, Amazon RDS, DynamoDB and Amazon VPC.**

When you are building large architectures repeatedly, you can use the CloudFormation template to create or modify an existing AWS CloudFormation template. A template describes all of your resources and their properties. When you use that template to create an AWS CloudFormation stack, AWS CloudFormation provisions the Auto Scaling group, load balancer, and database for you. After the stack has been successfully created, your AWS resources are up and running. You can delete the stack just as easily, which deletes all the resources in the stack. By using AWS CloudFormation, you easily manage a collection of resources as a single unit. Whenever working with more number of AWS resources together, CloudFormation is the best option.

### Question 18

The security policy of an organization requires an application to encrypt data before writing to the disk. Which solution should the organization use to meet this requirement?

- A: AWS KMS API
- B: AWS Certificate Manager
- C: API Gateway with STS
- D: IAM Access Key

#### *Answer: A*

**Option B is incorrect.** The AWS Certificate Manager can be used to generate SSL certificates to encrypt traffic in transit, but not at rest.

**Option C is incorrect.** It is used for issuing tokens while using the API gateway for traffic in transit.

Option D is used for providing secure access to EC2 Instances. (Or sometimes other AWS resources)

AWS Key Management Service (AWS KMS) is a managed service that makes it easy for you to create and control the encryption keys used to encrypt your data. AWS KMS is integrated with other AWS services including Amazon Elastic Block Store (Amazon EBS), Amazon Simple Storage Service (Amazon S3), Amazon Redshift, Amazon Elastic Transcoder, Amazon WorkMail, Amazon Relational Database Service (Amazon RDS), and others to make it simple to encrypt your data with encryption keys that you manage.

[AWS KMS user guid](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html)
[AWS KMS API references](https://docs.aws.amazon.com/kms/latest/APIReference/kms-api-reference.pdf#Welcome)

### Question 19

You are an AWS Solutions Architect. Your company has a successful web application deployed across multiple AWS Regions. The application attracts more and more global customers. However, the application’s performance is impacted. Your manager asks you how to improve the performance and availability of the application. Which of the following AWS services would you recommend?

- A: AWS DataSync
- B: Amazon DynamoDB Accelerator
- C: AWS Lake Formation
- D: AWS Global Accelerator

#### *Answer: D*

AWS Global accelerator provides static IP addresses that are anycast in the AWS edge network. Incoming traffic is distributed across endpoints in AWS regions. The performance and availability of the application are improved. Therefore, Option D is correct, [AWS Global Accelerator use case](https://docs.aws.amazon.com/global-accelerator/latest/dg/introduction-benefits-of-migrating.html)

### Question 20

A retailer exports data daily from its transactional databases into an S3 bucket in the Sydney region. The retailer's Data Warehousing team wants to import this data into an existing Amazon Redshift cluster in their VPC in Sydney. Corporate security policy mandates that data can **only be transported within the AWS's private network.** 

Which steps would satisfy the security policy?

- A: Enable Amazon Redshift Enhanced VPC Routing.
- B: Create a Cluster Security Group to allow the Amazon Redshift cluster to access Amazon S3.
- C: Create a NAT gateway in a public subnet to allow the Amazon Redshift cluster to access Amazon S3.
- D: Create and configure an Amazon S3 VPC endpoint.

#### *Answer: A & D*

Amazon Redshift Enhanced VPC Routing provides VPC resources access to Redshift.

Redshift will not be able to access the S3 VPC endpoints without enabling Enhanced VPC routing. So one option will not support the scenario if another is not selected.

NAT instance (the proposed answer) cannot be reached by Redshift without enabling Enhanced VPC Routing. [AWS RedShift Enhanced VPC Routing](https://aws.amazon.com/about-aws/whats-new/2016/09/amazon-redshift-now-supports-enhanced-vpc-routing/)

VPC Endpoints - It enables you to privately connect your VPC to the supported AWS Services and VPC Endpoint services powered by PrivateLink without requiring an IGW, NAT Device, VPN Connection or AWS Direct Connect connections. Instances in VPC do not require Public IP addresses to communicate with resources in the service and traffic between your VPC and other service does not leave the Amazon network.

S3 VPC Endpoint - it is a feature that will allow you to make even better use of VPC and S3.

### Question 21

A team is building an application that must persist and index JSON data in a highly available data store. The latency of data access must remain consistent despite very high application traffic.

Which service would help the team to meet the above requirement?

- A: Amazon EFS
- B: Amazon Redshift
- C: DynamoDB
- D: AWS CloudFormation

#### *Answer: C*

Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability.

The data in DynamoDB is stored in JSON format. Hence it is the perfect data storage to meet the requirement mentioned in the question.

[AWS DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html)

### Question 22 

An organization hosts a multi-language website on AWS, which is served using CloudFront. Language is specified in the HTTP request as shown below:

- http://d11111f8.cloudfront.net/main.html?language=de 
- http://d11111f8.cloudfront.net/main.html?language=en 
- http://d11111f8.cloudfront.net/main.html?language=es 

How should AWS CloudFront be configured to deliver cached data in the correct language?

- A: Forward cookies to the origin 
- B: Based on query string parameters
- C: Cache objects at the origin
- D: Serve dynamic content

#### *Answer: B*

Since language is specified in the query string parameters, CloudFront should be configured for the same.
For more information on configuring CloudFront via query string parameters, please visit the following URL: [AWS CloudFront Query String](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/QueryStringParameters.html)

### Question 23 

You have developed a new web application on AWS for a real estate firm. It has a web interface where real estate employees upload photos of newly constructed houses in S3 buckets. Prospective buyers log in to the website and access photos. The marketing team has initiated an intensive marketing event to promote new housing schemes which will lead to customers who frequently access these images. As this is a new application, you have no projection of traffic on the S3 bucket. You need an S3 storage class that can automatically optimize the storage costs with changing access patterns. Which of the following is a recommended storage solution to meet this requirement?

- A: Use One Zone-IA storage class to store all images.
- B: Use Standard-IA to store all images.
- C: Use S3 Intelligent-Tiering storage class.
- D: Use Standard storage class and use Storage class analytics to identify & move objects using lifecycle policies.

#### *Answer: C*

When the access pattern to web applications using S3 storage buckets is unpredictable, you can use S3 intelligent-Tiering storage class. S3 Intelligent-Tiering storage class includes two access tiers: frequent access and infrequent access. Based upon access patterns, it moves data between these tiers, which helps in cost saving. S3 Intelligent-Tiering storage class has the same performance as that of Standard storage class.

**Option A is incorrect.** Although it will save costs, it will not provide any protection in case of AZ failure. Also, this class is suitable for infrequently accessed data & not for frequently access data.

**Option B is incorrect** as Standard-IA storage class is for infrequently accessed data & there are retrieval charges associated. In the above requirement, you do not know the data access pattern, which may result in a higher cost.

**Option D is incorrect.** It has operational overhead to set up Storage class analytics & moves objects between various classes. Also, since the access pattern is undetermined, this will run into a costlier option.

### Question 24

You are part of the IT team of an assurance company. You have been having a consistent amount of usage of your EC2 instances and Fargate. However, there is also a consistent amount of usage increase. Because of this, you can predict that you may need to increase the size of the instances in 2 or 3 years. The finance team has asked you if there is a way to save costs in the EC2 instances and Fargate. What do you suggest?

- A: Purchase a Compute Saving plan.
- B: Purchase an EC2 instance saving plan.
- C: Purchase a Convertible Reserved Instance.
- D: Purchase a Standard Reserved Instance.

#### *Answer: A*

**Option A is correct.** With a Compute Saving Plan, you can save up to 66% and it applies to Fargate and EC2 instances. It also lets you change the instance's family and size. More details-[AWS Savings Plan](https://aws.amazon.com/savingsplans/faq/)

**Option B is incorrect.** The EC2 instance saving plan does not automatically apply to Fargate instances. 

**Option C and D are incorrect.** Reserved instances do not save the cost of Fargate. [AWS Reserved Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-reserved-instances.html)

### Question 25 

A company is generating large datasets with millions of rows to be summarized column-wise. To build daily reports from these data sets, Business Intelligence tools would be used.

Which storage service would meet these requirements?

- A: Amazon Redshift
- B: Amazon RDS
- C: ElasticCache
- D: DynamoDB

#### *Answer: A*

Amazon Redshift is a fully managed, petabyte-scale data warehouse service in the cloud. You can start with just a few hundred gigabytes of data and scale to a petabyte or more. This enables you to use your data to acquire new insights for your business and customers. [AWS Redshift](https://docs.aws.amazon.com/redshift/latest/mgmt/welcome.html)

Columnar storage for database tables is an important factor in optimizing analytic query performance because it drastically reduces the overall disk I/O requirements and the amount of data you need to load from disk. Amazon Redshift uses a block size of 1 MB, which is more efficient and further reduces the number of I/O requests needed to perform any database loading or other operations that are part of query execution.[AWS Columnar Storage](https://docs.aws.amazon.com/redshift/latest/dg/c_columnar_storage_disk_mem_mgmnt.html)

### Question 26 

A company is developing a web application to be hosted in AWS. This application needs a data store for session data.

As an AWS Solution Architect, what would you recommend as an ideal option to store session data? (SELECT TWO)

- A: CloudWatch
- B: DynamoDB
- C: Elastic Load Balancing
- D: ElasticCache
- E: Storage Gateway

#### *Answer: B & D*

DynamoDB and ElastiCache are perfect options for storing session data.

Amazon DynamoDB is a fast and flexible NoSQL database service for all applications that need consistent, single-digit millisecond latency at any scale. It is a fully managed cloud database and supports both document and key-value store models. Its flexible data model, reliable performance, and automatic scaling of throughput capacity make it a great fit for mobile, web, gaming, ad tech, IoT, and many other applications.

AWS ElastiCache is a web service that makes it easy to set up, manage, and scale a distributed in-memory data store or cache environment in the cloud. It provides a high-performance, scalable, and cost-effective caching solution while removing the complexity associated with the deployment and management of a distributed cache environment.

### Question 27 

A company needs to store images that are uploaded by users via a mobile application. There is also a need to ensure that security measures are in place to avoid data loss.

What step should be taken for protection against unintended user actions?

- A: Store data in an EBS volume and create snapshots once a week.
- B: Store data in an S3 bucket and enable versioning.
- C: Store data on Amazon EFS storage.
- D: Store data on EC2 instance storage.

#### *Answer: B*

Amazon S3 has an option for versioning, as shown below. Versioning is on the bucket level and can be used to recover prior versions of an object.

### Question 28 

An application needs to have a relational Datastore hosted in AWS. The following requirements are in place for the Datastore:

a) The initial storage capacity of 8 table

b) The ability to accommodate a database growth of 8GB per day 

c) The ability to have 4 Read Replicas

Which of the following Datastore is the best for this requirement?

- A: DynamoDB
- B: Amazon S3 
- C: Amazon Aurora
- D: ElasticCache

#### *Answer: C*

Aurora can have a storage limit of 64TB and can easily accommodate the initial 8TB plus a database growth of 8GB/day for nearly a period of 20+ years. It can have up to 15 Aurora Replicas that can be distributed across the Availability Zones that a DB cluster spans within an AWS Region.

Aurora Replicas work well for read scaling because they are fully dedicated to read operations on the cluster volume. Write operations are managed by the primary instance. Because the cluster volume is shared among all DB instances in your DB cluster, no additional work is required to replicate a copy of each Aurora Replica data. [AWS Aurora Replication](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Aurora.Replication.html)

### Question 29 

There is a requirement to host a database on an EC2 Instance. It is also required that the EBS volume should support 32,000 IOPS.

Which Amazon EBS volume type would meet the performance requirements of this database?

- A: EBS Provisioned IOPS SSD
- B: EBS Throughput Optimized HDD
- C: EBS General Purpose SSD
- D: EBS Cold HDD

#### *Answer: C*

For high performance and high IOPS requirements, as in this case, the ideal choice would be to choose EBS Provisioned IOPS SSD.
Even though general purpose IO2 Block Express meets the requirement of 32,000 IOPS, but key word is to run database service on EC2, Provisioned IOPS SSD is more desirable. 

### Question 30 

In your organization, development teams use S3 buckets to store log files for various applications hosted in AWS development environments. The developers intend to keep the logs for a month for troubleshooting purposes and subsequently purge the logs.

Which feature should be used to enable this requirement?

- A: Adding a bucket policy on the S3 bucket.
- B: Configuring lifecycle configuration rules on the S3 bucket.
- C: Creating an IAM policy for the S3 bucket.
- D: Enabling CORS on the S3 bucket.

#### *Answer: B*

### Question 31 

You are creating a new architecture for a financial firm. The architecture consists of some EC2 instances of different types and sizes. The management team has asked you to create this architecture by ensuring the reduction of the risk of simultaneous failures. Which placement group option could you suggest for the instances?

- A: Clustered Placement group
- B: Partition Placement Group 
- C: Multi-AZ Placement group
- D: Spread Placement Group 

#### *Answer: D*

**Option A is incorrect.** In Clustered Placement Groups, all the instances are placed in the same rack in the same availability zone. Therefore, they are very susceptible to hardware failures and simultaneous failures. Also, it is suggested to have the same size and types of instances in this Placement Group. More details-[AWS EC2 placement groups](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html)

**Option B is incorrect.** In partition placement groups, the chances of hardware failures and simultaneous failure are reduced compared to the Clustered placement group. Still, the Spread Placement group has fewer chances of this kind of failure. It is also suggested to have the same size and types of instances in this Placement Group.

**Option C is incorrect.** There is no Multi-AZ placement group.

**Option D is correct.** Spread Placement Groups place the instances in different racks. Every rack has its own hardware and power source. So, there is a minimum chance of simultaneous failure.

### Question 32 

You are creating a new architecture for a financial firm. The architecture consists of some EC2 instances with the same type and size (M5.large). In this architecture, all the EC2 mostly communicate with each other. Business people have asked you to create this architecture keeping in mind low latency as a priority. Which placement group option could you suggest for the instances?

- A: Partition Placement Group 
- B: Clustered Placement Group 
- C: Spread Placement Group 
- D: Enhanced Networking Placement Group 

#### *Answer: B*

*Refer to previous question explanation*

### Question 33 

A company has a media processing application deployed in a local data center. Its file storage is built on a Microsoft Windows file server. The application and file server need to be migrated to AWS. You want to set up the file server in AWS quickly. The application code should continue working to access the file systems. Which method should you choose to create the file server?

- A: Create a Windows File Server from Amazon WorkSpaces.
- B: Configure a high performance Windows File System in Amazon EFS.
- C: Create a Windows File Server in Amazon FSx.
- D: Configure a secure enterprise storage through Amazon WorkDocs.

#### *Answer: C*

In this question, a Windows file server is required in AWS, and the application should continue to work unchanged. Amazon FSx for Windows File Server is the correct answer as it is backed by a fully native Windows file system. [AWS Windows Guide](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/what-is.html)

**Option A is incorrect.** Because Amazon WorkSpace configures a desktop server which is not required in this question. Only a Windows file server is needed.

**Option B is incorrect.** Because EFS cannot be used to configure a Windows file server.

**Option D is incorrect.** Because Amazon WorkDocs is a file sharing service in AWS. It cannot provide a native Windows file system.

### Question 34 

There is a requirement to get the source IP addresses that access resources in a private subnet. Which of the following cost-optimized service could be used to fulfill this purpose?

- A: Trusted Advisor
- B: VPC FLow Logs 
- C: Use CloudWatch metrics
- D: Use CloudTrail

#### *Answer: B*

VPC Flow Logs is a feature that enables you to capture information about the IP traffic going to and from network interfaces in your VPC. Flow log data is stored using Amazon CloudWatch Logs. After you've created a flow log, you can view and retrieve its data in Amazon CloudWatch Logs. [AWS VPN Flow Logs](https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/flow-logs.html)

**Option A is incorrect.** Because AWS Trusted Advisor is your customized cloud expert! It helps you observe the best practices for using AWS by inspecting your AWS environment to save money, improve system reliability and performance, and close security gaps.

**Option C is incorrect.** Because CloudWatch metric is mainly used for performance metrics and cannot provide the source IP address.

**Option D is incorrect.** Because AWS CloudTrail is a service that enables governance, compliance and operational auditing, and risk auditing of your account. With CloudTrail, you can log, continuously monitor and retain account activity related to actions across your AWS infrastructure. However it is costly to use CloudTrail. [AWS CloudTrail Endpoint Support](https://aws.amazon.com/about-aws/whats-new/2018/08/aws-cloudtrail-adds-vpc-endpoint-support-to-aws-privatelink/#:~:text=This%20enables%20you%20to%20connect,VPC%20through%20the%20Amazon%20network.&text=By%20using%20AWS%20CloudTrail%20with,your%20compliance%20and%20regulatory%20requirements)

### Question 35 

You are part of the IT team of a small car manufacturer company. The company is starting to move its On-Premise resources to the cloud. The Marketing department was the first department to migrate its applications to the cloud. Now the finance team wants to do the same. Each department should have its own AWS account but you need one management account to pay for the bills of all the AWS accounts. What do you suggest to solve this?

- A: Create a different VPC for the Finance Department and limit their access to resources with IAM Roles and Policies.
- B: Use AWS Control Tower
- C: Use AWS Organizations to manage both AWS accounts.
- D: Use AWS Cost Explorer to divide the bills and use IAM policies to limit the access to resources.

#### *Answer: C*

With AWS Organizations, you can have separate bills for every account and pay it with the same account using consolidating billing. More details: https://aws.amazon.com/organizations/faqs/.

### Question 36 

Your team is developing a high-performance computing (HPC) application. The application resolves complex, compute-intensive problems and needs a high-performance and low-latency Lustre file system. You need to configure this file system in AWS at a low cost. Which method is the most suitable?

- A: Create a Lustre file system through Amazon FSx.
- B: Launch a high performance Lustre file system in Amazon EBS.
- C: Create a high-speed volume cluster in EC2 placement group.
- D: Launch the Lustre file system from AWS Marketplace.

#### *Answer: A*

The Lustre file system is an open-source, parallel file system that can be used for HPC applications. Refer to [Lustre](http://lustre.org/)  for its introduction. In Amazon FSx, users can quickly launch a Lustre file system at a low cost.

**Option B is incorrect.** Although users may be able to configure a Lustre file system through EBS, it needs lots of extra configurations. Option A is more straightforward.

### Question 37 

A Redshift cluster currently contains 60TB of data. There is a requirement that a disaster recovery site is put in place in another region. Which solution would help ensure that this requirement is fulfilled?

- A: Take a copy of the underlying EBS volumes to S3, and then do Cross-Region Replication.
- B: Enable Cross-Region snapshots for the Redshift Cluster.
- C: Create a CloudFormation template to restore the Cluster in another region.
- D: Enable Cross Availability Zone snapshots for the Redshift Cluster.

#### *Answer: B*

You can configure cross-regional snapshots when you want Amazon Redshift to automatically copy snapshots (automated or manual) to another region for backup purpose. Note that copying snapshots from source region to a destination region incurs data transfer charges. [AWS Redshift Cross Regional Snapshot](https://docs.aws.amazon.com/redshift/latest/mgmt/managing-snapshots-console.html)

### Question 38

A company is using a Redshift cluster to store its data warehouse. There is a requirement from the Internal IT Security team to encrypt data in the Redshift database. How could this be achieved? (SELECT TWO)

- A: Encrypt the EBS volumes of the underlying EC2 Instances.
- B: Use AWS KMS Customer Default master key.
- C: Use SSL/TLS for encrypting the data.
- D: Use hardware security module (HSM) to manage the top-level encryption keys.

#### *Answer: *

