# Launch a Spot Instance with Amazon EC2

## Lab Details

This lab walks you through the steps to launch an EC2 Spot Instance using the AWS Management Console. You will also learn about Saving Summary and pricing history.

You will practice using Amazon Machine Image (AMI) to launch Amazon EC2 Spot Instance and use key pairs for SSH authentication to log into your instance.

You will create a web page and publish it.

Duration: 1 hour

AWS Region: US East (N. Virginia) us-east-1 

## What is EC2 Spot instance

- Spot Instances are an unused part of Amazon EC2, using which you can save up to 90% on cost as compared to On-Demand cost, but AWS can interrupt your spot instances if the Current Price is higher than the Maximum Price you specified.

- Spot uses the same EC2 instances (AMI and instance type) what On-Demand and Reserved Instances use. It is the best to fit for use cases where data is reproducible and can sustain the interruption at any point in time.

- You can use Spot Instance as additional compute capacity to your On-Demand or Reserved Instances, where fault-tolerant is acceptable.

- EC2 Spot Instances can be launched the same way you launch EC2 Instance, like using Spot Fleet. Auto Scaling Groups or AWS Management Console.

- If AWS terminates or stops your Amazon EC2 Spot Instance within an hour then you will not be charged.

- However, if you choose to stop or terminate your newly launched Spot Instances by yourself, you will have to pay for the total number of seconds you have used.

## Task Details

Log into AWS Management Console.

Select an Amazon Linux Spot Instance from an Amazon Linux AMI 2.

Setting the price of a spot instance to Higher and lower values compared to a given value.

Launch the Spot Instance, to understand the difference between higher and lower prices.

Explore the Spot request, Saving Summary, and Pricing history options.

Test HTML page is launched or not using public IP.

Validation of the lab

Deleting AWS Resources
