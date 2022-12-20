# CloudFormation-Challenges
This repository contains sample cloudformation  infrastructure as code scripts

## Challenge 2
### Challenge Overview
You have been tasked with creating the required Infrastructure-as-code scripts for a new cloud environment in AWS. The Lead Solutions Architect for the project sends you the following diagram.

![image](https://user-images.githubusercontent.com/22508583/208399697-f42fd91d-b968-433b-818a-42ac7147251b.png)
### TODO
Write a CloudFormation script that:

1. Creates a VPC
  - It will accept the IP Range -also known as CIDR block- from an input parameter
2. Creates and attaches an Internet Gateway to the VPC
3. Creates Two Subnets within the VPC with Name Tags to call them “Public” and “Private”
  - These will also need input parameters for their ranges, just like the VPC.
4. The Subnet called “Public” needs to have a NAT Gateway deployed in it
  - This will require you to allocate an Elastic IP that you can then use to assign it to the NAT Gateway.
5. The Public Subnet needs to have the MapPublicIpOnLaunch property set to true. Use this reference for help.
6. The Private Subnet needs to have the MapPublicIpOnLaunch property set to false.
7. Both subnets need to be /24 in size.
  - If you need assistance with IP math, you can use a subnet calculator such as this one.
8. You will need 2 Routing Tables, one named Public and the other one Private
9. Assign the Public and Private Subnets to their corresponding Routing table
10. Create a Route in the Public Route Table to send default traffic ( 0.0.0.0/0 ) to the Internet Gateway you created
11. Create a Route in the Private Route Table to send default traffic ( 0.0.0.0/0 ) to the NAT Gateway
12. Finally, once you execute this CloudFormation script, you should be able to delete it and create it again, over and over in a predictable and repeatable manner, this is the true verification of working Infrastructure-as-Code
### Challenge Solution
https://github.com/Ngai-E/CloudFormation-Challenges/tree/main/challenge-1
### How to run script with AWS CLI
```aws cloudformation create-stack --stack-name challengeStack --template-body file://challenge_1.yml  --parameters file://challenge_1.json --capabilities "CAPABILITY_IAM" "CAPABILITY_NAMED_IAM" --region=us-east-1```


## Challenge 3
### Challenge Overview
In this challenge, you have been tasked with deploying a Linux server in a private subnet, using the infrastructure that you created in a previous challenge. In the future, this machine will be a web server that sits behind a load balancer, so it never needs to be public, as long as the Load Balancer can reach it.
Use the VPC and the private subnet to create a webserver created in the Challenge 2.
![image](https://user-images.githubusercontent.com/22508583/208591088-74713475-081c-4eea-a476-23174696d13c.png)
In order to connect your instance to AWS Systems Manager, you will be using Amazon Linux 2 for your AMI, since it’s already installed and configured in there.
### TODO
Use the infrastructure we created earlier to build and deploy the following:

1. <b>EC2 Instance</b>: An Amazon Linux 2 EC2 server in the private subnet. Choose the right AMI ID as applicable to your region and the ```t3.micro``` instance-type.
2. <b>SecurityGroup</b>: A security group for the server, that allows inbound port 80 access, for future use.
3. <b>IAM Role and InstanceProfile</b>: The IAM Role to allow EC2 Session Manager to access our server. An InstanceProfile will allow passing the IAM role to our server.
4. You will provide input parameters to this script, for future expansion and flexibility.
5. Bonus/Optional: Instead of hard-coding the VPC and Subnet ID, use the import-export feature to cross reference the resources created in Challenge 2.
