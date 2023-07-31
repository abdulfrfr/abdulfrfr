---
title: "Amazon Route53"
seoTitle: "Amazon Route53"
datePublished: Mon Jul 31 2023 12:06:45 GMT+0000 (Coordinated Universal Time)
cuid: clkqtri9x000509l8homd88g9
slug: amazon-route53
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690805019397/2d638eb7-eb73-48fe-a4b6-422094f40b41.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1690805155252/eb67ab19-5c67-4658-81bd-163f74cc3fdc.png
tags: aws, developer, devops, route53, system-administration

---

Amazon Route53 is a managed DNS service that serves as both a DNS Registry, where you can purchase domain names, and a DNS Authoritative server, allowing you to manage external domains by creating Host Zones and have records for routing record names to server’s IP Addresses.

First, let's talk about some Terminologies you need to get familiar with; Host Zone – That is your domain name which will be having DNS records also called records. DNS Records – Configurations for pointing record names to IP Addresses or other domain DNS Record Name – This is the hostname you will be creating from your host Zone for example, if your host zone is [myapp.com](http://myapp.com), then a record name will be like [api.myapp.com](http://api.myapp.com) A – is a record type for routing a record name (domain) to IPV4 Addresses AAA – for routing a record name (domain) to IPV6 Address CNAME – for routing a record name (domain) to other domain NS – for point the DNS Server to the hosted zone

Now let's talk about some Routing Policies, which are ways in which you can configure your records to your servers.

Routing Policies in Amazon Route53:

• Simple Routing Policy: In this policy, you route a record directly to an IP address or multiple IP addresses.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690804461929/500b3824-499c-4312-b655-a73edc998645.png align="center")

• Latency Routing Policy: With this policy, you can have multiple records of the same record name, each associated with a specific region. Users are directed to the record name with the region closest to them, minimizing latency and improving performance. We can also run health checks on our server to know whether or not our server is healthy otherwise, our users will get redirected to the nearest record with the nearest region closer to them. Use case: Best used for a global application where you have users all over the world.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690804714327/9ac1d39d-eede-4aa1-b326-3f2fdb28e596.png align="center")

• Weighted Routing Policy: This policy allows you to specify different percentages of traffic to be sent to different IP addresses. You can create multiple records with the same record name, each with its own weight (percentage of traffic). Use case: You should use this when you have an updated version of your application and want people to perceive that there is a change in your application.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690804871507/2b6dcc42-be6e-4fee-85dc-6779782ec003.png align="center")

• Failover Routing Policy: Using this policy, you create two records - Primary and Secondary. Route53 directs traffic to the Primary record unless it becomes unavailable, at which point traffic is automatically redirected to the Secondary record. You should also know that our primary record is going to pass through some Health checks which Route53 also manages for us but we are not going to be talking about that today. This ensures high availability.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690804890898/23092746-6405-41c7-b901-718948434602.png align="center")

• Geolocation Routing Policy: With this policy, you create multiple records for specific regions and a default record with the same record name. Users from specific regions are directed to their designated server IPs, while those not among the specified regions are redirected to the default server. Use case: This type of Routing Policy is best used when you have different content for users in different locations, and you want to serve each location the content that is meant for it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690804913501/9ce0dfa1-8657-4907-9290-0061f41e649c.png align="center")

• Geoproximity Routing Policy: This policy directs users to specific server IPs based on a bias factor. The higher the bias, the larger the area it covers. You create multiple records with different biases and link each record name to a specific region. Users are directed to servers based on their geographical proximity.

• Multi-Value Routing Policy: In this policy, a record is linked to multiple IP addresses, and Route53 automatically handles the server selection for users.

• IP-Based Routing Policy: This straightforward policy directly points a record to a particular user's IP address.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690804937375/0bb25d89-924e-4ecc-95de-e91d5a78f74e.png align="center")

Now, I hope you have understood the different types of routing policies we have. Next, I am going to talk to you about pointing a record name to an AWS service you are running in your account instead of an IP Address. We have what is called a CNAME and Alias, which, when specified, indicates that you are routing your record name to a service you are running on AWS. The Alias feature allows you to route a record name, such as [myapp.com](http://myapp.com), to an AWS service. Using the CNAME, a record name such as [myapp.com](http://myapp.com) cannot be routed to an IP Address using the types of Routing Policies we discussed earlier. They only allow record names such as [api.myapp.com](http://api.myapp.com), for example.

In short, the CNAME and Alias feature allows you to point a record to an AWS service, making it easier to manage resources and update service endpoints without changing DNS configurations.

I hope this has given you a very good insight into what you can leverage AWS's Route53 for.

Your comments and feedback would be appreciated, Thank you.