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

#### _Answer: B_

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

#### _Answer: B_

Expedited retrievals allow you to access data in 1–5 minutes for a flat rate of $0.03 per GB retrieved. Expedited retrievals allow you to quickly access your data when occasional urgent requests for a subset of archives are required.

The Vault Lock and Standard Retrieval are standard with 3-5 hours retrieval time while Bulk retrievals which can be considered the cheapest option have 5-12 hours retrieval time.

### Question 3

A Solutions Architect is designing a highly scalable system to track records. These records must remain available for immediate download for up to three months and then must be deleted. What is the most appropriate decision for this use case?

- A: Store the files in Amazon EBS and create a Lifecycle Policy to remove files after 3 months.
- B: Store the files in Amazon S3 and create a Lifecycle Policy to remove files after 3 months.
- C: Store the files in Amazon Glacier and create a Lifecycle Policy to remove files after 3 months.
- D: Store the files in Amazon EFS and create a Lifecycle Policy to remove files after 3 months.

#### _Answer: B_

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

#### _Answer: C_

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

#### _Answer: D_

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

#### _Answer: B & C_

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

#### _Answer: A_

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

#### _Answer: A_

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

#### _Answer: B_

Option B is correct. Amazon Cognito Identity Pools can support unauthenticated identities by providing a unique identifier and AWS credentials for users who do not authenticate with an identity provider. Unauthenticated users can be associated with a role with limited access to resources compared to a role for authenticated users.

Option A is incorrect. Cognito will allow unauthenticated users without being a security risk.

Option C is incorrect. Cognito supports both authenticated and unauthenticated users.

### Question 10

You have created an AWS Lambda function that will write data to a DynamoDB table. Which of the following must be in place to ensure that the Lambda function can interact with the DynamoDB table?

- A: Ensure an IAM Role is attached to the Lambda function which has the required DynamoDB privileges.
- B: Ensure an IAM User is attached to the Lambda function which has the required DynamoDB privileges.
- C: Ensure the Access keys are embedded in the AWS Lambda function.
- D: Ensure the IAM user password is embedded in the AWS Lambda function.

#### _Answer: A_

AWS Documentation mentions the following to support this requirement:

Each Lambda function has an IAM role (execution role) associated with it. You specify the IAM role when you create your Lambda function. Permissions you grant to this role determine what AWS Lambda can do when it assumes the role. There are two types of permissions that you grant to the IAM role:

If your Lambda function code accesses other AWS resources, such as reading an object from an S3 bucket or writing logs to CloudWatch Logs, you need to grant permissions for relevant Amazon S3 and CloudWatch actions to the role.

If the event source is stream-based (Amazon Kinesis Data Streams and DynamoDB streams), AWS Lambda polls these streams on your behalf. AWS Lambda needs permissions to poll the stream and read new records on the stream. So you need to grant the relevant permissions to this role.

### Question 11

Your company is planning to use Route 53 as the DNS provider. There is a need to ensure that the company's domain name points to an existing CloudFront distribution. How could this be achieved?

- A: Create an Alias record which points to the CloudFront distribution.
- B: Create a host record which points to the CloudFront distribution.
- C: Create a CNAME record which points to the CloudFront distribution.
- D: Create a Non-Alias Record which points to the CloudFront distribution.

#### _Answer: A_

AWS Documentation mentions the following.

While ordinary Amazon Route 53 records are standard DNS records, alias records provide a Route 53–specific extension to the DNS functionality. Instead of an IP address or a domain name, an alias record contains a pointer to a CloudFront distribution, an Elastic Beanstalk environment, an ELB Classic, Application, or Network Load Balancer, an Amazon S3 bucket that is configured as a static website, or another Route 53 record in the same hosted zone. When Route 53 receives a DNS query that matches the name and type in an alias record, Route 53 follows the pointer and responds with the applicable value. [Route Record Set](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html)

Note: Route 53 uses "Alias Name" to connect to the CloudFront as Alias Record is a Route 53 extension to DNS. Also, an Alias record is similar to a CNAME record, but the main difference is - you can create an Alias record for both root domain & subdomain. In contrast, a CNAME record can be created only to subdomain. Check the below link to get more information: [Routing to CloudFront](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-to-cloudfront-distribution.html)

### Question 12

You are building an automated transcription service where Amazon EC2 worker instances process an uploaded audio file and generate a text file. You must store both of these files in the same durable storage until the text file is retrieved. Customers fetch the text files frequently. You do not know about the storage capacity requirements. Which storage option would be both cost-efficient and highly available in this situation?

- A: Multiple Amazon EBS Volume with snapshots
- B: A single Amazon Glacier Vault
- C: A single Amazon S3 bucket
- D: Multiple instance stores

#### _Answer: C_

Correct Answer – C

Amazon S3 is the perfect storage solution for audio and text files. It is a highly available and durable storage device.

Option A is incorrect because storing files in EBS is not cost-efficient.

Option B is incorrect because files need to be retrieved frequently so Glacier is not suitable.

Option D is incorrect because instance store is not highly available compared with S3.

### Question 13

You are deploying an application to track the GPS coordinates of delivery trucks in the United States. Coordinates are transmitted from each delivery truck once every three seconds. You need to design an architecture that will enable real-time processing of these coordinates from multiple consumers. Which service should you use to implement data ingestion?

- A: Amazon Kinesis
- B: AWS Data Pipeline
- C: Amazon AppStream
- D: Amazon Simple Queue Service

#### _Answer: A_

Amazon Kinesis makes it easy to collect, process, and analyze real-time, streaming data so you can get timely insights and react quickly to new information. Amazon Kinesis offers key capabilities to process streaming data cost-effectively at any scale, along with the flexibility to choose the tools that best suit the requirements of your application.

With Amazon Kinesis, you can ingest real-time data such as video, audio, application logs, website clickstreams, and IoT telemetry data for machine learning, analytics, and other applications. Amazon Kinesis enables you to process and analyze data as it arrives and responds instantly instead of waiting until all your data is collected before the processing ca begin. [Amazon Kinesis](https://aws.amazon.com/kinesis/)

### Question 14

Your current architecture consists of a set of web servers spun up as part of an Autoscaling group. These web servers then communicate with a set of database servers. You need to ensure that the database servers' security groups are set properly to accept traffic from the web servers. Which of the following is the best way to accomplish this?

- A: Ensure that the Private IP addresses of the web servers are put as sources for the incoming rules in the database server security group.
- B: Ensure that the Public IP addresses of the web servers are put as sources for the incoming rules in the database server security group.
- C: Ensure that the web server security group is placed as the source for the incoming rules in the database server security group.
- D: Ensure that the Instance ID of the web servers are put as sources for the incoming rules in the database server security group.

#### _Answer: C_

Options A and B are invalid or not the best practice. Since they are part of the Autoscaling Group, the IP addresses of the instances can change.

Option D is incorrect since normally you don’t specify the Instance ID in Security Groups.

### Question 15

While managing permissions for the API Gateway, what could be used to ensure that the right level of permissions is given to Developers, IT Admins, and users? Also, the permissions should be easily managed.

- A: Use the secure token service to manage the permissions for different users.
- B: Use IAM Policies to create different policies for different types of users.
- C: Use the AWS Config tool to manage the permissions for different users.
- D: Use IAM Access Keys to create sets of keys for different types of users.

#### _Answer: B_

AWS Documentation mentions the following:

You control access to Amazon API Gateway with [IAM permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_controlling.html) by controlling access to the following two API Gateway component processes.

To create, deploy, and manage an API in API Gateway, you must grant the API developer permissions to perform the required actions supported by the API management component of API Gateway.

To call a deployed API or to refresh the API caching, you must grant the API caller permissions to perform required IAM actions supported by the API execution component of API Gateway.

### Question 16

A global sports news company has hosted its website on Amazon EC2 instance using a single Public IP address & is front-ended by TLS-enabled Application Load Balancer. For an upcoming mega sports event, they plan to launch a new website on the existing Amazon EC2 instance. The company has registered a different domain name & possesses a separate TLS certificate for this new website.

As an AWS consultant to this company, which of the following recommendations will you provide to support multiple certificates with existing Public IP addresses in the most cost-effective way?

- A: Launch an additional TLS-enabled ALB front ending Amazon EC2 instance with different certificates for each domain.
- B: Use Wildcard certificates on ALB matching old & new domain name.
- C: Use a single certificate on ALB & add Subject Alternative Name (SAN) for additional domain name.
- D: Use multiple TLS certificates on ALB using Server Name Indication (SNI).

#### _Answer: D_

ALB supports Server Name Indication (SNI), enabling hosting multiple domain names with different TLS certificates behind a single ALB. With SNI, multiple certificates can be associated with listeners in ALB, enabling each web application to use separate certificates. The below diagrams shows the process which takes place when a client tries to access a website. Client Browser starts a TLS handshake by sending a ClientHello message which consists of protocol version, extensions, cipher suites, and compression techniques. Based on browser capabilities, ALB responds with a valid certificate for a domain name of the requested web application.

Option A is incorrect as launching additional ALB will work. But it will incur additional cost & admin work for setup.

Option B is incorrect as using wildcard certificates can be used for related sub-domains & not different domains.

Option C is incorrect as using SAN certificates, for any new addition of domain, all certificates need to revalidate with certificate authority.

[ALB Server Namer Indication](https://aws.amazon.com/blogs/aws/new-application-load-balancer-sni/)

### Question 17

You work in a large organization. Your team creates AWS resources such as Amazon EC2 dedicated hosts and reserved capacities that need to be shared by other AWS accounts. You need an AWS service to centrally manage these resources so that you can easily specify which accounts or Organizations can access the resources. Which AWS service would you choose to meet this requirement?

- A: IAM
- B: Resource Access Manager
- C: Service Catalog
- D: AWS Single Sign-On

#### _Answer: B_

AWS Resource Access Manager (AWS RAM) helps users to share resources with other AWS accounts or Organizations. Refer to the reference in https://docs.aws.amazon.com/ram/latest/userguide/what-is.html.

Option A is incorrect: Because IAM cannot be used to manage and share these resources.

Option B is CORRECT: EC2 dedicated hosts and reserved capacities are shareable resources that are supported by Resource Access Manager. Check the reference in [AWS Shareable](https://docs.aws.amazon.com/ram/latest/userguide/shareable.html).

Option C is incorrect: Because Service Catalog is used to manage catalogs and cannot share resources with others.

Option D is incorrect: Because AWS Single Sign-On is used for SSO access and does not share the mentioned resources.

### Question 18

A company is planning to host an active-active site. One site will be deployed in AWS, and the other one on their On-premise data center. They need to ensure that the traffic is distributed to multiple resources, proportionately between both sites. Which of the following routing policy would you use for this purpose?

- A: Simple Routing
- B: Failover Routing
- C: Latency Routing
- D: Weighted Routing

#### _Answer: D_

The AWS Documentation mentions the following.

Weighted routing lets you associate multiple resources with a single domain name (example.com) or subdomain name (acme.example.com) and choose how much traffic is routed to each resource. This can be useful for various purposes, including load balancing and testing new versions of software.

To configure weighted routing, you create records with the same name and type for each of your resources. You assign each record a relative weight that corresponds with how much traffic you want to send to each resource. Amazon Route 53 sends traffic to a resource based on the weight you assign to the record as a proportion of the total weight for all the group records.

Option A is incorrect since this should be usedwhen you want to configure standard DNS records.

Option B is incorrect since this should be used when you want to route traffic to a resource when the resource is healthy or to a different resource when the first resource is unhealthy.

Option C is incorrect since this should be used when you want to improve your users' performance by serving their requests from the AWS Region that provides the lowest latency.

For more information on a Routing policy, please refer to the below URL-[AWS Routing Policy](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html)

### Question 19

You are planning to use Auto Scaling groups to maintain the performance of your web application. How would you ensure that the scaling activity has sufficient time to stabilize without executing another scaling action?

- A: Modify the Instance User Data property with a timeout interval.
- B: Increase the Auto Scaling Cooldown timer value.
- C: Enable the Auto Scaling cross zone balancing feature.
- D: Disable CloudWatch alarms till the application stabilizes.

#### _Answer: B_

The Cooldown period is a configurable setting for your Auto Scaling group, ensuring that it doesn't launch or terminate additional instances before the previous scaling activity takes effect. After the Auto Scaling group dynamically scales using a simple Scaling Policy, it waits for the Cooldown period to complete before resuming scaling activities.

For more information on Auto Scaling Cooldown, please visit the following URL- [Cooldown](https://docs.aws.amazon.com/autoscaling/ec2/userguide/Cooldown.html)

### Question 20

You have 2 development environments hosted in 2 different VPCs in an AWS account in the same region. There is now a requirement to access the resources of one VPC from another. How could this be accomplished?

- A: Establish a Direct Connect connection.
- B: Establish a VPN connection.
- C: Establish VPC Peering.
- D: Establish Subnet Peering.

#### _Answer C_

A VPC peering connection is a networking connection between two VPCs that enable you to route traffic between them privately. Instances in either VPC can communicate with each other as if they are within the same network. You can create a VPC peering connection between your own VPCs, with a VPC in another AWS account, or with a VPC in a different AWS Region.

### Question 21

Your company is planning to store sensitive documents in an S3 bucket. They want to keep the documents private but serve content only to selected users based on a particular time frame. Which of the following can help you accomplish this?

- A: Enable CORS for the S3 bucket
- B: Use KMS and enable encryption for the files
- C: Create pre-signed URL’s
- D: Enable versioning for the S3 bucket

#### _Answer C_

A pre-signed URL gives you access to the object identified in the URL, provided that the creator of the pre-signed URL has permissions to access that object. That is, if you receive a pre-signed URL to upload an object, you can upload the object only if the creator of the pre-signed URL has the necessary permissions to upload that object.

All objects and buckets by default are private. The pre-signed URLs are useful if you want your user/customer to be able to upload a specific object to your bucket, but you don't require them to have AWS security credentials or permissions. When you create a pre-signed URL, you must provide your security credentials and then specify a bucket name, an object key, an HTTP method (PUT for uploading objects), and an expiration date and time. The pre-signed URLs are valid only for the specified duration.

Option A is incorrect since this is used for Cross-origin access.

Option B is incorrect since this is used for encryption purposes.

Option D is incorrect since this is used for versioning.

### Question 22

You have a requirement to get a snapshot of the current configuration of resources in your AWS Account. Which service can be used for this purpose?

- A: AWS CodeDeploy
- B: AWS Trusted Advisor
- C: AWS Config
- D: AWS IAM

#### _Answer C_

With AWS Config, you can do the following.

Evaluate your AWS resource configurations for desired settings.
Get a snapshot of the current configurations of the supported resources that are associated with your AWS account.
Retrieve configurations of one or more resources that exist in your account.
Retrieve historical configurations of one or more resources.
Receive a notification whenever a resource is created, modified or deleted.
View relationships between resources. For example, you might want to find all resources that use a particular security group.

[AWS Config](http://docs.aws.amazon.com/config/latest/developerguide/WhatIsConfig.html)

### Question 23

You work for a company that has a set of EC2 Instances. There is an internal requirement to create another instance in another availability zone. One of the EBS volumes from the current instance needs to be moved from one of the older instances to the new instance. How can you achieve this?

- A: Detach the volume and attach to an EC2 instance in another AZ.
- B: Create a new volume in the other AZ and specify the current volume as the source.
- C: Create a snapshot of the volume and then create a volume from the snapshot in the other AZ
- D: Create a new volume in the AZ and do a disk copy of contents from one volume to another.

#### _Answer: C_

For a volume to be available in another availability zone, you need to create a snapshot from the volume. Then in the snapshot from creating a volume, you can then specify the new availability zone accordingly.

The EBS Volumes attached to the EC2 Instance will always have to remain in the same availability zone as the EC2 Instance. A possible reason for this could be because EBS Volumes are present outside of the host machine, and instances have to be connected over the network. If the EBS Volumes are present outside the Availability Zone, there can be potential latency issues and subsequent performance degradation.

What one can do in such a scenario is to get the Snapshot of the EBS Volume. Snapshot sequentially captures the state of your EBS Volume. You can create an EBS Volume from this snapshot in your desired Availability Zone and attach it to your new Instance.

Later you can detach the volume from the older instance and delete then.

Option A is invalid because the Instance and Volume have to be in the same AZ to be attached to the instance. After all, we have to specify AZ while creating Volume.

Option B is invalid because there is no way to specify a volume as a source.

Option D is invalid because the Diskcopy would be a tedious process.

### Question 24

You work as an architect for a company. An application is going to be deployed on a set of EC2 instances in a VPC. The Instances will be hosting a web application. You need to design the security group to ensure that users have the ability to connect from the Internet via HTTPS. Which of the following needs to be configured for the security group?

- A: Allow Inbound access on port 443 for 0.0.0.0/0
- B: Allow Outbound access on port 443 for 0.0.0.0/0
- C: Allow Inbound access on port 80 for 0.0.0.0/0
- D: Allow Outbound access on port 80 for 0.0.0.0/0

#### _Answer: A_

A security group acts as a virtual firewall for your instance to control inbound and outbound traffic. When you launch an instance in a VPC, you can assign five security groups to the instance. Security groups act at the instance level, not the subnet level. Therefore, each instance in a subnet in your VPC could be assigned to a different set of security groups. If you don't specify a particular group at launch time, the instance is automatically assigned to the default security group for the VPC.

AWS Security groups are stateful. It means that you do not need to open the outbound for responses - open only inbound for requests. If you think your instances will be sending requests to certain IPs (for example: to upgrade/install a package), then you need to open the IP/port for that request. By default, it is open for all traffic.

Option B is incorrect since security groups are stateful. You don’t need to define the rule for outbound traffic.

Options C and D are incorrect since you need to ensure access for HTTPS. Hence you should not configure rules for port 80.

### Question 25

You have been designing a CloudFormation template that creates one elastic load balancer fronting two EC2 instances. Which section of the template should you edit so that the load balancer's DNS is returned upon creating the stack?

- A: Resources
- B: Parameters
- C: Outputs
- D: Mappings

#### _Answer: C_

The below example shows a simple CloudFormation template. It creates an EC2 instance based on the AMI - ami-d6f32ab5. When the instance is created, it will output the AZ in which it is created.

```
{

    "Resources": {

        "MyEC2Instance": {

            "Type": "AWS::EC2::Instance",

            "Properties": {

                "ImageId": "ami-d6f32ab5"

            }

        }

    },

    "Outputs": {

        "Availability": {

            "Description": "The Instance ID",

            "Value":

            { "Fn::GetAtt" : [ "MyEC2Instance", "AvailabilityZone" ]}

        }

    }

}
```

[AWS CloudFormation](https://aws.amazon.com/cloudformation/)
[AWS intrinsic function reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-getatt.html)

Option A is incorrect because this is used to define the main resources in the template.

Option B is incorrect because this is used to define parameters that can be taken during template deployment.

Option D is incorrect because this is used to map key-value pairs in a template.

### Question 26

You work as an architect for a company. There is a requirement for an application to be deployed on a set of EC2 Instances. These would be part of a compute cluster that requires low inter-node latency. Which of the following would you use for this requirement?

- A: Multiple Availability Zones
- B: AWS Direct Connect
- C: EC2 Dedicated Instances
- D: Cluster placement Groups
- E: VPC private subnets

#### _Answer: D_

Amazon Web Services' solution to reduce latency between instances involves the use of placement groups. As the name implies, a placement group is just that -- a group. AWS instances that exist within a common availability zone can be grouped into a placement group. Group members can communicate with one another in a way that provides low latency and high throughput.

Cluster Placement groups are recommended for applications that benefit from low network latency, high network throughput, or both. The majority of the network traffic is between the instances in the group. To provide the lowest latency and the highest packet-per-second network performance for your placement group, choose an instance type that supports enhanced networking.

Because of what is mentioned in the documentation, all other options are incorrect.

### Question 27

You are working as an AWS Architect for a software company. You are working on a new project which involves an application deployed on twenty C5 EC2 On-demand Instances with Elastic IP attached to each instance. During peak hours, when you are initiating new instances, a considerable delay is observed. You perform a pilot test for the option of initiating these Instances and hibernating so that during peak hours, these instances could be quickly launched.

It works fine during the pilot phase. You are recommending this option to be implemented in production. The management team is concerned about the pricing of many EC2 instances in the Hibernate state. What is considered to calculate the pricing for an EC2 instance in the Hibernate state?

- A: Elastic IP address and EBS volumes attached to EC2 Instance
- B: Total Compute capacity per hour, Elastic IP address and EBS volumes attached to EC2 Instance
- C: Total Compute capacity per hour and EBS volumes attached to EC2 Instance
- D: Total Compute capacity per hour & Elastic IP address attached to EC2 Instance

#### _Answer: A_

Compute capacity is not chargeable during hibernate state of EC2 instances. When an EC2 instance is in the Hibernate state, you pay only for the EBS volumes and Elastic IP Addresses attached to it.

Options B, C, and D are incorrect because when an EC2 instance is in a hibernate state, compute capacity charges are not applicable. The charges are only applicable for the EBS volumes and Elastic IP Addresses attached to it.

### Question 28

You are planning to launch the AWS ECS container instance. You would like to set the ECS container agent configuration during the ECS container instance initial launch. What should you perform to configure container agent information?

- A: Set configuration in the ECS metadata parameter during cluster creation.
- B: Set configuration in the user data parameter of EC2 instance.
- C: Define configuration in the task definition.
- D: Define configuration in the service definition.

#### _Answer: B_

When you launch an Amazon ECS container instance, you have the option of passing user data to the instance. The data can be used to perform common automated configuration tasks and even run scripts when the instance boots. For Amazon ECS, the most common use cases for user data are to pass configuration information to the Docker daemon and the Amazon ECS container agent.

[AWS Launch ECS container](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/launch_container_instance.html)

Use `echo` to copy the configuration parameters to the file:

```
#!/bin/bash
echo "ECS_CLUSTER=MyCluster" >> /etc/ecs/ecs.config
```

If there is multiple variables to be written in the ECS configuration file:

```
#!/bin/bash
cat << 'EOF' >> /etc/ecs/ecs.config
ECS_CLUSTER=MyCluster
ECS_ENGINE_AUTH_TYPE=docker
ECS_ENGINE_AUTH_DATA={"https://index.docker.io/v1/":{"username":"my_name","password":"my_password","email":"email@example.com"}}
ECS_LOGLEVEL=debug
EOF
```

### Question 29

Which of the following actions is required by Lambda execution role to write the logs into AWS CloudWatch? (choose 3 options)

- A: logs:CreateLogGroup
- B: logs:GetLogEvents
- C: logs:CreateLogStream
- D: logs:DescribeLogStreams
- E: logs:PutLogEvents

#### _Answer: A & C & E_

The corresponding configuration of `AWSLambdaBasicExecutionRole` is as follow:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:PutLogEvents"
      ],
      "Resource": "*"
    }
  ]
}
```

### Question 30

Your company has setup EC2 Instances in a VPC for their application. The IT Security department has advised that all traffic be monitored to the EC2 Instances. Which of the following features can be used to capture information for outgoing and incoming IP traffic from network interfaces in a VPC.

- A: AWS Cloudwatch
- B: AWS EC2
- C: AWS SQS
- D: AWS VPC Flow Logs

#### _Answer: D_

VPC Flow Logs is a feature that enables you to capture information about the IP traffic going to and from network interfaces in your VPC. Flow log data can be published to Amazon CloudWatch Logs and Amazon S3. After you've created a flow log, you can retrieve and view its data in the chosen destination.

Option A is incorrect since this is a monitoring service

Option B is incorrect since this is a compute service

Option C is incorrect since this is a messaging service

### Question 31

A media firm uses the Amazon S3 bucket to save all videos shared by reporters across the globe. Operation Team has instructed all reporters to use only Multipart Uploads while uploading these large-sized videos to Amazon S3 bucket in each region. Most of the reporters are working from remote areas & face challenges in uploading videos. The Finance Team is concerned about high costs incurred by saving data in the Amazon S3 bucket & seeking your guidance. Post verification, you observe a large number of incomplete uploads in Amazon S3 buckets in each region. The uncompleted uploads can be deleted after a certain period of time.

Which of the following actions can minimize charges for saving video files in the Amazon S3 bucket?

- A: Reporter's need to compress video files locally before uploading to Amazon S3 bucket.
- B: Reporters need to upload Videos to Amazon S3 Glacier to save additional charges.
- C: Create a Lifecycle Policy to move all incomplete Multipart uploads to Amazon S3 Glacier after weeks time from initiation.
- D: Create a Lifecycle Policy to delete all incomplete Multipart uploads after weeks time from initiation.

#### _Answer: D_

Incomplete Multipart Uploads incur storage charges on the Amazon S3 bucket. Lifecycle rules can be used to abort the uploading of multipart uploads that are incomplete since a specific time frame & also deletes these parts to free up storage, reducing costs for this storage.

Option A & B are incorrect as Incomplete Multipart Uploads incur charges. These charges can be stopped by stopping multipart uploads.

Option C is incorrect as Moving all incomplete Multipart uploads to Amazon S3 Glacier would not completely reduce the cost for storing data. As data in Amazon S3 Glacier would incur cost, it would be less than data storing the Amazon S3 bucket. Also, incomplete Multipart uploads would not be used until fully uploaded.

### Question 32

Your team has deployed an application that consists of a web and database tier hosted on separate EC2 Instances. Both EC2 Instances are using General Purpose SSD for their underlying volume type. Of late, there are performance issues related to the read and writes of the database EC2 Instance. Which of the following could be used to alleviate the issue?

- A: Change the Instance type to a higher Instance Type.
- B: Change the EBS volume to Provisioned IOPS SSD.
- C: Enable Enhanced Networking on the Instance.
- D: Enable Multi-AZ for the database.

#### _Answer: B_

The Provisioned IOPS SSD EBS volume type is perfect for these types of workloads. The below excerpt from the documentation shows the key differences between the different volume types.

Option A is incorrect since the primary issue is that the volume type is not correct.

Option C is incorrect since networking is not an issue here.

Option D is incorrect since this option is applicable for the AWS RDS service.

### Question 33

Your company is planning to make use of the Elastic Container service for managing their container-based applications. They are going to process both critical and non-critical workloads with these applications. Which of the following COST effective setup would they consider?

- A: Use ECS orchestration and Spot Instances for processing critical data and On-Demand for the non-critical data.
- B: Use ECS orchestration and On-Demand Instances for processing critical data and Spot Instances for the non-critical data.
- C: Use ECS orchestration and Spot Instances for both the processing of critical data and non-critical data.
- D: Use ECS orchestration and On-Demand Instances for both the processing of critical data and non-critical data.

#### _Answer: B_

Spot Instance and On-demand Instance are very similar in nature. The main difference between these is a commitment. In Spot Instance, there is no commitment. As soon as the Bid price exceeds the Spot price, a user gets the Instance. In an On-demand Instance, a user has to pay the On-demand rate specified by Amazon. Once they have bought the Instance, they have to use it by paying that rate.

In Spot Instance, once the Spot price exceeds the Bid price, Amazon will shut the instance. The benefit to the user is that they will not be charged for the partial hour in which the Instance was taken back from them.

Spot instances are not always cheaper than on-demand, they can and do sometimes fluctuate wildly, even to very high per hour amounts, higher than th on-demand price at times.

A Spot Instance is an unused EC2 instance that is available for less than the On-Demand price. Because Spot Instances enable you to request unused EC2 instances at steep discounts, you can significantly lower your Amazon EC2 costs. The hourly price for a Spot Instance is called a Spot price. The Spot price of each instance type in each Availability Zone is set by Amazon EC2 and adjusted gradually based on the long-term supply of and demand for Spot Instances. Your Spot Instance runs whenever capacity is available, and the maximum price per hour for your request exceeds the Spot price.

Options A and C are incorrect since Spot Instances can be taken back or interrupted and should not be used for critical workloads.

Option D is not a cost-effective solution. You can use Spot Instances for non-critical workloads.e

### Question 34

A company has its major applications deployed in AWS. The company is building a new office and requires a high-performance network connection between the local office network and the AWS network. The connection needs to have high bandwidth throughput and allow users in the office to connect with multiple AWS VPCs of multiple AWS Regions. How would you establish the connection in the most appropriate way?

- A: For each AWS Region, create an AWS Direct Connect by configuring a public VIF between the VPC Virtual Private Gateway and the Customer Router.
- B: Create a Direct Connect Gateway to connect the local network with multiple Amazon VPCs across different regions.
- C: Configure two Direct Connects with two private VIFs to provide highly-available ad dedicated private connections.
- D: Create an AWS Direct Connect dedicated network connection on top of Amazon VPN to establish an end-to-end secure IPSec connection.n

#### _Answer: B_

Option A is incorrect because in this option users need to configure an AWS Direct Connect for each AWS Region, which is not the most appropriate method. Besides, private VIF should be set up in Direct Connection instead of public VIF. Private virtual interface is used to access Amazon VPC using private IP addresses and public virtual interface is used to access AWS public services. In this scenario, the connections need to be secured, so private VIF should be used.

Option B is CORRECT because Direct Connect Gateway, as a globally available resource, can be used to establish high-performance network connections to different AWS Regions and reduce management loads.

Option C is incorrect because this option is suitable for scenarios in which highly available and redundant connections are needed. There is no such requirement in the question.

Option D is incorrect because the question does not require a secure IPSec connection therefore VPN is not needed. This option also does not address the requirements to connect with different AWS Regions.

### Question 35

Your company owns several EC2 Windows servers in production. In order to be compliant with recent company security policies, you need to create an EC2 Windows bastion host for users to connect to the instances via the Remote Desktop Protocol (RDP). How would you ensure that users can perform remote administration for the Windows servers ONLY through the new bastion host?

- A: Configure the security groups of the Windows server instances to only accept TCP/3389 connections from the security group of the Windows bastion host.
- B: Configure the security group of the Windows bastion host to only allow RDP from the company’s IP addresses.
- C: Add a NACL rule in the subnets of the Windows server instances to deny TCP/443 and TCP/22.
- D: In the NACL of the bastion host server, allow the inbound and outbound traffic for TCP/3389.

#### _Answer: A_

Option A is CORRECT because with this option, Windows server instances only allow the RDP traffic from the bastion host instance. Users need to login to the bastion host to connect to the Windows servers.

Option B is incorrect because this option only allows the connections to the bastion host. It does not provide the RDP connections to the Windows servers through the bastion host.

Option C is incorrect because this option only denies ports 443 and 22. It does not allow any rules for the inbound RDP connections.

Option D is incorrect because similar to option B, it only controls the RDP traffic of the bastion host and there are no controls or limitations on the Windows instances. Users can bypass the bastion host to connect to the Windows servers via RDP and there is no NACL rule to deny it.
The NACL of the bastion host server cannot block the unexpected connections. Instead, the control should be applied in the Windows instances to only allow the connections from the Windows bastion host.

### Question 36

Your team uses Amazon ECS to manage containers for several micro-services. To save cost, multiple ECS tasks should run at a single container instance. When a task is launched, the host port should be dynamically chosen from the container instance's ephemeral port range. The ECS service should select a load balancer that supports dynamic mapping. Which types of load balancers are appropriate?

- A: Application Load Balancer or Network Load Balancer.
- B: Application Load Balancer only.
- C: Network Load Balancer only.
- D: Application Load Balancer or Classic Load Balancer.

#### _Answer: A_

Option A is CORRECT because both Application Load Balancer and Network Load Balancer support dynamic mapping. You can configure the ECS service to use the load balancer, and a dynamic port will be selected for each ECS task automatically. With Dynamic mapping, multiple copies of a task can run on the same instance.

Option B and C are incorrect: Please check the below references.

Option D is incorrect because Classic Load Balancer does not support dynamic mapping. With Classic Load Balancer, you have to define the port mappings on a container instance statically.

[AWS Load Balancer Types](https://docs.aws.amazon.com/AmazonECS/latest/userguide/load-balancer-types.html)
[ECS Dynamic Port Mapping](https://aws.amazon.com/premiumsupport/knowledge-center/dynamic-port-mapping-ecs/)

### Question 37

A large amount of structured data is stored in Amazon S3 using the JSON format. You need to use a service to analyze the S3 data directly with standard SQL. In the meantime, the data should be easily visualized through data dashboards. Which of the following services is the most appropriate?

- A: Amazon Athena and Amazon QuickSight.
- B: AWS Glue and Amazon Athena.
- C: AWS Glue and Amazon QuickSight.
- D: Amazon Kinesis Data Stream and Amazon QuickSight.

#### _Answer: A_

Option A is CORRECT because Amazon Athena is the most suitable to run ad-hoc queries to analyze data in S3. Amazon Athena is serverless, and you are charged for the amount of scanned data. Besides, Athena can integrate with Amazon QuickSight that visualizes the data via dashboards.

Option B is incorrect because AWS Glue is an ETL (extract, transform, and load) service that organizes, cleanses, validates, and formats data in a data warehouse. This service is not required in this scenario.

Option C is incorrect because it is the same as Option B. AWS Glue is not required.

Option D is incorrect because, with Amazon Kinesis Data Stream, users cannot perform queries for the S3 data through standard SQL.

[AWS Athena](https://aws.amazon.com/athena/pricing/)
[AWS Create a data set athena](https://docs.aws.amazon.com/quicksight/latest/user/create-a-data-set-athena.html)

### Question 38

You have an Amazon Route 53 alias record that routes the traffic to an Application Load Balancer. Later on, the availability zones enabled for the load balancer are changed by a team member. When you check the load balancer using the dig command, you find that the IPs of the ELB have changed. What kind of change do you need to do for the alias record in Route 53?

- A: Change the record type from A to CNAME.
- B: Modify the destination to the DNS name of the Application Load Balancer.
- C: Add the new IP addresses in the destination of the alias record.
- D: Nothing as Route 53 automatically recognizes changes in the resource for the alias record.

#### _Answer: D_

Option A is incorrect because there is no need to change the type to CNAME as the alias record continues to work, although the IP addresses are changed for the ELB.

Option B is incorrect because Route 53 can find out the new IPs of the ELB. This change is not required.

Option C is incorrect because you cannot add any extra IPs to this record after creating the alias record. Route 53 is responsible for routing the traffic to the correct IP addresses.

Option D is CORRECT because Route 53 automatically routes the traffic to the new ELB IP addresses. With alias records, users do not need to change the record sets even if they have some configuration changes.

### Question 39

You have an S3 bucket that is used to store important data for a web application. You want to receive an email notification whenever an object removal event happens in the S3 bucket. How would you configure the S3 bucket to achieve this requirement?

- A: Configure the object-level logging for the S3 bucket and register an SNS topic to provide notifications.
- B: Configure the server access logging for the object removal events. Add an SNS topic to notify the team via emails.
- C: Set up an AWS Config rule to check the object deletion events. Register a Lambda function to send notifications.
- D: Configure an S3 event notification for the object removal events. Send the events to an SNS topic.

#### _Answer: D_

Option A is incorrect because object-level logging is used to record object-level API activities in CloudTrail. Users cannot register an SNS topic for object-level logging.

Option B is incorrect because server access logging does not trigger an SNS topic for the object removal events.

Option C is incorrect because you would need to write a custom Lambda function in the AWS Config rule to check the object removal events. This method is more complicated than option D.

Option D is CORRECT because with an S3 event notification, you can select which events are enabled for the notification.

[S3 enable event notification](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/enable-event-notifications.html)
[S3 notification](https://docs.aws.amazon.com/AmazonS3/latest/dev/NotificationHowTo.html)

### Question 40 

Your organization had asked to be cost-efficient in designing AWS solutions. You have created three VPCs(VPC A, VPC B, VPC C), peered VPC A to VPC B and VPC B to VPC C. You have created a NAT gateway in VPC B and would like to use the same NAT Gateway for resources within VPC A and VPC C. However, the resources within VPC A and VPC C cannot communicate to the internet through NAT Gateway, but resources in VPC B can communicate. What could be the reason?

- A: Route tables in VPC A and VPC C are not configured to have VPC B’s NAT gateway.
- B: Using another VPC's NAT Gateway is not supported in AWS.
- C: VPC A has not peered with VPC C.
- D: NAT Gateway is not created inside VPC B’s public subnet.

#### _Answer: B_

In a VPC peering connection, using the NAT Gateway of another VPC becomes transitive routing and is not supported in AWS.
You can use a NAT gateway to connect to other VPCs or your on-premises network, but cannot make other VPC connect to the internet.

You cannot route traffic to a NAT gateway through a VPC peering connection, a Site-to-Site VPN connection, or AWS Direct Connect. A NAT gateway cannot be used by resources on the other side of these connections. [NAT gateway basics](https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-nat-gateway.html#nat- gateway-basics)

For Option A, in VPC’s route table, only NAT Gateway of the belonging VPC can be configured. VPC A and VPC C cannot configure VPC B’s NAT Gateway in their respective route tables. This option is incorrect.

For Option B, as explained above, transitive routing is not supported. This option is correct.

For Option C, even if VPC A and C have peered and configured route tables with their entire IP range, using NAT Gateway of another VPC is not possible.

For Option D, the question says VPC B resources can communicate with the internet, for which NAT gateway should be on a public subnet. So this option is not valid.

### Question 41 

As a Cloud Architect, you have deployed an existing application from the local server to an On-demand EC2 instance. You found out that there is an issue while connecting the application using the HTTPS Protocol. After troubleshooting the issue, you added port 443 to the security group of the instance. How much time will it take to update changes to all of the resources related to Security groups?

- A: It can take up to 10 minutes depending on the number of resources.
- B: You just need to restart the EC2 Server.
- C: You cannot make any change to existing security group, you have to create new Security group. 
- D: Immediately without restart.
- E: You have to deploy your application again.

#### _Answer: D_

You can assign a security group to an instance when you launch the instance. When you add or remove rules, those changes are automatically applied to all instances to which you've assigned the security group.

Option A is incorrect. Any changes made to the Security Group are immediately effected.

Option B is incorrect because you don’t need to restart the server to check any Security Group updates.

Option C is incorrect because you can modify rules in the security group.

Option D is CORRECT because any changes made to the security group are taken into effect immediately.

Option E is incorrect because this security group works at the instance level, not at the application level.

### Question 42

One of your colleagues, who is new to the company where you work as a cloud Architect, has some issues with IP Addresses. He has created an Amazon VPC with an IPV4 CIDR block 10.0.0.0/24, but now there is a requirement of hosting a few more resources to that VPC. As per his knowledge, he is thinking of creating a new VPC with a greater range. Could you suggest to him a better way that should be reliable?

- A: Delete the existing subnets in the VPC and create new Subnets in VPC.
- B: He is thinking of the right approach.
- C: You can create new VPC and connect old VPC with a new one.
- D: You can expand existing VPC by adding Secondary CIDR to your current VPC.

#### _Answer: D_

Options A, B, C are incorrect because it is not reliable to go for this type of approach as VPC to VPC connection will take new resources like VPC Peering. Creating a new VPC or Subnet is also not suggested.

Option D is correct because you can associate Secondary CIDR to your current VPC to accommodate more hosts.

[Working with VPCs](https://docs.aws.amazon.com/vpc/latest/userguide/working-with-vpcs.html#add-ipv4-cidr)

### Question 43 

You are a solutions architect working for a financial services firm. Your firm requires a very low latency response time for requests via API Gateway and Lambda integration to your securities master database. The securities master database, housed in Aurora, contains data about all of the securities your firm trades. The data consists of the security ticker, the trading exchange, trading partner firm for the security, etc. As this securities data is relatively static, you can improve the performance of your API Gateway REST endpoint by using API Gateway caching. Your REST API calls for equity security request types and fixed income security request types to be cached separately.
Which of the following options is the most efficient way to separate your cache responses via request type using API Gateway caching?

- A: Payload compression
- B: Custom domain name
- C: API Stage
- D: Query string

#### _Answer: D_

Option A is incorrect. Payload compression is used to compress and decompress the payload to and from your API Gateway. It is not used to separate cache responses.

Option B is incorrect. Custom domain names are used to provide more readable URLs for the users of your AIPs. They are not used to separate cache responses.

Option C is incorrect. An API stage is used to create a name for your API deployments. They are used to deploy your API in an optimal way.

Option D is correct. You can use your query string parameters as part of your cache key. This allows you to separate cache responses for equity requests from fixed income request responses.

### Question 44 

You are a solutions architect working for a data analytics company that delivers analytics data to politicians that need the data to manage their campaigns. Political campaigns use your company’s analytics data to decide on where to spend their campaign money to get the best results for the efforts. Your political campaign users access your analytics data through an Angular SPA via API Gateway REST endpoints. You need to manage the access and use of your analytics platform to ensure that the individual campaign data is separate. Specifically, you need to produce logs of all user requests and responses to those requests, including request payloads, response payloads, and error traces. Which type of AWS logging service should you use to achieve your goas?

- A: Use CloudWatch access logging
- B: Use CloudWatch execution logging
- C: Use CloudTrail logging
- D: Use CloudTrail execution loggingl

#### _Answer: B_

Option A is incorrect. CloudWatch access logging captures which resource accessed an API and the method used to access the API. It is not used for execution traces, such as capturing request and response payloads.

Option B is correct. CloudWatch execution logging allows you to capture user request and response payloads as well as error traces.

Option C is incorrect. CloudTrail captures actions by users, roles, and AWS services. CloudTrail records all AWS account activity. CloudTrail does not capture error traces.

Option D is incorrect. CloudTrail does not have a feature called execution logging.

### Question 45 

You are a solutions architect working for a social media company that provides a place for civil discussion of political and news-related events. Due to the ever-changing regulatory requirements and restrictions placed on social media apps that provide these services, you need to build your app in an environment where you can change your implementation instantly without updating code. You have chosen to build the REST API endpoints used by your social media app user interface code using Lambda. How can you securely configure your Lambda functions without updating code? (Select TWO)

- A: Pass environment variables to your Lambda function via the request header sent to your API Gateway methods.
- B: Configure your Lambda functions to use key configuratio.
- C: Use encryption helpers
- D: Use Lambda layers
- E: Use Lambda aliasesn

#### _Answer: B & C_ 

Option A is incorrect. Sending environment variables to your Lambda function as request parameters would expose the environment variables as plain text. This is not a secure approach.

Option B is correct. Lambda key configuration allows you to have your Lambda functions use an encryption key. You create the key in AWS KMS. The key is used to encrypt the environment variables that you can use to change your function without deploying any code.

Option C is correct. Encryption helpers make your lambda function more secure by allowing you to encrypt your environment variables before they are sent to Lambda.

Option D is incorrect. Lambda layers are used to package common code such as libraries, configuration files, or custom runtime images. Layers will not give you the same flexibility as environment variables for use in managing change without deploying any code.

Option E is incorrect. Lambda aliases are used to refer to a specific version of your Lambda function. You could switch between many versions of your Lambda function, but you would have to deploy new code to create a different version of your Lambda function.

[Data protection in AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/security-dataprotection.html)
[Lambda function aliases](https://docs.aws.amazon.com/lambda/latest/dg/configuration-aliases.html)
