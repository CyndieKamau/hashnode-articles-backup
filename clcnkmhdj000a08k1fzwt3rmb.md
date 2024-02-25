---
title: "How To Create an AWS Site-to-Site VPN Connection Part One: Setting Up."
datePublished: Sun Jan 08 2023 16:09:57 GMT+0000 (Coordinated Universal Time)
cuid: clcnkmhdj000a08k1fzwt3rmb
slug: how-to-create-an-aws-site-to-site-vpn-connection-part-one-setting-up
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1673189288036/821f66e9-a619-4023-a447-9db9cb0aaab0.jpeg
tags: cloud, aws, vpn

---

Heeeeyyyy helllooooowww AWS fahm!!!! It's so good to be back!!!!! Mahn had I missed blogging!!!🥰🥰🥰

As usual it's your AWS guurll here Cyndie!! 💃💃 . Now before I forget, I got picked to be an AWS Community Builder!! Yaay!! My AWS Gospel is starting to pay off!!!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673188886153/4143ac28-bd41-45ed-8c07-dcc304b94a6b.png align="center")

Sooooo today I'll be talking about how you can connect your physical data center to the cloud! Technically called a Site-to-Site Virtual Private Network (VPN) connection.

Now for this tutorial, it will be completely hands-on (no boring theory!), and it will be divided into different stages, so that we can go through each stage slowly and avoid too much technical jargon. It's a bit intermediate, meaning some background knowledge is required (especially when we get to networking!!!) buuutt I'll explain as much as I can, and include extra resources.

So buckle up we going to the cloud!!!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673189742216/07c88df7-5e0b-4c98-8756-b27682c48173.jpeg align="center")

## 1\. What is this Site VPN anyways?

### a) What is a VPN?

So a Virtual Private Network, or what we know as *'VPN; The No. 1 Way of Hiding on the Internet!'* is just that; a service that hides your online identity and encrypts your data traffic. It's how we can access blocked websites!!!

Although China works really hard to detect and block VPNs as well!!! Anyways that's a simple explanation of what a VPN is.

The same service is also applied in the cloud, where clients want a cloud environment that is secure.

### b) What is Cloud?

Again in simple terms, think of the cloud as how we rent apartments and pay rent. That's it! The landlord builds the house, partitions it into apartments, then lets them out. Then we rent the apartments.

Similarly, a cloud provider (landlord) buys infrastructure such as servers, builds a center to house them, ensures everything is set, then voila! Our "apartments" are ready! They then rent out the infrastructure as services.

Now I won't go much into that, but we'll go through the 3 main types of Cloud Computing, to get an overview of where site-to-site is applicable.

1. **Public Cloud**
    
    Let's say an apartment has 4 floors. In the public cloud, tenants occupy and rent the 4 floors. They share the resources such as stairs, laundry rooms etc.
    
2. **Private Cloud**
    
    In our same apartment, on the 3rd floor, a single tenant booked the whole floor exclusively for them. So tenants share out the other floors, but the 3rd floor is dedicated just to our very rich tenant. That's a private cloud.
    
3. **Hybrid Cloud**
    
    In hybrid cloud, we have a tenant who has their own private mansion, but still wants to rent some rooms in our block. So they privately own their own house and are still tenants (must be nice).
    

### c) What is a Site-to-Site VPN Connection?

Now let's take our Hybrid Cloud tenant. He/She has their own mansion, and some rented apartments. But they want to connect both, so they can go to their mansion or apartment when they want to. (This tenant is becoming a nuisance😂😂😂)

So what will the landlord do? Create a gate connecting both. That's a Site-to-Site connection!!!

Now our tenant wants the gate to be fortified so that thieves don't access their mansion and apartments. So they hire a security guard to guard that gate. That's where VPN comes in. So we now have a Site-to-Site VPN connection!!!!

Note that it's not the landlord who will hire the security guard, but the tenant!! Therefore in the cloud, the provider will provide the infrastructure, but it's up to the client to protect their networks. It's what's called the **Shared Responsibility Model.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673190619805/f290bc2f-dc35-4a49-9da5-e98f75fc521d.png align="center")

N/B!!! For the hybrid cloud model, there are 2 ways AWS connects on-premise to the cloud.

1. [AWS Direct Connect:](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-direct-connect.html) This is a dedicated network connecting AWS to an on-premise network, but it bypasses the public internet. So no need for VPN, and it reduces congestion while increasing bandwidth. This is used by companies having high throughput workloads.
    
2. [AWS Site-to-Site VPN:](https://docs.aws.amazon.com/vpn/latest/s2svpn/VPC_VPN.html) This now connects AWS to an on-premise network, but through the public internet. Therefore for security, VPN is then configured. It's normally used for small to medium businesses, and it's what we'll look at today.
    

## 2\. Steps to configure the Site-to-Site VPN Connection.

Now there are some Key concepts that we'll go through quickly, then I'll provide extra info. But first, remember this;

For a Site-to-Site VPN connection to work, we have 3 parties involved;

**The client;** The client having the on-premise equipment.

**AWS;** We have the cloud, where the client has some deployed resources.

**VPN;** We have a 3rd party who'll provide the physical hardware or software application, on the client's side, to ensure a secure connection. Eg includes Cisco, Fortinet, pfsense (we'll use pfsense in our tutorial.)

### Key Terminologies Used

**a. VPN Connection:** It's the secure connection between our Cloud environment (Virtual Private Cloud), and our on-premise (Physical) equipment.

**b. Customer Gateway Device:** It's the appliance found on the client's side. Some of these appliances, like pfsense +, can work as a router, firewall and VPN.

**c. Customer Gateway:** It's an AWS resource that will provide information to AWS, about the client's Customer Gateway Device.

**d. Target Gateway:** For the connection, our VPN will have a 'Starting Point' on the client's side. The endpoint on AWS' side is generically called the Target Gateway.

**e. Virtual Private Gateway:** It's simply the 'gate' to access your cloud resources on the AWS side. Each gateway is attached to a single Virtual Private Cloud, where the cloud resources are located.

Here's the [official AWS documentation on Site-to-Site Connection.](https://docs.aws.amazon.com/vpn/latest/s2svpn/VPC_VPN.html)

### Steps of Creating a Site-to-Site Connection.

* Create a customer gateway
    
* Create a target gateway
    
* Configure routing
    
* Update security group
    
* Create a site-to-site connection
    
* Download the configuration file
    
* Configure the Customer Gateway Device
    

For our demo I'll be using a simulated on-premise environment, meaning that I won't be needing any VPN- Capable physical hardware to set up my connection.

Here's what our final connection will look like; I got this lovely architecture from [Adrian Cantrill's labs.](https://github.com/acantril/learn-cantrill-io-labs/tree/master/aws-simple-site2site-vpn)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673097608515/76e1b1d9-55e6-4710-bb9a-232d544bdad8.png align="center")

As you can see here;

1. On the right, we have our on-premise (physical) center, with our traditional servers. Our servers are private so only people within the network can access them.
    
2. For our servers to access the internet, we have our software appliance, which we called the Customer Gateway Device. In this case, we are using pfsense, which acts as a firewall, VPN, and router. The green little thingies you are seeing there are called Network Interface Cards.
    
3. On the left, we then have our AWS VPC, which has our virtual server (the cat smiling at you) running our website on cats.
    
4. The 2 tunnels you're seeing there is now the Site-to-Site connection between our physical center, and our cloud, which we'll accomplish step by step below.
    

---

## STEP 1: Preparations and Setup

The first thing before we get our hands dirty is to ensure the following;

You have an active AWS account that has admin rights. N/B it is much better having an IAM account having admin rights, than running as root. [Create an account below.](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)

In the now active AWS account, we'll be using the **US East region (N. Virginia).**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673429141688/9911a73b-abe9-421f-b461-36d70da7a605.png align="center")

We'll also deploy the pfsense application found in [AWS Marketplace.](https://aws.amazon.com/marketplace/search/results/ref=brs_navgno_search_box?searchTerms=vpn) It comes with a 30-Day trial so no extra costs!

1. You'll just click on the 'Continue to Subscribe' button [here.](https://aws.amazon.com/marketplace/pp/prodview-gzywopzvznrr4)
    
    We'll then need to generate a new SSH (Secure Shell) Key Pair in our console. Key pairs are used to securely login via SSH to one's instances (EC2). Lemme quickly outline the steps here.
    

* First search for 'EC2' in the console's search bar, hit enter. You can also star it as we'll use it frequently.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673100752716/72a78dc1-d117-45a7-8888-f8bd1eb5a55b.png align="center")

* In EC2 Dashboard on the left side there's a menu. Scroll down till you get to **Network and Security**, then click on **Key Pairs.** Once inside, click on **Create key pair** button. I had made other key pairs so don't worry if your dashboard is blank!
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673101171929/fd5c4306-017d-415c-b3e2-5969314dfc98.png align="center")

* Once inside you'll first choose the appropriate key pair name you want. I called mine 'site-site-infra'. Then leave the default as it is for the key pair type.
    
    As for the file format, linux and unix users use the **.pem** format, because SSH is installed in the system. For those using Windows [PuTTY](https://www.putty.org/), they'll use the **.ppk** format.
    
* Once that's set click on the Create key pair button below.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673102440823/cbc2416c-b021-490b-bdf1-85d67d7b2da1.png align="center")
    
    * Voila! Our key pair will be generated, and the file will automatically download itself.
        
        Once that's done, we'll then use [AWS Cloud Formation](https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/) service to be able to manage all the services we'll need. To understand fully what Cloud Formation is, I've embedded one of my favorite explanations, from [BeABetterDev.](https://www.youtube.com/@BeABetterDev)
        
    
    %[https://www.youtube.com/watch?v=0Sh9OySCyb4&t=589s] 
    
    Okay so we won't be creating a Cloud Formation stack from scratch (We'll do this in another tutorial), but we'll be using one made by [Adrian Cantrill](https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/quickcreate?templateURL=https://learn-cantrill-labs.s3.amazonaws.) (If you've got no idea what I'm talking about, watch the video dummy!!🙄🙄🙄🙄 ). Here's a snippet of the [YAML file](https://learn-cantrill-labs.s3.amazonaws.com/aws-simple-site2site-vpn/infra.yaml) he created for our stack;
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673105516116/48283fa5-a354-4982-8f0a-7b6eaf8913e2.png align="center")
    
    Remember the pfsense subscription and the SSH key pair? This is why we had to configure them first so that once we deploy the stack, everything runs smoothly.
    
    Okay! So to access the stack click [here.](https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/quickcreate?templateURL=https://learn-cantrill-labs.s3.amazonaws.com/aws-simple-site2site-vpn/infra.yaml&stackName=S2SVPN) You should see this;
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673106166652/75605eca-697a-45ec-a6c8-6aa0c1abaa83.png align="center")

Everything is configured, so all you'll need to do is scroll down and acknowledge that the stack might create IAM resources, then click on the **Create stack** button.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673106406443/46e116da-7e52-42f6-b38f-789c52faa3c1.png align="center")

Once that's done you'll be redirected back to the Cloud Formation dashboard, where you'll see the progress of our stack, called **S2SVPN.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673106633903/05d1debd-6461-4bd0-876b-e1f30b88ec02.png align="center")

Note that it will take some time to finish creating, but once it's done your console should output this;

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673106856115/1d5cc4b8-6176-416e-8b3a-fdde073a1b80.png align="center")

Yaaay!!! Setup is complete!!!! We can now start the process of setting up a site-to-site connection, which I'll break it down to several stages. But for now, Stage 1 complete!! Here's how our current architecture now looks like.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673107379749/0a2c7e18-12ea-4280-9b72-9c973288e34c.png align="center")

Okaaaay so the next step will be configuring the AWS VPN. See yah in a bit!!!! 😚😚😚

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673188706966/b430ffd1-0760-4b7c-a3e5-f34a79424835.png align="center")