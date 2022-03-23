# CSAA Practice Test 0

### Question 1 

Your company is planning on the following architecture for their application.

- A set of EC2 Instances hosting the web part of the application.
- A relational database for the backend.
- A Load balancer for distribution of traffic.
- A NAT gateway for routing traffic from the database server to the Internet.

Which of the following architecture ensures high availability across all components?

- A: A Load balancer with one public subnet, one private subnet. The EC2 Instances placed in one Availability Zone. RDS with Multi-AZ Enabled. NAT Gateway in one availability zone.
- B: A Load balancer with 2 public subnets, 2 private subnets. The EC2 Instances placed across 2 Availability Zones. RDS with Multi-AZ Enabled. NAT Gateways in each availability zone.
- C: A Load balancer with 2 public subnets, 2 private subnets. The EC2 Instances placed in 2 Availability Zones. RDS with Multi-AZ Enabled. NAT Gateway in one availability zone.
- D: A Load balancer with 2 public subnets, 2 private subnets. The EC2 Instances placed in one Availability Zone. RDS with Multi-AZ Enabled. NAT Gateway in one availability zone.

#### *Answer: B*

In a Multi-AZ deployment, Amazon RDS automatically provisions and maintains a synchronous standby replica in a different Availability Zone. Running a DB instance with high availability can enhance availability during planned system maintenance and help protect your databases against DB instance failure and Availability Zone disruption.

Option A is incorrect because High Availability is not ensured.
We recommend that you enable multiple Availability Zones. With this configuration, if one Availability Zone becomes unavailable or has no healthy targets, the load balancer can continue to route traffic to the healthy targets in another Availability Zone.

Option B is Correct because High Availability is ensured.
If one of the AZs should fail, then the EC2 instances in the remaining private subnet will still be able to communicate with the Internet because they have their own NAT Gateway in the same AZ.

Options C and D are incorrect because High Availability is not ensured as either if we have EC2 in a single AZ or multiple AZ. We have NAT Gateway in single AZ is a cause for not ensuring High Availability.

However, if there is a failure with Availability Zone A (rare, but can happen), then the NAT Gateway is not reachable from Private-Subnet-B. Thus, the system may be impacted even though it runs across two AZs or a single AZ.

### Question 2

An AWS Solutions Architect designing a solution to store and archive corporate documents has determined Amazon Glacier as the right choice. 

An important requirement is that the data must be delivered within 5 minutes of a retrieval request.

Which feature in Amazon Glacier could help to meet this requirement?

- A: Vault Lock
- B: Expedited retrieval
- C: Bulk retrieval
- D: Standard retrieval

#### *Answer: B*

Expedited retrievals allow you to access data in 1–5 minutes for a flat rate of $0.03 per GB retrieved. Expedited retrievals allow you to quickly access your data when occasional urgent requests for a subset of archives are required.

The Vault Lock and Standard Retrieval are standard with 3-5 hours retrieval time while Bulk retrievals which can be considered the cheapest option have 5-12 hours retrieval time. 

### Question 3

A Solutions Architect is designing a highly scalable system to track records. These records must remain available for immediate download for up to three months and then must be deleted. What is the most appropriate decision for this use case?

- A: Store the files in Amazon EBS and create a Lifecycle Policy to remove files after 3 months.
- B: Store the files in Amazon S3 and create a Lifecycle Policy to remove files after 3 months.
- C: Store the files in Amazon Glacier and create a Lifecycle Policy to remove files after 3 months.
- D: Store the files in Amazon EFS and create a Lifecycle Policy to remove files after 3 months.

#### *Answer: B*

Lifecycle configuration enables you to specify the Lifecycle Management of objects in a bucket. The configuration is a set of one or more rules, where each rule defines an action for Amazon S3 to apply to a group of objects. These actions can be classified as follows:

Transition actions – In which you define when the transition of the object occurs to another storage class. For example, you may choose to transition objects to the STANDARD_IA (IA, for infrequent access) storage class 30 days after creation or archive objects to the GLACIER storage class one year after creation.

Expiration actions – In which you specify when the objects will expire. Then Amazon S3 deletes the expired objects on your behalf.

Option A is incorrect since the records need to be stored in a highly scalable system.

Option C is incorrect since the records must be available for immediate download.

Option D is incorrect since EFS lifecycle management is used to migrate files that have not been accessed for a certain period of time to the Infrequent Access storage class. Files moved to this storage remain indefinitely and not get deleted. And due to this reason, this option is not correct.

### Question 4 

You have developed a new web application on AWS for a real estate firm. It has a web interface where real estate employees upload photos of newly constructed houses in S3 buckets. Prospective buyers log in to the website and access photos. The marketing team has initiated an intensive marketing event to promote new housing schemes which will lead to customers who frequently access these images. As this is a new application, you have no projection of traffic on the S3 bucket. You need an S3 storage class that can automatically optimize the storage costs with changing access patterns. Which of the following is a recommended storage solution to meet this requirement? 

- A: Use One Zone-IA storage class to store all images.
- B: Use Standard-IA to store all images.
- C: Use S3 Intelligent-Tiering storage class.
- D: Use Standard storage class and use Storage class analytics to identify & move objects using lifecycle policies.

#### *Answer: C*

When the access pattern to web applications using S3 storage buckets is unpredictable, you can use S3 intelligent-Tiering storage class. S3 Intelligent-Tiering storage class includes two access tiers: frequent access and infrequent access. Based upon access patterns, it moves data between these tiers, which helps in cost saving. S3 Intelligent-Tiering storage class has the same performance as that of Standard storage class.

Option A is incorrect. Although it will save costs, it will not provide any protection in case of AZ failure. Also, this class is suitable for infrequently accessed data & not for frequently access data.

Option B is incorrect as Standard-IA storage class is for infrequently accessed data & there are retrieval charges associated. In the above requirement, you do not know the data access pattern, which may result in a higher cost.

Option D is incorrect. It has operational overhead to set up Storage class analytics & moves objects between various classes. Also, since the access pattern is undetermined, this will run into a costlier option.

### Question 5 

You host a static website in an S3 bucket, and there are global clients from multiple regions. You want to use an AWS service to store cache for frequently accessed content so that the latency is reduced and the data transfer rate increases. Which of the following options would you choose?

- A: Use AWS SDKs to horizontally scale parallel requests to the Amazon S3 service endpoints.
- B: Create multiple Amazon S3 buckets and put Amazon EC2 and S3 in the same AWS Region.
- C: Enable Cross-Region Replication to several AWS Regions to serve customers from different locations.
- D: Configure CloudFront to deliver the content in the S3 bucket.

#### *Answer: D*

CloudFront can store the frequently accessed content as a cache, and the performance is optimized. Other options may help with the performance. However, they do not store cache for the S3 objects.

Option A is incorrect: This option may increase the throughput. However, it does not store cache.

Option B is incorrect: Because this option does not use cache.

Option C is incorrect: This option creates multiple S3 buckets in different regions. It does not improve the performance using cache.

Option D is CORRECT: Because CloudFront caches copies the S3 files in its edge locations. Users are routed to the edge location that has the lowest latency.

### Question 6

You have planned to host a web application on AWS. You create an EC2 Instance in a public subnet that needs to connect to an EC2 Instance that will host an Oracle database. Which steps would ensure a secure setup? (SELECT TWO)

- A: Place the EC2 Instance with the Oracle database in the same public subnet as the Webserver for faster communication.
- B: Place the ec2 instance that will host the Oracle database in a private subnet.
- C: Create a database Security group which allows incoming traffic only from the Web server's security group.
- D: Ensure that the database security group allows incoming traffic from 0.0.0.0/0.

#### *Answer: B & C*

Correct Answer – B and C

The best and most secure option is to place the database in a private subnet. The below diagram from AWS Documentation shows this setup. Also, you ensure that access is not allowed from all sources but only from the web servers.

Option A is incorrect because DB instances are placed in Private subnets and allowed to communicate with web servers in the public subnet as per the best practice guidelines. 

Option D is incorrect because allowing all incoming traffic from the Internet to the DB instance is a security risk.

### Question 7 

Your company needs to develop an application that needs to have a login module in place. Their key requirement is to ensure that users can also use their current identities with various providers such as Facebook to log into the application. Which of the following can help you accomplish this?

- A: Using the AWS Cognito service
- B: Using the AWS Config service
- C: Using the AWS SQS service
- D: Using the AWS WAF service

#### *Answer: A*

The AWS Documentation mentions the following.

Amazon Cognito provides authentication, authorization, and user management for your web and mobile apps. Your users can sign in directly with a user name and password, or through a third party such as Facebook, Amazon, or Google.

The two main components of Amazon Cognito are user pools and identity pools. User pools are user directories that provide sign-up and sign-in options for your app users. Identity pools enable you to grant your users access to other AWS services. You can use identity pools and user pools separately or together.

Option B is incorrect since this is a configuration service.

Option C is incorrect since this is a messaging service.

Option D is incorrect since this is a web application firewall service.

[AWS Cognito](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html)

### Question 8 

A company currently hosts a Redshift cluster in AWS. It should ensure that all traffic from and to the Redshift cluster does not go through the Internet for security reasons. Which features can be used to fulfill this requirement in an efficient manner?

- A: Enable Amazon Redshift Enhanced VPC Routing.
- B: Create a NAT Gateway to route the traffic.
- C: Create a NAT Instance to route the traffic.
- D: Create a VPN Connection to ensure traffic does not flow through the Internet.

#### *Answer: A*

Correct Answer - A

AWS Documentation mentions the following: 

When you use Amazon Redshift Enhanced VPC Routing, Amazon Redshift forces all COPY and UNLOAD traffic between your cluster and your data repositories through your Amazon VPC.

If Enhanced VPC Routing is not enabled, Amazon Redshift routes traffic through the Internet, including traffic to other services within the AWS network.

### Question 9 

You have implemented AWS Cognito services to require users to sign in and sign up to your app through social identity providers like Facebook, Google, etc. Your marketing department wants users to anonymously try out the app because the current log-in requirement is excessive, which may reduce the demand for products and services offered through the app. What would you suggest to the marketing department in this regard?

- A: It’s too much of a security risk to allow unauthenticated users access to the app.
- B: Cognito Identity supports guest users for the ability to enter the app and have limited access.
- C: A second version of the app will need to be offered for unauthenticated users.
- D: This is possible only if we remove the authentication from everywhere.

#### *Answer: B*

Option B is correct. Amazon Cognito Identity Pools can support unauthenticated identities by providing a unique identifier and AWS credentials for users who do not authenticate with an identity provider. Unauthenticated users can be associated with a role with limited access to resources compared to a role for authenticated users.

Option A is incorrect. Cognito will allow unauthenticated users without being a security risk.

Option C is incorrect. Cognito supports both authenticated and unauthenticated users.

### Question 10 

You have created an AWS Lambda function that will write data to a DynamoDB table. Which of the following must be in place to ensure that the Lambda function can interact with the DynamoDB table?

- A: Ensure an IAM Role is attached to the Lambda function which has the required DynamoDB privileges.
- B: Ensure an IAM User is attached to the Lambda function which has the required DynamoDB privileges.
- C: Ensure the Access keys are embedded in the AWS Lambda function.
- D: Ensure the IAM user password is embedded in the AWS Lambda function.

#### *Answer: A*

AWS Documentation mentions the following to support this requirement:

Each Lambda function has an IAM role (execution role) associated with it. You specify the IAM role when you create your Lambda function. Permissions you grant to this role determine what AWS Lambda can do when it assumes the role. There are two types of permissions that you grant to the IAM role:

If your Lambda function code accesses other AWS resources, such as reading an object from an S3 bucket or writing logs to CloudWatch Logs, you need to grant permissions for relevant Amazon S3 and CloudWatch actions to the role.

If the event source is stream-based (Amazon Kinesis Data Streams and DynamoDB streams), AWS Lambda polls these streams on your behalf. AWS Lambda needs permissions to poll the stream and read new records on the stream. So you need to grant the relevant permissions to this role.
