---
title: "AWS Storage Types; S3, EBS & EFS And How To Differentiate Them!"
datePublished: Sat Jul 16 2022 16:43:08 GMT+0000 (Coordinated Universal Time)
cuid: cl5o4b8qh01j5hanv5xgfba3z
slug: aws-storage-types-s3-ebs-and-efs-and-how-to-differentiate-them
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1657692550764/v9d1FzntT.jpg
tags: aws, aws-s3, aws-ebs, aws-efs

---

Heeeeeyyyy guys!!!! 🤗🤗🤗🤗 It's been a loong loong time!
So I went on I think a two months' hiatus and didn't post much, but I'm back now!

![happydog.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657985450620/M8GloNyuv.png align="center")

Damn I really had missed writing! I just didn't have the energy for it for a while. But I'm back to the game now! 🥳🥳🥳
<br>
Now as I was planning out my future posts, I realized I didn't quite finish talking about AWS services. So without further ado, let's talk about **AWS Storage**.
</br>
<br>
Now AWS has 3 main categories of storage: 
- Object Storage (S3)
- Block Storage (EBS)
- File Storage (EFS)
</br>

<br>
We are going to discuss each type of storage with regards to;
- Architecture
- Use Cases
- Availability and durability
- Costs
</br>



 ### a. Object Storage (Amazon Simple Storage Service)

Now *What is S3?*  So in order to fully differentiate these storage types, I'm going to use an analogy to explain them. *duuh I live for analogies!* Imagine I'm a writer, writing my book on zombie apocalypse!!


![zombie.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657986195277/WafZHZx8_.png align="center")

<br>
Now previously, I used to store my manuscripts locally on my laptop, until I got robbed on my way home and lost everything! This led me to store my work on AWS! (After starting from scratch.... again! If you have never lost your work you've never experienced true heartbreak!!)
</br>

![angryGirl.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657986637319/H2ZYK9jNB.png align="center")
<br>
So we have our file, 'zombieworks.txt' . I decide to use S3 as my storage option. With object storage, S3 will simply place my file as it is; 'zombieworks.txt' . It will be placed as an object in the bucket. It's just like collecting balls and storing them in a bucket. I will now be accessing my manuscript over the internet, through a link.
</br>

<br>
Now imagine I want to add a new chapter to my manuscript. With S3, I now have to retrieve the whole file, work on it, then re-upload it. Just like taking a ball from the bucket, using it, then returning it back to the bucket. Meaning if I get a new idea in the middle of the night, instead of just working on a specific area, I now have to download the whole document. Not quite optimal if I'm gonna be working on it frequently, yes? That's where block storage steps in.
</br>


### b. Block Storage (Amazon Elastic Block Storage)

<br>
With block storage, EBS now takes our manuscript, 'zombieworks.txt', and divides it up to smaller portions called blocks. let's say chapter 1, 2,3 etc. These blocks are then assigned a unique number for identification, then I'm given a key, which is like a roadmap to know which block has what. 


So if today I'm working on say chapter 1, I'll just take out the chapter 1 block, make changes, and they automatically update to the block! So no need to re-upload. Cool right? That's what block storage means.
</br>

<br>
So as I continue working on my story, let's say I'm adding some collaborators to help me on the story plot, my friends are reviewing the story and making some changes, I've already started having a fan base, my manuscript will now have to be accessed by many people at the same time, yes? That's where file storage butts in.
</br>


### c. File Storage (Amazon Elastic File Storage)

With EFS, data is now stored as files. What's better, it's a shared file system. Meaning our manuscript can now be shared across several people in different locations at the same time! Without now having to manually share it to them individually.

<br>
So with that analogy in mind, let's get back to the 3 main storage options; S3, EBS and EFS. 
</br>

### *1. Architecture*

#### - Amazon S3


![s3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657989081267/Z0Vq-Luy_.png align="center")
*Image from [cloudonaut.](https://cloudonaut.io/introducing-the-object-store-s3/)*

<br>
As described above, S3 is a simple object storage service. It's made up of different types of buckets described in detail [here.](https://aws.amazon.com/s3/storage-classes/?nc=sn&loc=3&refid=f890feca-7de4-48c4-80e4-b97e374b0d41)
</br>

<br>
With S3, they are available in regions, example say Northern Virginia region, Tokyo region etc. But they are globally accessed anywhere! This is because they are accessed over the internet. Meaning I can decide to store my data in a bucket in China, but so long as I have a link to the data, I can access it anywhere.
</br>


#### - Amazon EBS


![aws_ebs.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657989398441/XFpOSx9Va.png align="center")
*Image from [OodlesTechnologies.](https://www.oodlestechnologies.com/blogs/AWS-EC2-Expanding-linux-root-partition/)*



<br>
Now with EBS, one important thing to note is that they have really high performance, but they are attached to the EC2 machines. It's just like a computer's hard disk. You can't really use it without a computer, yes? They are therefore restricted. 
</br>


#### - Amazon EFS

![aws_efs.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657989645678/MJzhjDDpN.png align="center")
*Image from [Suraj Jadhav.](https://medium.com/@surajjadhav525k/deployment-of-application-on-aws-using-terraform-efs-service-d3cf522242fa)*


<br>
With EFS, it is usually needed when several EC2 machines have been fired up, say 10-1,000 , and they need a connected storage system so they can mutually gain access to the data stored.


 Think of it this way; we have two EC2 machines. Each machine has it's own EBS storage. One day, the first machine needs the data stored in the second machine, but the EBS volumes are not connected. With EFS, instead of each machine having its own storage, it acts like a storage pool. So all these machines can access data from each other. 
</br>


### *2. Use Cases*

#### - Amazon S3
<br>
Because it's a simple storage system which is accessible over the internet, some of its use cases include;

- Storing videos, images 
- Hosting static websites
- Creating backups and archives
</br>


<br>
A company like Netflix would greatly benefit from S3, since all their movies could be stored there, and only retrieved when Cyndie wants to watch marvel! We'll also discuss why they are great for backups on availability and durability.
</br>


#### - Amazon EBS
<br>
Because of it's low latency, EBS is great for any workload which requires frequent access with really low downtime. An example would be;

- Hosting an OS (Operating System) and its database.
</br>


<br>
So say you want to run Linux on your computer virtually, and you fire up a Linux virtual machine using AWS, EBS would be the storage option for you. 
</br>


#### - Amazon EFS
<br>
As earlier explained, EFS is a great option when say you have 50 Linux virtual machines running, so instead of having 50 EBS volumes you have one storage pool. It's therefore great for;

- Shared files access
- Big data analytics
- Huge workflows
- Container storage (Kubernetes for eg uses EFS). You can learn more about containers [here.](https://www.intel.com/content/www/us/en/cloud-computing/containers.html)
</br>

N.B: With EFS, there's a specific file system for Windows, known as Amazon FSx for Windows. You can learn more about FSx [here.](https://aws.amazon.com/fsx/) 



### *3. Availability and Durability*
<br>
With *availability*, this means that the systems are operating so you get your requests on time. So nothing is lagging or 'hanging'.
</br>
<br>
With *durability*, think of long-term storage. What you've stored can go for 10 years without getting corrupted or lost.
</br>


With that in mind, let's go through our 3 storage types.



#### - Amazon S3


![s3availabilityTable.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1657979213644/jKcHbuSn-.jpg align="center")
*image from [UnixArena.](https://www.unixarena.com/2017/06/amazon-aws-s3-storage-overview-part-6.html/)*


<br>
As you can see, S3 has 99.999999999% (11 9's) durability! Meaning if say you stored 10 million objects in S3, the probability of losing a single object is once in 10,000 years! This is why S3 is the best when it comes to backups and long-term storage.
</br>

<br>
As for availability, S3 is 99.99% . Compared to its durability, it's availability is on a lower scale. This is why it's not advisable to store data needed frequently and urgently on S3. But for long-term storage, it's the best!
</br>


#### - Amazon EBS

<br>
EBS has an availability of 99.999%, which makes it best for critical workloads which require very low downtime. As for durability, it ranges between 99.8 to 99.9% depending on the type of EBS volume used, therefore it's not advisable for long term storage.
</br>

<br>
EBS is therefore great for running critical applications which need really low downtime, but it's not great for long-term storage. 
</br>


#### - Amazon EFS

<br>
Like S3, EFS has 11 9's durability scale. It is highly available within an AWS region. The best practice with EFS, would be to create backups within different [AWS Availability Zones](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/), so you know, just in case a whole zone goes up in flames!! 😂😂
</br>

Otherwise, EFS has the same performance metrics as S3.


### *4. Costs*
Finally, let's top off with Costs!

#### - Amazon S3

![s3pricing.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657981587071/XNsxKQAWF.png align="center")
*Image from [AWS Documentation](https://aws.amazon.com/s3/pricing/?nc=sn&loc=4)*


<br>
S3 is the cheapest storage cost, with a [pay-as-you-go](https://digitalcloud.training/aws-billing-and-pricing/#:~:text=AWS%20works%20on%20a%20pay%20as%20you%20go,for%20a%20service%20when%20you%20stop%20using%20it.) model. Meaning you pay for only what you use.
</br>

<br>
The prices also vary depending on the type of storage one needs. Example, for long term storage, an S3 storage class known as [S3 Glacier](https://aws.amazon.com/s3/storage-classes/glacier/) would be more appropriate. 
</br>


#### - Amazon EBS

![AWS EBS pricing](https://cdn.hashnode.com/res/hashnode/image/upload/v1657982493547/JKnFDfYkZ.png align="center")
*Image from [AWS Documentation.](https://aws.amazon.com/ebs/pricing/)*


<br>
So EBS is a more expensive option as compared to S3. Something to note here is that with EBS, you pay for provisioned capacity. Meaning if you provision a volume of 5 TB to your machine, even if you use 2 TB, you'll still pay for the 5 TB. Also, like S3, the pricing also depends on the type of storage volume. You can learn more about EBS volumes [here.](https://aws.amazon.com/ebs/)
</br>


#### - Amazon EFS

![AWS EFS Pricing](https://cdn.hashnode.com/res/hashnode/image/upload/v1657983114134/d11PYbnmI.png align="center")
*Image from [AWS Documentation](https://aws.amazon.com/efs/pricing/)*


Now EFS might be the most expensive of the three, but it can be more cost-efficient compared to EBS, since it serves multiple EC2 instances at once. So instead of paying for say 50 EBS volumes, you just pay  for an EFS with a higher capacity. You can learn more about EFS [here.](https://aws.amazon.com/efs/)


<br>
With that, let's top off with a lovely decision tree I came across the internet! It is used to show which factors to consider when choosing a storage option for your business, to help choose the most appropriate solution!.
</br>
![AWS Storage Decision Tree.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657983782424/QDOFuxApV.png align="center")


I got it from [AWS Training Center.](https://www.youtube.com/watch?v=6vNC_BCqFmI) It's just to show how to choose a service appropriate for your needs, by making a decision tree.

<br>
BTW!! Imagine you are using all these services, and you need to create backups of everything, and manage them. With [AWS Backup](https://aws.amazon.com/backup/?whats-new-cards.sort-by=item.additionalFields.postDateTime&whats-new-cards.sort-order=desc), you can create a centralized backup system, so you manage all your backups in a central position, instead of having to manage separate backups. Pretty cool right? 😍😍 
</br>

<br>
And once again, a friendly reminder:

> Always Backup Your Data! To avoid heartbreak and other short stories 💔.

</br>

<br>
See yah around the block! I'll be delving deeper into the storage options one by one. It's time I know create a mini series! See you soon. Who knows? I'll prolly be done with that zombie apocalypse book by then! Adios 😚😚. 
</br>



![casual-life-3d-excited-young-woman-receiving-like-notifications-on-her-laptop.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657987834369/v7ggLmiXU.png align="center")



    







 
