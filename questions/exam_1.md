# CSAA Practice Test 1

### Question 10

You are working for a start-up company that develops mobile gaming applications using AWS resources. For creating AWS resources, the project team is using CloudFormation Templates. The Project Team is concerned about the changes made in EC2 instance properties by the Operations Team, apart from parameters specified in CloudFormation Templates. To observe changes in AWS EC2 instance, you advise using CloudFormation Drift Detection. After Drift detection, when you check drift status for all AWS EC2 instances, drift for certain property values with default values for resource properties is not displayed. What would you do to include these resource properties to be captured in CloudFormation Drift Detection?

- [A]: Run CloudFormation Drift Detection on individual stack resources instead of entire CloudFormation stack.
- [B]: Explicitly set the property value, which can be the same as the default value.
- [C]: Manually check these resources as this is not supported in CloudFormation Drift Detection.
- [D]: Assign Read permission to CloudFormation Drift Detection to determine drift.

#### *Answer: B*

AWS CloudFormation Drift Detection can be used to detect changes made to AWS resources outside the CloudFormation Templates. AWS CloudFormation Drift Detection only checks property values explicitly set by stack templates or by specifying template parameters. It does not determine drift for property values that are set by default. To determine drift for these resources, you can explicitly set property values that can be the same as that of the default value.

**Option A is incorrect.** If property values are assigned explicitly to these properties, running AWS CloudFormation Drift Detection would be detected in both individuals and the entire CloudFormation Stack.

**Option C is incorrect.** CloudFormation Drift Detection supports the AWS EC2 instance.

**Option D is incorrect.** Since for all other resources, CloudFormation Drift Detection has already determined drift, there is no other read permission to be granted further.

For more information on AWS CloudFormation Drift Detection, refer to [AWS CloudFormation Drift Detection](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-stack-drift.html)

### Question 11

You are responsible for performing a migration from your company's on-premise data to the AWS cloud. You have about 400 GB of data stored in an NFS. One requirement of this migration is to transfer some of this data to AWS EFS and the other part to S3. Which is the easiest to use and with the most cost-effective solution?

- [A]: Use AWS Storage gateway.
- [B]: Use S3 Transfer Acceleration.
- [C]: Use S3 DataSync.
- [D]: Use AWS Database Migration Service.

#### *Answer: C*

DataSync is a service used to transfer data between on-premise storage to AWS S3, EFS and FSx. It is cost-effective, easy to use, and can handle the transfer to EFS and S3. More details: [AWS S3 DataSync](https://aws.amazon.com/datasync/faqs/)

**Option A is incorrect.**  Storage Gateway is a hybrid cloud storage service to share and access data between your on-premise resources and AWS resources. It is not mainly designed to migrate data from On-Premise to AWS. Additionally, all three storage gateway patterns are backed by S3, not EFS. More details: [AWS Storage gateway](https://aws.amazon.com/storagegateway/faqs/)

**Option B is incorrect.**  S3 Transfer Acceleration is used to transfer data to S3 using Amazon CloudFront’s globally distributed edge locations, increasing data transfer speed. However, this option doesn't work to transfer data to AWS EFS. More details: [AWS S3](https://docs.aws.amazon.com/AmazonS3/latest/dev/transfer-acceleration.html)

**Option D is incorrect.** Because AWS Database Migration Service is used to migrate databases to AWS databases like Aurora, DynamoDB, etc. In this scenario, we don’t mention a database migration, and with this service, you can not transfer data to EFS nor S3. More details: [AWS DMS](https://aws.amazon.com/dms/)

### Question 12

A company hosts a popular web application that connects to an Amazon RDS MySQL DB instance running in a default VPC private subnet with NACL settings that was created by AWS as default. The web servers must be accessible only to customers on HTTPS connections, and the database must only be accessible to web servers in a public subnet. Which solution would meet these requirements without impacting other applications? (SELECT TWO)

- [A]: Create a network ACL on the Web Server's subnets, allow HTTPS port 443 inbound and specify the source as 0.0.0.0/0.
- [B]: Create a Web Server security group that allows HTTPS port 443 inbound traffic from anywhere (0.0.0.0/0) and apply it to the Web Servers.
- [C]: Create a DB Server security group that allows MySQL port 3306 inbound and specify the source as the Web Server security group.
- [D]: Create a network ACL on the DB subnet, allow MySQL port 3306 inbound for Web Servers and deny all outbound traffic.
- [E]: Create a DB Server security group that allows HTTPS port 443 inbound and specify the source as a Web Server security group.

#### *Answer: B & C*

1) To ensure that traffic can flow into your webserver from anywhere on secure traffic, you need to allow inbound security at 443.

2) And then, you need to ensure that traffic can flow from the webserver to the database server via the database security group.

### Question 13

You lead a team to develop a new web application in AWS EC2. The application will have a large number of users globally. For a great user experience, this application requires very low network latency and jitter. If the network speed is not fast enough, you will lose customers. Which tool would you choose to improve the application performance? (Select TWO.)

- [A]: AWS VPN
- [B]: AWS Global Accelerator
- [C]: Direct connect
- [D]: API Gateway
- [E]: CloudFront

#### *Answer: B & E*

This web application has global users and needs low latency. Both CloudFront and Global Accelerator can speed up the distribution of contents over the AWS global network.

**Option A is incorrect.** AWS VPN links on-premise network to AWS network. However, no on-premise services are mentioned in this question.

**Option B is correct.** AWS Global Accelerator works at the network layer and can direct traffic to optimal endpoints. For reference, check the link. [AWS Global Accelerator](https://docs.aws.amazon.com/global-accelerator/latest/dg/what-is-global-accelerator.html)

**Option C is incorrect.** Direct Connect links on-premise network to AWS network. However, no on-premise services are mentioned in this question.

**Option D is incorrect.** API Gateway is a regional service and cannot improve the application performance. API Gateway is suitable for serverless applications such as Lambda.

**Option E is correct.** Because CloudFront delivers content through edge locations, and users are routed to the edge location with the lowest time delay.

### Question 14

You are deploying an application on Amazon EC2 that must call AWS APIs. Which method would you use to allow the application access to the APIs securely?

- [A]: Pass API credentials to the instance using Instance userdata.
- [B]: Store API credentials as an object in Amazon S3.
- [C]: Embed the API credentials into your application.
- [D]: Assign IAM roles to the EC2 Instances.

#### *Answer: D*

You can use roles to delegate access to users, applications, or services that don't normally have access to your AWS resources. It is not a good practice to use IAM credentials for a production-based application. However, it is a good practice to use IAM Roles. [AWS IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)

### Question 15

A website runs on EC2 Instances behind an Application Load Balancer. The instances run in an Auto Scaling Group across multiple Availability Zones and deliver several static files stored on a shared Amazon EFS file system. The company needs to avoid serving the files from EC2 Instances every time a user requests these digital assets.

What should the company do to improve the user experience of the website?

- [A]: Move the digital assets to Amazon Glacier.
- [B]: Cache static content using CloudFront.
- [C]: Resize the images so that they are smaller.
- [D]: Use reserved EC2 Instances.

#### *Answer: B*

Amazon CloudFront is a web service that speeds up distribution of your static and dynamic web content, such as .html, .css, .js, and image files to your users. CloudFront delivers your content through a worldwide network of data centers called edge locations. When a user requests content that you're serving with CloudFront, the user is routed to the edge location that provides the lowest latency (time delay), so that the content is delivered with the best possible performance. If the content is already in the edge location with the lowest latency, CloudFront delivers it immediately. [AWS CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)

In addition, the glacier is not used for frequent retrievals. So Option A is not a good solution. Options C & D will also not help in this situation.

### Question 16

A Solutions Architect is designing a highly scalable system to track records. These records must remain available for immediate download for up to three months and then must be deleted. What is the most appropriate decision for this use case?

- [A]: Store the files in Amazon EBS and create a Lifecycle Policy to remove files after 3 months.
- [B]: Store the files in Amazon S3 and create a Lifecycle Policy to remove files after 3 months.
- [C]: Store the files in Amazon Glacier and create a Lifecycle Policy to remove files after 3 months.
- [D]: Store the files in Amazon EFS and create a Lifecycle Policy to remove files after 3 months.

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

- [A]: AWS Beanstalk
- [B]: AWS CloudFormation
- [C]: AWS CodeBuild
- [D]: AWS CodeDeploy

#### *Answer: B*

AWS Documentation mentions the following on AWS CloudFormation:

AWS CloudFormation is a service that helps you model and set up your Amazon Web Service resources so that you can spend less time managing those resources and more time focusing on your applications that run in AWS. You create a template that describes all the AWS resources that you want (like Amazon EC2 instances or Amazon RDS DB instances), and AWS CloudFormation takes care of provisioning and configuring those resources for you. [AWS CloudFormation user guide](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)

AWS Elastic Beanstalk is an easy-to-use service for deploying and scaling web applications and services developed with Java, .NET, PHP, Node.js etc. You can upload your code, and Elastic Beanstalk automatically handles the deployment, from capacity provisioning, load balancing, auto-scaling to application health monitoring.

In question mentioned that "A consulting firm **repeatedly builds large architectures for their customers using AWS resources from several AWS services including IAM, Amazon EC2, Amazon RDS, DynamoDB and Amazon VPC.**

When you are building large architectures repeatedly, you can use the CloudFormation template to create or modify an existing AWS CloudFormation template. A template describes all of your resources and their properties. When you use that template to create an AWS CloudFormation stack, AWS CloudFormation provisions the Auto Scaling group, load balancer, and database for you. After the stack has been successfully created, your AWS resources are up and running. You can delete the stack just as easily, which deletes all the resources in the stack. By using AWS CloudFormation, you easily manage a collection of resources as a single unit. Whenever working with more number of AWS resources together, CloudFormation is the best option.

### Question 18

The security policy of an organization requires an application to encrypt data before writing to the disk. Which solution should the organization use to meet this requirement?

- [A]: AWS KMS API
- [B]: AWS Certificate Manager
- [C]: API Gateway with STS
- [D]: IAM Access Key

#### *Answer: A*

**Option B is incorrect.** The AWS Certificate Manager can be used to generate SSL certificates to encrypt traffic in transit, but not at rest.

**Option C is incorrect.** It is used for issuing tokens while using the API gateway for traffic in transit.

Option D is used for providing secure access to EC2 Instances. (Or sometimes other AWS resources)

AWS Key Management Service (AWS KMS) is a managed service that makes it easy for you to create and control the encryption keys used to encrypt your data. AWS KMS is integrated with other AWS services including Amazon Elastic Block Store (Amazon EBS), Amazon Simple Storage Service (Amazon S3), Amazon Redshift, Amazon Elastic Transcoder, Amazon WorkMail, Amazon Relational Database Service (Amazon RDS), and others to make it simple to encrypt your data with encryption keys that you manage.

[AWS KMS user guid](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html)
[AWS KMS API references](https://docs.aws.amazon.com/kms/latest/APIReference/kms-api-reference.pdf#Welcome)

### Question 19

You are an AWS Solutions Architect. Your company has a successful web application deployed across multiple AWS Regions. The application attracts more and more global customers. However, the application’s performance is impacted. Your manager asks you how to improve the performance and availability of the application. Which of the following AWS services would you recommend?

- [A]: AWS DataSync
- [B]: Amazon DynamoDB Accelerator
- [C]: AWS Lake Formation
- [D]: AWS Global Accelerator

#### *Answer: D*

AWS Global accelerator provides static IP addresses that are anycast in the AWS edge network. Incoming traffic is distributed across endpoints in AWS regions. The performance and availability of the application are improved. Therefore, Option D is correct, [AWS Global Accelerator use case](https://docs.aws.amazon.com/global-accelerator/latest/dg/introduction-benefits-of-migrating.html)

### Question 20

A retailer exports data daily from its transactional databases into an S3 bucket in the Sydney region. The retailer's Data Warehousing team wants to import this data into an existing Amazon Redshift cluster in their VPC in Sydney. Corporate security policy mandates that data can **only be transported within the AWS's private network.** 

Which steps would satisfy the security policy?

- [A]: Enable Amazon Redshift Enhanced VPC Routing.
- [B]: Create a Cluster Security Group to allow the Amazon Redshift cluster to access Amazon S3.
- [C]: Create a NAT gateway in a public subnet to allow the Amazon Redshift cluster to access Amazon S3.
- [D]: Create and configure an Amazon S3 VPC endpoint.

#### *Answer: A & D*

Amazon Redshift Enhanced VPC Routing provides VPC resources access to Redshift.

Redshift will not be able to access the S3 VPC endpoints without enabling Enhanced VPC routing. So one option will not support the scenario if another is not selected.

NAT instance (the proposed answer) cannot be reached by Redshift without enabling Enhanced VPC Routing. [AWS RedShift Enhanced VPC Routing](https://aws.amazon.com/about-aws/whats-new/2016/09/amazon-redshift-now-supports-enhanced-vpc-routing/)

VPC Endpoints - It enables you to privately connect your VPC to the supported AWS Services and VPC Endpoint services powered by PrivateLink without requiring an IGW, NAT Device, VPN Connection or AWS Direct Connect connections. Instances in VPC do not require Public IP addresses to communicate with resources in the service and traffic between your VPC and other service does not leave the Amazon network.

S3 VPC Endpoint - it is a feature that will allow you to make even better use of VPC and S3.

### Question 21

A team is building an application that must persist and index JSON data in a highly available data store. The latency of data access must remain consistent despite very high application traffic.

Which service would help the team to meet the above requirement?

- [A]: Amazon EFS
- [B]: Amazon Redshift
- [C]: DynamoDB
- [D]: AWS CloudFormation

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

- [A]: Forward cookies to the origin 
- [B]: Based on query string parameters
- [C]: Cache objects at the origin
- [D]: Serve dynamic content

#### *Answer: B*

Since language is specified in the query string parameters, CloudFront should be configured for the same.
For more information on configuring CloudFront via query string parameters, please visit the following URL: [AWS CloudFront Query String](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/QueryStringParameters.html)

### Question 23 

You have developed a new web application on AWS for a real estate firm. It has a web interface where real estate employees upload photos of newly constructed houses in S3 buckets. Prospective buyers log in to the website and access photos. The marketing team has initiated an intensive marketing event to promote new housing schemes which will lead to customers who frequently access these images. As this is a new application, you have no projection of traffic on the S3 bucket. You need an S3 storage class that can automatically optimize the storage costs with changing access patterns. Which of the following is a recommended storage solution to meet this requirement?

- [A]: Use One Zone-IA storage class to store all images.
- [B]: Use Standard-IA to store all images.
- [C]: Use S3 Intelligent-Tiering storage class.
- [D]: Use Standard storage class and use Storage class analytics to identify & move objects using lifecycle policies.

#### *Answer: C*

When the access pattern to web applications using S3 storage buckets is unpredictable, you can use S3 intelligent-Tiering storage class. S3 Intelligent-Tiering storage class includes two access tiers: frequent access and infrequent access. Based upon access patterns, it moves data between these tiers, which helps in cost saving. S3 Intelligent-Tiering storage class has the same performance as that of Standard storage class.

**Option A is incorrect.** Although it will save costs, it will not provide any protection in case of AZ failure. Also, this class is suitable for infrequently accessed data & not for frequently access data.

**Option B is incorrect** as Standard-IA storage class is for infrequently accessed data & there are retrieval charges associated. In the above requirement, you do not know the data access pattern, which may result in a higher cost.

**Option D is incorrect.** It has operational overhead to set up Storage class analytics & moves objects between various classes. Also, since the access pattern is undetermined, this will run into a costlier option.

### Question 24

You are part of the IT team of an assurance company. You have been having a consistent amount of usage of your EC2 instances and Fargate. However, there is also a consistent amount of usage increase. Because of this, you can predict that you may need to increase the size of the instances in 2 or 3 years. The finance team has asked you if there is a way to save costs in the EC2 instances and Fargate. What do you suggest?

- [A]: Purchase a Compute Saving plan.
- [B]: Purchase an EC2 instance saving plan.
- [C]: Purchase a Convertible Reserved Instance.
- [D]: Purchase a Standard Reserved Instance.

#### *Answer: A*

**Option A is correct.** With a Compute Saving Plan, you can save up to 66% and it applies to Fargate and EC2 instances. It also lets you change the instance's family and size. More details-[AWS Savings Plan](https://aws.amazon.com/savingsplans/faq/)

**Option B is incorrect.** The EC2 instance saving plan does not automatically apply to Fargate instances. 

**Option C and D are incorrect.** Reserved instances do not save the cost of Fargate. [AWS Reserved Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-reserved-instances.html)

### Question 25 

A company is generating large datasets with millions of rows to be summarized column-wise. To build daily reports from these data sets, Business Intelligence tools would be used.

Which storage service would meet these requirements?

- [A]: Amazon Redshift
- [B]: Amazon RDS
- [C]: ElasticCache
- [D]: DynamoDB

#### *Answer: A*

Amazon Redshift is a fully managed, petabyte-scale data warehouse service in the cloud. You can start with just a few hundred gigabytes of data and scale to a petabyte or more. This enables you to use your data to acquire new insights for your business and customers. [AWS Redshift](https://docs.aws.amazon.com/redshift/latest/mgmt/welcome.html)

Columnar storage for database tables is an important factor in optimizing analytic query performance because it drastically reduces the overall disk I/O requirements and the amount of data you need to load from disk. Amazon Redshift uses a block size of 1 MB, which is more efficient and further reduces the number of I/O requests needed to perform any database loading or other operations that are part of query execution.[AWS Columnar Storage](https://docs.aws.amazon.com/redshift/latest/dg/c_columnar_storage_disk_mem_mgmnt.html)

### Question 26 

A company is developing a web application to be hosted in AWS. This application needs a data store for session data.

As an AWS Solution Architect, what would you recommend as an ideal option to store session data? (SELECT TWO)

- [A]: CloudWatch
- [B]: DynamoDB
- [C]: Elastic Load Balancing
- [D]: ElasticCache
- [E]: Storage Gateway

#### *Answer: B & D*

DynamoDB and ElastiCache are perfect options for storing session data.

Amazon DynamoDB is a fast and flexible NoSQL database service for all applications that need consistent, single-digit millisecond latency at any scale. It is a fully managed cloud database and supports both document and key-value store models. Its flexible data model, reliable performance, and automatic scaling of throughput capacity make it a great fit for mobile, web, gaming, ad tech, IoT, and many other applications.

AWS ElastiCache is a web service that makes it easy to set up, manage, and scale a distributed in-memory data store or cache environment in the cloud. It provides a high-performance, scalable, and cost-effective caching solution while removing the complexity associated with the deployment and management of a distributed cache environment.

### Question 27 



