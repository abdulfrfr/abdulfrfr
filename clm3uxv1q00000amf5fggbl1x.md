---
title: "Networking on AWS."
seoTitle: "amazon vpc"
datePublished: Sun Sep 03 2023 19:40:24 GMT+0000 (Coordinated Universal Time)
cuid: clm3uxv1q00000amf5fggbl1x
slug: networking-on-aws
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1693769963441/e8746d46-83d9-40b0-aa0a-0ab50fd8ef6c.png
tags: aws, networking, vpc

---

VPC is an isolated environment where we can deploy our resources and do networking.

Subnet

A subnet is a partition of your network. Used for dividing our network into different sections using our vpc’s CIDR. We can have a Public and a Private subnet, as the name implies, A public subnet is a partition of our network where we can deploy our public resources which will have access to and from the internet.

Internet Gateway

For our VPC to allow traffic into the internet we need what we call an Internet Gateway to be attached to our VPC.

Route Tables

This is used to route traffic coming out of our subnet to the specified destination, e.g., routing any traffic trying to go out of our VPC to go through our Internet Gateway.

NAT Gateway

A NAT Gateway allows our private subnet to have access to the internet. This is done by using our route table to route traffic going out of our private subnet to go through the NAT Gateway which will be hosted in our public subnet.

Security Groups and NACLs

Security Groups is a virtual firewall at our instance level, it allows only rules both inbound and outbound. We open a port and specify the IP address(es) that’s allowed in or out. It is stateful in the sense that, when a request is received, it will recognize that request and send back a response.

NACLs is also a virtual firewall at our subnet level, it allows both allow and deny rules, and it’s stateless, unlike our security groups. Here when a request is allowed in, it doesn’t send a response unless we explicitly configure that, it only allows a traffic in or denies a traffic.

Now we are going to give a scenario where we will be using all we have explained and I will also provide a diagram to illustrate the explanation for more insights.

  
From the diagram below, we have our VPC with two subnets, a Private and a Public subnet. IN both subnets we deployed an EC2 instance each, and both are secured with a security group, Our public subnets have an NACL firewall securing it. Our VPC also has an Internet Gateway which our public subnet route tables are being routed. And in our Public subnet, a NAT Gateway is deployed where traffic from our Private subnet is being routed using the routing table.

NOTE: The arrow in between our Private and Public subnets indicates that communication between them is private and automatically configured by AWS for us.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693769956814/cb7557db-b644-449b-88cd-51a6d5a8779c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693769917825/aaa6df84-ccfe-425a-aa5a-8c673d36c12a.png align="center")