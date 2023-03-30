# Infrastructure as Code (IaC) with AWS

The project uses AWS [CloudFormation](https://aws.amazon.com/cloudformation/) to set up the infrastructure to be used to deploy a simple \"Hello World\" website in an EC2 instance. 

## Components

AWS resources used are:
 - Virtual Private Cloud (VPC)
 - Internet gateway (IGW)
 - Subnet
 - Network Address Translation gateway (NAT)
 - Route table and Route
 - Security group
 - Launch configuration
 - Load balancer, target group, load balancer listener, and load balancer listener rule
 - Auto Scaling Group (ASG)

## How it works

The infrastructure consists of a VPC that contains two public and two private subnets (for redundancy and high availability). A request is received from the internet by the IGW that will then allow the request to be propagated into the VPC. The request is received by a NAT gateway that will provide an private IP that can be used in the private subnets. It will also translate the response's IP to the corresponding request's public IP on it's way back to the public subnet. The request is forwarded to the load balancer which determines how to distribute traffic to multiple targets. The request is received by the EC2 instance if it is allowed through the instance's security group. The server will then send out a response.

The ASG will automatically adjust the number of instances based on the amount of traffic. It uses the launch configuration to know how to set up the new instances.