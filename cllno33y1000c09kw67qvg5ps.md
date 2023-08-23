---
title: "Amazon Elastic Beanstalk"
seoTitle: "amazon elastic beanstalk"
seoDescription: "build your application on amazon elastic beanstalk"
datePublished: Wed Aug 23 2023 11:44:12 GMT+0000 (Coordinated Universal Time)
cuid: cllno33y1000c09kw67qvg5ps
slug: amazon-elastic-beanstalk
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692790807841/36709cff-8e6d-4c5e-9d30-b686cfd756c5.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1692790853304/d88f30b4-97cd-4a84-934e-61e75d38d299.png
tags: cloud, aws, developer, cloud-computing, devops

---

Amazon Elastic Beanstalk is a SaaS offered by AWS, which helps deploy applications in a managed environment. This allows developers to focus solely on application development without the hassle of setting up server infrastructure.

Amazon Elastic Beanstalk boasts important features that we will examine shortly.

Let's delve into the Deployment Modes of Amazon Elastic Beanstalk, which dictate how your application is deployed and how new versions are handled.

**All-in-One**: In this mode, the application is deployed, and when a new version is released, the old environment is completely shut down. Amazon Elastic Beanstalk then deploys a new environment with the newer version of the uploaded application. While this is the fastest mode, there may be some downtime. For example, if you initially deployed your application on 4 EC2 instances managed by Amazon Elastic Beanstalk, when uploading a new version, the 4 instances of the old version will be shut down, and 4 new instances with the new version will be started.

**Rolling**: In this mode, the application is deployed, and when a new version is available, a specified number of instances running the application are temporarily taken down and updated with the new version. This process continues until all instances with the old version are updated. To illustrate, let's assume you're running a total of 4 instances and you choose to update 2 at a time. When a new version is uploaded, Elastic Beanstalk will shut down 2 old instances, start 2 new instances with the new version, and then repeat the process until all instances are updated. This approach minimizes downtime but takes time to complete.

**Rolling with Additional Batch**: Similar to Rolling Updates, this mode creates new instances with the new version before shutting down the old instances. For instance, if you have 4 instances and specify that 2 new instances should be created at a time, Elastic Beanstalk will first launch 2 new instances with the new version, then gradually replace the old instances with new ones in batches of 2. This maintains zero downtime but is time-consuming.

**Immutable**: In this mode, Elastic Beanstalk creates new instances running the new version in a temporary Auto-Scaling group and swaps them with the old version instances in the running environment when ready.

Now let's explore two deployment strategies for testing new versions on Amazon Elastic Beanstalk.

**Blue-Green**: This strategy involves creating a separate test environment, cloning the production environment, and making updates. Traffic redirection, using Route53 records, for instance, allows for controlled testing. Once testing is confirmed, the test environment replaces the production environment, becoming the new production environment.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692790661826/e848e5c0-c3f3-4f7b-98c8-78bf0c38b40d.png align="center")

**Traffic Splitting**: This strategy entails creating distinct production and testing environments, both fronted by a load balancer. A minimal amount of traffic is directed to the testing environment. After development, the production environment is removed from the load balancer, leaving the test environment as the new production setup.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692790675512/62fe3f2b-32dd-45b3-8343-14569fcc0a54.png align="center")

These strategies aim to minimize application downtime and ensure high availability when introducing new versions of your application.