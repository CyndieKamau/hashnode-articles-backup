---
title: "AWS Core Services Part 1: Compute"
datePublished: Sat Apr 23 2022 07:29:04 GMT+0000 (Coordinated Universal Time)
cuid: cl2bjj4yl0662w4nvgfr59u2q
slug: aws-core-services-part-1-compute
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1650680082954/rRwbgkx7O.jpg
tags: cloud, aws, business

---

Soooo my dear sisters and brothers in AWS!! Welcome to another goodie  episode!! 🤗🤗🤗🤗
<br>As I'm writing this, its raining heavily outside!! The urge to just curl up and take a nap is so overwhelming!! Then all of us in the mighty third world system know that once the rainy season starts then be prepared for frequent blackouts! So just incase you see a half finished post, then well.....🤭🤭🤭</br>


![images.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650632958981/0m9a2kv1zn.png)

<br>Anyways, since the agenda must agend come rain come blackout, then let's get to business!!</br>
<br>So I recall the first time I fell in love with AWS (kinda sucks that this is the only evidence of my shitty love life💔) I searched for AWS, signed up on the console ( I didn't have a credit card back then. Lemme tell you! Its easier to pass through the eye of the needle than convincing an African parent to lend you their card. No I'm not buying online, mum. Noo no one's gonna steal from you! And the most difficult question to answer.</br>
<br> '' Well, if you are not buying anything, well why do they need my card?'' </br>


![depositphotos_112367768-stock-illustration-angry-cartoon-mom_1_1_70.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1650673339041/SozfL9sJK.jpg)

<br>Oh well. So I 'borrowed' the card. It was all for a higher cause!!) and voila! I felt like an associate already!!</br>

<br>But then..All I saw was the language of the gods. Compute? Elastic BeanStalk? Lambda? Where to start? I just wanted to learn about AWS🥺🥺🥺. So I fully understand how overwhelming it may feel at first! Not to worry though, I got you!.</br>
<br>Now AWS offers over 200 services, but the core services are divided into five main categories:</br>
- Compute
- Storage
- Database
- Networking
- Security

<br>We'll also go through the AWS Cost Management. Actually, most of these services integrate with each other, so we'll touch on other services as well! But for now we'll go through the compute section.</br>

![Screenshot_20220420-023458~2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650638552767/YyTfym8LX.png)
<br>**AWS COMPUTE**</br>
<br>First of all, *what is compute?*</br>
<br>Imagine if you could access iPhone 13 Pro Max on a Tekno phone through the internet, for let's say 30 dollars per month.</br>
<br>So you still have your Tekno phone, but you've got 1 TB storage, selfies look like a photoshoot, and yes! Your tweets have 'Twitter for iPhone' 🤭🤭🤭.</br>
<br>So you don't have to buy the actual phone for 1000 dollars. That's pretty much what AWS Compute entails. Accessing powerful computer machinery online at an affordable cost.</br>

<br>**AWS EC2 **</br>
<br>So referencing back to my Tekno analogy, it perfectly describes EC2!! It's simply accessing a much faster, powerful machine virtually, at a much cheaper cost! Technically the virtual machines are known as instances.</br>

<br>*Practical Use Case *</br>



![pngwing.com.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650636850136/0P5JLuiVz.png)

<br>Cyndie wants to open up an E-Commerce site, but with full control over everything. In this case, EC2 will be the best option for her. She can build, deploy and manage her site on the virtual machines, and depending on traffic, can scale the capacity up or down.</br>
<br>But remember, with great power comes great responsibility. With EC2, you are in charge of everything. From setting up to maintenance, managing EC2 instances can be quite complicated. Not forgetting how it can rack up a huuuge bill if you're not careful!</br>

![IMG-20220422-WA0000.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1650639564382/duww3bJXm.jpg)
<br>*How EC2 can mess you up*</br>
- Launching too many instances
- Leaving EC2 instances running when not in use
- Exposing your private access keys (this is no joke!! Malicious people can access your account and have a field day)

<br>**AWS LightSail**</br>
<br>So Cyndie started building her site using EC2, but then realized that she needed to set up so many things like static IP, SSD Storage manually. So complicated! But Lightsail saves the day!</br>
<br> Lightsail is a simplified version of EC2. It sets up most of the EC2 settings for you, you just choose what you want to use. Example; if Cyndie wants to set up her E-commerce site on wordpress, she will first choose the servers she wants (eg Linux, or Windows), and the wordpress platform.</br>

![Screenshot_20220421-143515~2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650635774416/eQUe55qQ-.png)

<br>**N.B.** While Lightsail is easier to use than EC2, it is quite restricted. For full computing power, EC2 is the best option.</br>

<br>**AWS Lambda**</br>
<br>So Cyndie changed her mind about lightsail, and decided to continue with EC2. She built and deployed her site on the servers. So far so good! But then traffic is still low. She gets 2 to 3 visitors everyday. So majority of the day the site has no traffic. And the EC2 Servers are running the whole day, and the billing is per hour. Meaning she's paying for 21 hours of idle server runtime. Not profitable right?</br>
<br>This is where Lambda comes in. With Lambda, you go serverless! Your application doesn't need to be on any server.</br>
<br>*How does it work?*</br>
<br>So we still have our E-Commerce site. Normally, it would be hosted on a server for it to work (think of a server as a home for your application) but servers can be quite expensive to keep up with. Now with lambda, your application is serverless! You just write code (technically known as a function) that triggers an event. So the functions act as a set of instructions for the site. Example;</br>
- When a user clicks on an item, enlarge it.
- When a user orders for an item, proceed to checkout.
<br>Just note that with Lambda, the developers have to write some high quality code, and anticipate a user's needs in advance, to ensure every scenario has its own function. Otherwise, the site might end up having a bunch of errors!</br>

![images (1).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650647454049/WroOU7tb-.png)

<br>**AWS Batch**</br>
<br>I majored in Genomic Science in campus, and Batch is extremely useful in the world of science!! Lemme briefly take you through the world of genetics🤭. Did you know that 99.9% of everyone's DNA is similar? It's only 0.1% of our DNA that makes us unique from each other. How do we know this? Through genome sequencing.</br>

![112773851-set-of-genome-sequensing-elements-small-sientists-microscope-molecule-helix-of-dna-.webp](https://cdn.hashnode.com/res/hashnode/image/upload/v1650647679868/FKcl93xi9.webp)

<br>Genome sequencing is simply making a Google map of an organism's entire DNA in the lab.</br>
So how does AWS fit in? This, plus other lab procedures have a set of procedures done using computers, generically known as batch processing. So AWS Batch helps with the heavy computerized processes, making work easier!

<br>**AWS Elastic BeanStalk**</br>
<br>When it comes to deploying an app on cloud, Elastic BeanStalk is every developer's best friend! Previously we used to consider the client and how AWS Compute services fulfill their needs. Now let's consider the developer creating the application for the client.</br>
<br>So previously, Cyndie chose EC2 as the platform for her app. Now for a developer, deploying the app on EC2 takes alot of work! So many steps to configure manually! But with Elastic BeanStalk, the developer only uploads the code for the application. AWS sets everything up.</br> 

<br>**AWS Serverless Application Repository**</br>
<br>Serverless Application Repository is like a collection of serverless applications (which we discussed in AWS Lambda). With SAR, developers don't need to build serverless apps over and over again, they just reuse pre-built applications and tailor them to their needs. Think of it as a stack overflow for serverless apps!</br>

<br>**AWS OutPosts**</br>
<br>AWS OutPosts is for large enterprises dealing with aloot of sensitive data, which is too risky to fully migrate to the cloud. Think of hospitals, large scale industries, media and entertainment, banks.</br>
<br>Normally, the essence of cloud is for enterprises to avoid maintaining physical servers and hardwares. But some enterprises require the physical hardware to ensure that there's low latency (delay time) in rendering services, and ensure maximum security measures.</br> 
<br>Therefore, the enterprise provides physical space, power and network. AWS then provides the machinery (eg servers) sets up everything and maintains it. So an enterprise has its own physical center managed by AWS, while still using the cloud services. Technically this is known as hybrid cloud services.</br>

![[Downloader.la]-62636611b05d5.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1650681405462/vrqnfP_fC.jpg)

<br>**AWS EC2 Image Builder**</br>
<br>When it comes to EC2, we have the EC2 servers themselves, then something else known as an [Amazon Machine Image (AMI)](https://www.techtarget.com/searchaws/definition/Amazon-Machine-Image-AMI). AMIs provide more information about the instance you are about to launch. Example, if I want to launch Linux servers, I will use Linux AMI to launch it.</br>

![Screenshot_20220423-033913~2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650674497230/atloaOrnu.png)

<br>Now one of the challenges encountered when using EC2, is that errors occur frequently during launching. That's because of inadequate testing, as EC2 lacks a testing environment where you can ensure everything is okay before launching the instance. But EC2 Image Builder caters for this gap.</br>
<br>With EC2 Image Builder, you manage all your images efficiently! Not only that, you can test your images against AWS standards or your own, to ensure they are fully compliant! These ensures that during production, you launch virtual machines with fewer errors and security vulnerabilities.</br>

<br>**AWS App Runner**</br>
<br>AWS App Runner is a service that helps developers to quickly deploy 'containerized' web applications and scale.</br>
<br>So *what is containerization?*</br>
<br>Imagine you've got a big presentation in a few days. You've prepared your slides, data, practised infront of a mock audience, everything! Then on the big day, your slides refuse to open on the host's laptop. Or they have a completely alien formatting. Pretty stressful right? That's a challenge developers had to face before containers.</br>
<br>So a developer would test their application on their own laptop first, to ensure everything is okay, before transferring it to the team's test environment. But now the issue would arise when the developer's environment and the test environment are different.</br>
 <br>With containers, think of an all-in-one package, where your application and all its dependencies are stored in one environment. So lets say you built an app using Python 2.7 and containerized it. It doesn't matter whether the test or production environment is using Python 3. Because you came with your own library, it will still run.</br>

<br>So let's do a quick recap of the AWS Compute services.</br>
- AWS EC2:- Launch virtual machines the hard way
- AWS LightSail:- Launch virtual machines the easy way
- AWS Lambda:- Avoid the servers altogether
- AWS Batch:- Perform batch processes efficiently
- AWS Elastic BeanStalk:- Uplode code, AWS will set up the rest
- Serverless Application Repository:- Collection of serverless apps
- AWS OutPosts:- Provide space, power and network, AWS will bring and maintain physical servers
- EC2 Image Builder:- Highly secure and compliant EC2 instances
- AWS App Runner:- Build containerized web apps quickly.

<br>For more information on EC2,AMI and Lambda [click here](https://medium.com/programmingnotes/aws-compute-ec2-ami-ecs-aws-lambda-12240db1b003)</br>

<br>🎉🎉That's all for today! I hope you learnt something!🤗🤗🤗 On the next episode we'll delve into AWS Storage. See you soon! I'm so sleepy!💤💤</br>

![casual-life-3d-girl-sleeping-on-the-table.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650680614723/bPjUT7Vrz.png)








