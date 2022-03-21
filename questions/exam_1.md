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
