---
title: "Networking on AWS."
seoTitle: "amazon vpc"
datePublished: Sun Sep 03 2023 19:40:24 GMT+0000 (Coordinated Universal Time)
cuid: clm3uxv1q00000amf5fggbl1x
slug: networking-on-aws
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1693769963441/e8746d46-83d9-40b0-aa0a-0ab50fd8ef6c.png
tags: aws, networking, vpc

---

Amazon Web Services (AWS) provides a robust infrastructure for hosting your applications and services, and at the core of this infrastructure is the Virtual Private Cloud (VPC). A VPC serves as an isolated environment where you can deploy your resources and establish networking configurations. In this article, we'll delve into the fundamental components of AWS VPC, shedding light on subnets, Internet Gateways, Route Tables, NAT Gateways, Security Groups, and Network Access Control Lists (NACLs).

**Subnet: Building Blocks of Your Network**

Subnets are the foundational building blocks of your VPC. Think of them as partitions within your network, designed to segment your VPC resources logically. Subnets are defined using a Classless Inter-Domain Routing (CIDR) notation and serve to divide your network into different sections. Within your VPC, you can create both Public and Private subnets, each with a specific role. As their names suggest, a Public subnet is where you deploy resources with direct internet connectivity, while a Private subnet houses resources isolated from public internet access.

**Internet Gateway: The Gateway to the World Wide Web**

To enable communication between your VPC and the public internet, you need an Internet Gateway. This essential component acts as the conduit for traffic entering and exiting your VPC. By attaching an Internet Gateway to your VPC, you establish the connectivity required for your public resources to interact with the internet.

**Route Tables: Navigating Traffic**

Route Tables are instrumental in directing traffic within your VPC. These tables define the path that traffic should follow as it exits a subnet. For instance, a Route Table can be configured to route outbound traffic from your VPC through the attached Internet Gateway, ensuring that resources within your Public subnet can communicate with the internet.

**NAT Gateway: Bridging the Gap for Private Subnets**

When your VPC includes Private subnets that require internet access but need to remain private, you employ a Network Address Translation (NAT) Gateway. This specialized component allows resources in your Private subnet to access the internet indirectly. Traffic is routed from the Private subnet to the NAT Gateway, which resides in the Public subnet, and then forwarded to the internet. This architecture maintains the security and isolation of your Private resources while granting them necessary internet access.

**Security Groups and NACLs: Guarding Your Resources**

Security Groups and Network Access Control Lists (NACLs) serve as crucial security mechanisms within your VPC.

* **Security Groups** function as virtual firewalls at the instance level, regulating both inbound and outbound traffic. They enable you to specify which IP addresses are allowed to communicate with your resources. Security Groups operate in a stateful manner, meaning they can recognize incoming requests and permit corresponding responses.
    
* **NACLs**, on the other hand, operate at the subnet level and manage both allow and deny rules for network traffic. Unlike Security Groups, NACLs are stateless, which means they don't inherently recognize response traffic. They primarily serve as access control tools, either permitting or denying traffic based on configured rules.
    

**Putting It All Together: A Scenario**

Now, let's illustrate these concepts with a practical scenario. In the diagram below, you'll see a VPC with two subnets: one Private and one Public. Within each subnet, an EC2 instance is deployed, with both instances protected by Security Groups. The Public subnet also has an NACL firewall to enhance security.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693769956814/cb7557db-b644-449b-88cd-51a6d5a8779c.png align="center")

Additionally, an Internet Gateway is attached to the VPC, facilitating internet access for resources in the Public subnet. To enable internet connectivity for resources in the Private subnet while maintaining isolation, a NAT Gateway is deployed within the Public subnet, and the route tables are configured to direct traffic accordingly.

**Note:** The arrow connecting the Private and Public subnets signifies that AWS automatically configures private communication between these subnets, ensuring secure and seamless interaction.

In conclusion, understanding the core components of AWS VPC is essential for designing secure and scalable cloud architectures. Subnets, Internet Gateways, Route Tables, NAT Gateways, Security Groups, and NACLs provide the necessary tools to craft robust networking solutions within the AWS cloud environment. By leveraging these components effectively, you can build and manage a VPC tailored to your specific requirements.