# CSAA Practice Test 1

### Question 10

You are working for a start-up company that develops mobile gaming applications using AWS resources. For creating AWS resources, the project team is using CloudFormation Templates. The Project Team is concerned about the changes made in EC2 instance properties by the Operations Team, apart from parameters specified in CloudFormation Templates. To observe changes in AWS EC2 instance, you advise using CloudFormation Drift Detection. After Drift detection, when you check drift status for all AWS EC2 instances, drift for certain property values with default values for resource properties is not displayed. What would you do to include these resource properties to be captured in CloudFormation Drift Detection?

- [A]: Run CloudFormation Drift Detection on individual stack resources instead of entire CloudFormation stack.
- [B]: Explicitly set the property value, which can be the same as the default value.
- [C]: Manually check these resources as this is not supported in CloudFormation Drift Detection.
- [D]: Assign Read permission to CloudFormation Drift Detection to determine drift.

### *Answer: B*

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

### *Answer: C*

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

### *Answer: B & C*

1) To ensure that traffic can flow into your webserver from anywhere on secure traffic, you need to allow inbound security at 443.

2) And then, you need to ensure that traffic can flow from the webserver to the database server via the database security group.

### Question 13

You lead a team to develop a new web application in AWS EC2. The application will have a large number of users globally. For a great user experience, this application requires very low network latency and jitter. If the network speed is not fast enough, you will lose customers. Which tool would you choose to improve the application performance? (Select TWO.)

- [A]: AWS VPN
- [B]: AWS Global Accelerator
- [C]: Direct connect
- [D]: API Gateway
- [E]: CloudFront

### *Answer: B & E*

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

### *Answer: D*

You can use roles to delegate access to users, applications, or services that don't normally have access to your AWS resources. It is not a good practice to use IAM credentials for a production-based application. However, it is a good practice to use IAM Roles. [AWS IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)

### Question 15

A website runs on EC2 Instances behind an Application Load Balancer. The instances run in an Auto Scaling Group across multiple Availability Zones and deliver several static files stored on a shared Amazon EFS file system. The company needs to avoid serving the files from EC2 Instances every time a user requests these digital assets.

What should the company do to improve the user experience of the website?

- [A]: Move the digital assets to Amazon Glacier.
- [B]: Cache static content using CloudFront.
- [C]: Resize the images so that they are smaller.
- [D]: Use reserved EC2 Instances.

### *Answer: B*

Amazon CloudFront is a web service that speeds up distribution of your static and dynamic web content, such as .html, .css, .js, and image files to your users. CloudFront delivers your content through a worldwide network of data centers called edge locations. When a user requests content that you're serving with CloudFront, the user is routed to the edge location that provides the lowest latency (time delay), so that the content is delivered with the best possible performance. If the content is already in the edge location with the lowest latency, CloudFront delivers it immediately. [AWS CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)

In addition, the glacier is not used for frequent retrievals. So Option A is not a good solution. Options C & D will also not help in this situation.

### Question 16

A Solutions Architect is designing a highly scalable system to track records. These records must remain available for immediate download for up to three months and then must be deleted. What is the most appropriate decision for this use case?

- [A]: Store the files in Amazon EBS and create a Lifecycle Policy to remove files after 3 months.
- [B]: Store the files in Amazon S3 and create a Lifecycle Policy to remove files after 3 months.
- [C]: Store the files in Amazon Glacier and create a Lifecycle Policy to remove files after 3 months.
- [D]: Store the files in Amazon EFS and create a Lifecycle Policy to remove files after 3 months.

### *Answer: B*

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

- [A]: 
- [B]: 
- [C]: 
- [D]: 

### *Answer: *


