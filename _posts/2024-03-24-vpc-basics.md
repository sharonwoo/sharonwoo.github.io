---
title: "AWS SAA-C03 part 5: Virtual Private Cloud Basics"
categories:
  - exams
tags:
  - aws-saa-c03
---


## vpc-vpc-sizing-and-structure-1.txt

Welcome back. In this lesson, I'm going to cover a topic that many courses don't bother with, how to design a well-structured and scalable network inside AWS using a VPC. Now, this lesson isn't about the technical side of VPC, it's about how to design an IP plan for a business, which includes how to design an individual network within that plan, which when running in AWS means designing a VPC.

So let's get started and take a look because this is really important to understand, especially if you're looking to design real world solutions or if you're looking to identify any problems or performance issues in exam questions. Now, during this section of the course, you'll be learning about and creating a custom VPC, a private network inside AWS. When creating a VPC, one of the first things you'll need to decide on is the IP range that the VPC will use.

The VPC CIDR. You can add more than one, but if you take architecture seriously, you need to know what range the VPC will use in advance, even if that range is made up of multiple smaller ranges, you need to think about this stuff in advance. Deciding on an IP plan and VPC structure in advance is one of the most critically important things you will do as a solutions architect because it's not easy to change later and it will cause you a world of pain if you don't get it right.

Now, when you start this design process, there are a few things that you need to keep in mind. First, what size should the VPC be? This influences how many things, how many services can fit into that VPC.

Each service has one or more IPs and they occupy the space inside a VPC. Secondly, you need to consider other networks that you'll use or that you'll need to interact with. In the previous lesson, I mentioned that overlapping or duplicate ranges would make network communication difficult, so choosing widely at this stage is essential.

Be mindful about ranges that other VPCs use, ranges which are utilized in other cloud environments, on other on-premises networks, and even partners and vendors. Try to avoid ranges which other parties use which you might need to interact with and be cautious. If in doubt, assume the worst.

You should also aim to predict what could happen in the future. What the situation is now is important, but we all know that things change, so consider what things could be like in the future. You'll also need to consider the structure of the VPC.

For a given IP range that we allocate to a VPC, it will need to be broken down further. Every IT network will have tiers, web tier, application tier and database tier are three common examples but there are more, and these will depend on your exact IT architecture. Tiers are things which separate application components and allow different security to be applied, for example.

Modern IT systems also have different resiliency zones known as availability zones in AWS. Networks are often split and parts of that network are assigned to each of these zones. These are my starting points for any systems design.

As you can see, it goes beyond the technical considerations and rightfully so. A good solid infrastructure platform is just as much about a good design as it is about a good technical implementation. So since this course is structured around a scenario, what do we know about the Animals4Life organization so far?

We know that the organization has three major offices, London, New York and Seattle. That will be three IP address ranges which we know are required for our global network. We don't know what those networks are yet, but as solutions architects, we can find out by talking to the IT staff of the business.

We know that the organization have field workers who are distributed globally, and so they'll consume services from a range of locations, but how will they connect to the business? Will they access services via web apps? Will they connect to the business networks using a virtual private network or VPN?

We don't know, but again, we can ask the question to get this information. What we do know is that the business has three networks which already exist, 192.168.10.0/24 which is the business's on-premise network in Brisbane. 10.0.0.0/16 which is a network used by an existing AWS Pilot.

And finally, 172.31.0.0/16, which is used in an existing Azure Pilot. These are all ranges our new AWS network design cannot use and also cannot overlap with. We might need to access data in these networks.

We might need to migrate data from these networks or in the case of the on-premises network, it will need to access our new AWS deployment, so we have to avoid these three ranges. And this information that we have here is our starting point, but we can obtain more by asking the business. Based on what we already know, we have to avoid 192.168.10.0/24.

We have to avoid 10.0.0.0/16, and we have to avoid 172.31.0.0/16. These are confirmed networks that are already in use. And let's also assume that we've contacted the business and identified the other on-premises networks, which are in use by the business.

192.168.15.0/24 is used by the London office. 192.168.20.0/24 is used by the New York office and 192.168.25.0/24 is used by the Seattle office. We've also received some disturbing news.

The vendor who previously helped Animals4Life with their Google Cloud proof of concept cannot confirm which networks are in use in Google Cloud. But what they have told us is that the default range is 10.128.0.0/9 and this is a huge amount of IP address space. It starts at 10.128.0.0 and runs all the way through to 10.255.255.255, and so we can't use any of that if we're trying to be safe, which we are.

So this list would be my starting point. When I'm designing an IP addressing plan for this business, I would not use any of this IP address space. Now, I want you to take a moment, pause the video if needed and make sure you understand why each of these ranges can't be used.

Start trying to become familiar with how the network address and the prefix map onto the range of addresses that the network uses. You know that the IP address represents the start of that range. Can you start to see how the prefix helps you understand the end of that range?

Now, with the bottom example for Google, remember that a /8 is one fixed value for the first octet of the IP and then anything else. Google's default uses a /9, which is half of that. So it starts at 10.128 and uses the remainder of that 10.

Space, so 10.128 through to 10.255. Another interesting fact. The Azure Network is using the same IP address range as the AWS Default VPC users, so 172.31.0.0.

And that means that we can't use the default VPC for anything production, which is fine because as I talked about earlier in the course, as architects, where possible, we avoid using the default VPC. So at this point, if this was a production process, if we were really designing this for a real organization, we'd be starting to get a picture of what to avoid. So now it's time to focus on what to pick.

Now, there is a limit on VPC sizing in AWS. A VPC can be at the smallest a /28 network. So that's 16 IP addresses in total.

And at most, it can be a /16 network, which is just over 65,000 IP addresses. Now I do have a personal preference, which is to use networks in the 10 range, so 10.x.y.z, and given the maximum VPC size, this means that each of these /16 networks in this range would be 10.1, 10.2, 10.3, all the way through to 10.255. I also find it important to avoid common ranges and in my experience, this is logically 10.0 because everybody uses that as a default and 10.1, because as human beings, everybody picks that one, to avoid 10.0.

I'd also avoid anything up to and including 10.10 to be safe. And just because I like base two numbers, I would suggest the starting point of 10.16. With this starting point in mind, we need to start thinking about the IP plan for the Animals4Life business.

We need to consider the number of networks the business will need because we'll allocate these networks starting from this 10.16 point in the 10 range. Now, the way I normally determine how many ranges a business requires is I like to start thinking about how many AWS regions the business will operate in. Be cautious here and think of the highest possible number of regions that a business could ever operate in and then add a few as a buffer.

At this point, we're going to be pre-allocating things in our IP plan, so caution is the term of the day. I suggest ensuring that you have at least two ranges which can be used in each region, in each AWS account that your business uses. For Animals4Life, we really don't yet know how many regions the business will be operating in, but we can make an educated guess and then add some buffer to protect us against any growth.

Let's assume that the maximum number of regions the business will use is three regions in the U.S., one in Europe and one in Australia. That's a total of five regions. We want to have two ranges in each region, so that's a total of five times two, so 10 ranges.

And we also need to make sure that we've got enough for all of our AWS accounts, so I'm going to assume four AWS accounts. So that's a total number of IP ranges of two in each of five regions, so that's 10. And then that in each of four accounts, so that's a total of ideally 40 IP ranges.

So to summarize where we are, we're going to use the 10 range. We're going to avoid 10.0 to 10.10 because they're far too common. We're going to start at 10.16, because that's a nice clean base two number.

And we can't use 10.128 through to 10.255, because potentially that's used by Google Cloud. So that gives us a range of possibilities from 10.16 to 10.127 inclusive, which we can use to create our networks. And that's plenty.

Okay, so this is the end of part one of this lesson. It was getting a little bit on the long side and so I wanted to add a break. It's an opportunity just to take a rest or grab a coffee.

Part two will be continuing immediately from the end of part one. So go ahead, complete the video and when you're ready, join me in part two.

## vpc-vpc-sizing-and-structure-2.txt

Welcome back. This is part two of this lesson. We're gonna continue immediately from the end of part one.

So let's get started. That's a good starting point for our plan. Before I elaborate more on that plan though, let's think about VPC sizing and structure.

AWS provide some useful pointers on VPC sizing, which I'll link to in the lesson text, but I also want to talk about it briefly in this lesson. They define micro as a /24 VPC with eight subnets inside it. Each subnet is a /27, which means 27 IP addresses per subnet, and a total of 216.

This goes all the way through to extra large, which is a /16 VPC, with 16 subnets inside, each of which is a /20, offering 4091 IP addresses per subnet, for a total of just over 65,000. And deciding which to use, there are two important questions. First, how many subnets will you need in each VPC?

And second, how many IP addresses will you need in total? And how many IP addresses in each subnet? Now deciding how many subnets to use, there's actually a method that I use all of the time which makes it easier.

Let's look at that next. So this is the shell of a VPC, but you can't just use a VPC to launch services into. That's not how it works in AWS.

Services use subnets, which are where IP addresses are allocated from. VPC services run from within subnets, not directly from the VPC. And if you remember all the way back at the start of the course, where I introduced VPCs and subnets, I mentioned that a subnet is located in one Availability Zone.

So the first decision point that you need to think about, is how many Availability Zones your VPC will use. This decision impacts high availability and resilience, and it depends somewhat on the region that the VPC is in, since some regions are limited in how many Availability Zones they have. Some have three, some have more.

So step one is to pick how many Availability Zones your VPC will use. Now, I'll spoil this and make it easy. I always start with three as my default.

Why? Because it will work in almost any region. But I also always add a spare, because we all know at some point things grow, so aim for at least one spare.

And this means as a minimum four Availability Zones, A, B, C, and the spare. If you think about it, that means that we have to at least split the VPC into at least four smaller networks. So if we started with a /16, we would now have four /18s.

As well as the Availability Zones inside of EPC, we also have tiers, and tiers are for different types of infrastructure that are running inside that VPC. We might have a web tier, an application tier, a database tier, that makes three and you should always add buffer. So my default is to start with four tiers.

Web, application, database, and a spare. Now the tiers used in your architecture might be different, but my default for most designs is to assume three, plus a spare. So web, application, database, and then a spare for future use.

If you only used one Availability Zone, then each tier would need its own subnet, meaning four subnets in total, but we also have four AZs. And since we want to take full advantage of the resiliency provided by these AZs, we need the same base networking duplicated in each Availability Zone. So each tier has its own subnet in each Availability Zone, four web subnets, four app subnets, four database subnets, and four spares, for a total of 16 subnets.

So if we chose a /16 for the VPC, that would mean that each of the 16 subnets would need to fit into that /16. So a /16 VPC split into 16 subnets results in 16 smaller network ranges, each of which is a /20. Remember, each time the prefix is increased from 16 to 17 it creates two networks, from 16 to 18 it creates four, from 16 to 19 it creates eight, and from 16 to 20, it creates 16 smaller networks.

Now that we know that we need 16 subnets, we could start with a /17 VPC, and then each subnet would be a /21. Or we could start with a /18 VPC, and then each subnet would be a /22, and so on. Now that you know the number of subnets, and because of that, the size of the subnets in relation to the VPC prefix size, picking the size of the VPC is all about how much capacity you need.

Whatever prefix you pick for the VPC, the subnets will be four steps away. So let's move on to the last part of this lesson, where we're going to be deciding exactly what to use. Now, Animals4Life is a global organization already, but with what's happening environmentally around the world, the business could grow significantly, and so when designing the IP plan for the business, we need to assume a huge level of growth.

We've talked about a preference for the 10 range, but avoiding the common networks and avoiding Google gives us 10.16 to 10.127 to use as /16 networks. We have five regions that we're going to be assuming the business will use, three to be chosen in the US, one in Europe, and one in Australia. So if we start at 10.16, and break this down into segments, we could choose to use 10.16 to 10.31 as US region one, 10.32 to 10.47 as US region two, 10.48 to 10.63 as US region three, 10.64 to 10.79 as Europe, and 10.80 to 10.95 as Australia.

That is a total of 16 /16 network ranges for each region. Now we have a total of three accounts right now, General, Prod, and Dev, and let's add one more buffer. So that's four total accounts.

So if we break down those ranges that we've got for each region, break them down into four, one for each account, then each account in each region gets four /16 ranges, enough for four VPCs per region per account. So I've created this PDF, and I've included it attached to this lesson, and in this lesson's folder on the course GitHub repository. So if you go into VPC-Basics, in there is a folder called VPC Sizing and Structure, and then in this folder is a document called A4L, for Animals4Life, _IPplan.PDF.

And this is that document. So I've just tried to document here exactly what we've done with these different ranges. So starting at the top here, we've blocked off all of these networks, these are common ranges to avoid, and we're starting at 10.16 for Animals4Life.

And then starting at 10.16, I've blocked off 16 /16 networks for each region. So US region one, region two, region three, Europe, and Australia, and then we're left with some that are unused, and they're reserved. After that of course, from 10.128 onwards, that's reserved for the Google Cloud usage, which we're uncertain about.

So all the way to the end, that's blocked off. And then within each region, we've got three AWS accounts that we know about, General, Prod, and Dev, and then one set for reserved future use. So in the region, each of those accounts has four class B networks, enough for four non-overlapping VPCs.

So feel free to look through this document, I've included the PDF, and the original Apple Numbers document. So feel free to use this, adjust this for your network, and just experiment with some IP planning. But this is the type of document that I will be using as a starting point for any large AWS deployments.

And we're going to be using this throughout this course to plan the IP address ranges whenever we're creating a VPC. We obviously won't be using all of them, but we will be using this as a foundation. Now, based on that plan, that means we have a /16 range to use for each VPC in each account in each region, and these are non-overlapping.

Now I'm going to be using the VPC structure that I've demonstrated earlier in this lesson. So I'll be assuming the usage of three Availability Zones plus a spare, and three application tiers plus a spare. And this means that each VPC is broken down into a total of 16 subnets, and each of those subnets is a /20 subnet, which represents 4,091 IP addresses per subnet.

Now this might seem excessive, but we have to assume the highest possible growth potential for Animals4Life. We've got the potential growth of the business, we've got the current situation with the environment, and the raising profile of animal welfare globally. So there is a potential that this business could grow rapidly.

This process might seem vague and abstract, but it's something that you'll need to do every time you create a well-designed environment in AWS. You'll consider the business needs, you'll avoid the ranges that you can't use, you'll allocate the remainder based on your business' physical or logical layout, and then you'll decide upon and create VPC and subnet structure from there. You'll always work either top down or bottom up.

You can start with the minimum subnet size that you need and work up, or start with the business requirements and work down. When we start creating VPCs and services from now on in the course, we will be using this structure, and so I will be referring back to this lesson and that PDF document constantly, so you might want to save it somewhere safe, or print it out, make sure you've got a copy handy, because we will be referring back to it constantly as we are deciding upon our network topology throughout the course. With that being said though, that's everything I wanted to cover in this lesson.

I hope it's been useful. I know it's vague and a little bit abstract, but I wanted to step you through the process that a real world solutions architect would use when deciding on the size of subnets and the VPCs, as well as the different structure these network components would have in relation to each other, so the IP plan. But at this point, that is it with the abstract theory, from this point onward in this section of the course, we're going to start talking about the technical aspects of AWS private networking, starting with VPCs and VPC subnets.

So go ahead, complete this video, and when you're ready, you can move on to the next.

## vpc-custom-vpcs-1.txt

Welcome back. Over the remaining lessons in this section, you're going to learn how to build a complex, multi-tier custom VPC step-by-step. One of the benefits of the VPC product is that you can start off simple and layer components in piece by piece.

This lesson will focus on just the VPC shell, but by the end of this section you'll be 100% comfortable building a pretty complex private network inside AWS. So let's get started. Now, don't get scared off by this diagram, but this is what we're going to implement together in this section of the course.

Right now, it might look complicated, but it's like building a Lego project. We'll start off simple and add more and more complexity as we go through the section. This is a multi-tier custom VPC.

If you look at the IP plan document that I linked in the last lesson, it's using the IP address of the first range of the U.S. Region one for the general account, so 10.16.0.0/16 So the VPC will be configured to use that range. Inside the VPC, there'll be space for four tiers running in four Availability Zones for a total of 16 possible subnets.

Now, we'll be creating all four tiers. So reserved, database, app and web, but only three Availability Zones, A, B, and C. We won't be creating any subnets in the capacity reserved for the future Availability Zone.

So that's the part at the bottom here. In addition to the VPC that we'll create in this lesson, the subnets that we'll create in the following lessons, we'll also, as we move through the section of the course, be creating an internet gateway which will give resources in the VPC public access. We'll be creating NAT gateways which will give private instances outgoing only access, and we'll be creating a bastion host which is one way that we can connect into the VPC.

Now, using bastion hosts is frowned upon and isn't best security practice for getting access to AWS VPCs, but it's important that you understand how not to do something in order to appreciate good architectural design. So I'm going to step you through how to implement a bastion host in this part of the course, and as we move through later sections of the course, you'll learn more secure alternatives. Finally, later on in the section, we'll also be looking at network access control lists, or NACLs, which can be used to secure the VPC as well as data transfer costs for any data that moves in and around the VPC.

Now, this might look intimidating, but don't worry. I'll be explaining everything every step of the way. To start with though, we're going to keep it simple and just create the VPC.

Before we do create the VPC, I want to cover some essential architectural theory, so let's get started with that. VPCs are a regionally isolated and regionally resilient service. A VPC is created in a Region, and it operates from all of the AZs in that Region.

It allows you to create isolated networks inside AWS. So even in a single Region in an account, you can have multiple isolated networks. Nothing is allowed in or out of a VPC without a piece of explicit configuration.

It's a network boundary, and it provides an isolated blast radius. What I mean by this is if you have a problem inside a VPC, so if one resource or a set of resources are exploited, the impact is limited to that VPC or anything that you have connected to it. I talked earlier in the course about the default VPC being set up by AWS using the same static structure of one subnet per Availability Zone, using the same IP address ranges, and requiring no configuration from the account administrator.

Well, custom VPCs are pretty much the opposite of that. They let you create networks with almost any configuration, which can range from a simple VPC to a complex multi-tier one, such as the one that we're creating in this section. Custom VPCs also support hybrid networking, which let you connect your VPC to other cloud platforms as well as on-premises networks, and we'll cover that later on in the course.

When you create a VPC, you have the option of picking default or dedicated tenancy. This controls whether the resources created inside the VPC are provisioned on shared hardware or dedicated hardware. Be really careful with this option.

If you pick default, then you can choose on a per resource basis later on when you provision resources as whether it goes on shared hardware or dedicated hardware. If you pick dedicated tenancy at a VPC level, then that's locked in. Any resources that you create inside that VPC have to be on dedicated hardware.

So you need to be really careful with this option because dedicated tenancy comes at a cost premium and my rule on this is unless you really know that you require dedicated, then pick default, which is the default option. Now, a VPC can use IP version four private and public IPs. The private CIDR block is the main method of IP communication for the VPC.

So by default, everything uses these private addresses. Public IPs are used when you want to make resources public, when you want them to communicate with the public internet or the AWS public zone, or you want to allow communication to them from the public internet. Now, a VPC is allocated one mandatory private IP version four CIDR block.

This is configured when you create the VPC, which you'll see in a moment when we actually create a VPC. Now, this primary block has two main restrictions. It can be at its smallest, a /28 prefix, meaning the entire VPC has 16 IP addresses, and some of those can't be used.

More on that in the next lesson when I talk about subnets though. At the largest, a VPC can use a /16 prefix, which is 65,536 IPs. Now, you can add secondary IP version four CIDR blocks after creation, but by default at the time of creating this lesson, there's a maximum of five of those, but they can be increased by using a support ticket.

But generally, when you're thinking conceptually about a VPC, just imagine it that it's got a pool of private IP version four addresses, and optionally it can use public addresses. Now, another optional configuration is that a VPC can be configured to use IP version six by assigning a /56 IPv6 CIDR to the VPC. Now, this is a feature set which is still being matured, so not everything works with the same level of features as it does for IP version four.

But with the increasing worldwide usage of IP version six, in most circumstances, you should start looking at applying an IP version six range as default. An important thing about IP version six is that the range is either allocated by AWS, as in you have no choice on which range to use, or you can select to use your own IP version six addresses. Addresses which you own.

You can't pick a block like you can with IP version four. Either let AWS assign it, or you use addresses that you own. Now, IP version six IPs don't have the concept of private and public.

The range of IP version six addresses that AWS uses are all publicly route-able by default, but if you do use them, you still have to explicitly allow connectivity to and from the public internet. So don't worry about security concerns. It just removes an admin overhead because you don't need to worry about this distinction between public and private.

Now, AWS VPCs also have fully featured DNS. It's provided by Route 53 and inside the VPC, it's available on the base IP address of the VPC plus two. So if the VPC is 10.0.0.0, then the DNS IP will be 10.0.0.2.

Now, there are two options which are critical for how DNS functions in a VPC, so I've highlighted both of them. The first is a setting called enableDnsHostnames, and this indicates whether instances with public IP addresses in a VPC are given public DNS host names. So if this is set to true, then instances do get public DNS host names.

If it's not set to true, they don't. The second option is enableDnsSupport, and this indicates whether DNS is enabled or disabled in the VPC. So DNS resolution.

If it is enabled, then instances in the VPC can use the DNS IP address. So the VPC plus two IP address. If this is set to false, then this is not available.

Now, why I mention both of these is if you do have any questions in the exam or any real world situations where you're having DNS issues, these two should be the first settings that you check are switched on or off as appropriate. And in the demo part of this lesson, I'll show you where to access those. Speaking of which, it's now time for the demo component to this lesson, and we're going to implement the framework, the VPC, for the Animals4Life organization together inside our AWS account.

So let's go ahead and finish the theory part of this lesson right now, and then in the next lesson, the demo part, we'll implement this VPC together.

## vpc-custom-vpcs-2.txt

Welcome back. Over the remaining lessons in this section, you're going to learn how to build a complex, multi-tier custom VPC step-by-step. One of the benefits of the VPC product is that you can start off simple and layer components in piece by piece.

This lesson will focus on just the VPC shell, but by the end of this section you'll be 100% comfortable building a pretty complex private network inside AWS. So let's get started. Now, don't get scared off by this diagram, but this is what we're going to implement together in this section of the course.

Right now, it might look complicated, but it's like building a Lego project. We'll start off simple and add more and more complexity as we go through the section. This is a multi-tier custom VPC.

If you look at the IP plan document that I linked in the last lesson, it's using the IP address of the first range of the U.S. Region one for the general account, so 10.16.0.0/16 So the VPC will be configured to use that range. Inside the VPC, there'll be space for four tiers running in four Availability Zones for a total of 16 possible subnets.

Now, we'll be creating all four tiers. So reserved, database, app and web, but only three Availability Zones, A, B, and C. We won't be creating any subnets in the capacity reserved for the future Availability Zone.

So that's the part at the bottom here. In addition to the VPC that we'll create in this lesson, the subnets that we'll create in the following lessons, we'll also, as we move through the section of the course, be creating an internet gateway which will give resources in the VPC public access. We'll be creating NAT gateways which will give private instances outgoing only access, and we'll be creating a bastion host which is one way that we can connect into the VPC.

Now, using bastion hosts is frowned upon and isn't best security practice for getting access to AWS VPCs, but it's important that you understand how not to do something in order to appreciate good architectural design. So I'm going to step you through how to implement a bastion host in this part of the course, and as we move through later sections of the course, you'll learn more secure alternatives. Finally, later on in the section, we'll also be looking at network access control lists, or NACLs, which can be used to secure the VPC as well as data transfer costs for any data that moves in and around the VPC.

Now, this might look intimidating, but don't worry. I'll be explaining everything every step of the way. To start with though, we're going to keep it simple and just create the VPC.

Before we do create the VPC, I want to cover some essential architectural theory, so let's get started with that. VPCs are a regionally isolated and regionally resilient service. A VPC is created in a Region, and it operates from all of the AZs in that Region.

It allows you to create isolated networks inside AWS. So even in a single Region in an account, you can have multiple isolated networks. Nothing is allowed in or out of a VPC without a piece of explicit configuration.

It's a network boundary, and it provides an isolated blast radius. What I mean by this is if you have a problem inside a VPC, so if one resource or a set of resources are exploited, the impact is limited to that VPC or anything that you have connected to it. I talked earlier in the course about the default VPC being set up by AWS using the same static structure of one subnet per Availability Zone, using the same IP address ranges, and requiring no configuration from the account administrator.

Well, custom VPCs are pretty much the opposite of that. They let you create networks with almost any configuration, which can range from a simple VPC to a complex multi-tier one, such as the one that we're creating in this section. Custom VPCs also support hybrid networking, which let you connect your VPC to other cloud platforms as well as on-premises networks, and we'll cover that later on in the course.

When you create a VPC, you have the option of picking default or dedicated tenancy. This controls whether the resources created inside the VPC are provisioned on shared hardware or dedicated hardware. Be really careful with this option.

If you pick default, then you can choose on a per resource basis later on when you provision resources as whether it goes on shared hardware or dedicated hardware. If you pick dedicated tenancy at a VPC level, then that's locked in. Any resources that you create inside that VPC have to be on dedicated hardware.

So you need to be really careful with this option because dedicated tenancy comes at a cost premium and my rule on this is unless you really know that you require dedicated, then pick default, which is the default option. Now, a VPC can use IP version four private and public IPs. The private CIDR block is the main method of IP communication for the VPC.

So by default, everything uses these private addresses. Public IPs are used when you want to make resources public, when you want them to communicate with the public internet or the AWS public zone, or you want to allow communication to them from the public internet. Now, a VPC is allocated one mandatory private IP version four CIDR block.

This is configured when you create the VPC, which you'll see in a moment when we actually create a VPC. Now, this primary block has two main restrictions. It can be at its smallest, a /28 prefix, meaning the entire VPC has 16 IP addresses, and some of those can't be used.

More on that in the next lesson when I talk about subnets though. At the largest, a VPC can use a /16 prefix, which is 65,536 IPs. Now, you can add secondary IP version four CIDR blocks after creation, but by default at the time of creating this lesson, there's a maximum of five of those, but they can be increased by using a support ticket.

But generally, when you're thinking conceptually about a VPC, just imagine it that it's got a pool of private IP version four addresses, and optionally it can use public addresses. Now, another optional configuration is that a VPC can be configured to use IP version six by assigning a /56 IPv6 CIDR to the VPC. Now, this is a feature set which is still being matured, so not everything works with the same level of features as it does for IP version four.

But with the increasing worldwide usage of IP version six, in most circumstances, you should start looking at applying an IP version six range as default. An important thing about IP version six is that the range is either allocated by AWS, as in you have no choice on which range to use, or you can select to use your own IP version six addresses. Addresses which you own.

You can't pick a block like you can with IP version four. Either let AWS assign it, or you use addresses that you own. Now, IP version six IPs don't have the concept of private and public.

The range of IP version six addresses that AWS uses are all publicly route-able by default, but if you do use them, you still have to explicitly allow connectivity to and from the public internet. So don't worry about security concerns. It just removes an admin overhead because you don't need to worry about this distinction between public and private.

Now, AWS VPCs also have fully featured DNS. It's provided by Route 53 and inside the VPC, it's available on the base IP address of the VPC plus two. So if the VPC is 10.0.0.0, then the DNS IP will be 10.0.0.2.

Now, there are two options which are critical for how DNS functions in a VPC, so I've highlighted both of them. The first is a setting called enableDnsHostnames, and this indicates whether instances with public IP addresses in a VPC are given public DNS host names. So if this is set to true, then instances do get public DNS host names.

If it's not set to true, they don't. The second option is enableDnsSupport, and this indicates whether DNS is enabled or disabled in the VPC. So DNS resolution.

If it is enabled, then instances in the VPC can use the DNS IP address. So the VPC plus two IP address. If this is set to false, then this is not available.

Now, why I mention both of these is if you do have any questions in the exam or any real world situations where you're having DNS issues, these two should be the first settings that you check are switched on or off as appropriate. And in the demo part of this lesson, I'll show you where to access those. Speaking of which, it's now time for the demo component to this lesson, and we're going to implement the framework, the VPC, for the Animals4Life organization together inside our AWS account.

So let's go ahead and finish the theory part of this lesson right now, and then in the next lesson, the demo part, we'll implement this VPC together.

## vpc-vpc-subnets.txt

Welcome back and in this lesson, I want to continue the theme of VPC networking in AWS by covering VPC subnets. Now, subnets are what services run from inside VPCs and they're how you add structure, functionality, and resilience to VPCs. So there are an important thing to get right both for production deployment and to do well in the exam.

So, let's not waste time. Let's jump in and get started. In this lesson, we'll be starting off with this architecture.

This is exactly how we left off at the end of the previous lesson, a framework VPC, a skeleton. What we'll be doing is creating an internal structure using subnets. We'll be turning this into this.

Now, if you compare this diagram to the one that I've linked previously, you might notice that the web tier subnets on the right are blue on this diagram instead of green on the diagram that I've previously linked. Now with AWS diagrams, blue means private subnets and green means public subnets. Subnets inside of VPC, start off entirely private and they take some configuration to make them public.

So, at this point, the subnets which will be created on the right, so the web tier, they'll be created as private subnets and in the following lessons, we'll change that together. So for now, this diagram showing them as private subnets is correct. So what exactly is a subnet?

It's an AZ resilient feature of a VPC, a subnetwork of the VPC, a part of the VPC that's inside a specific availability zone. It's created within one availability zone, and it can never be changed. Because it runs inside of an availability zone, if that availability zone fails, then the subnet itself fails.

And so do any services that are only hosted in that one subnet. And as AWS solutions architects, when we design highly available architectures, we're trying to put different components of our system into different availability zones to make sure that if one fails, our entire system doesn't fail. And the way that we do that is to put these components of our infrastructure into different subnets, each of which are located in a specific availability zone.

The relationship between subnets and availability zones is that one subnet is created in a specific availability zone in that region. It can never be changed and a subnet can never be in multiple availability zones. That's an important one to remember for the exam.

One subnet is in one availability zone. A subnet can never be in more than one availability zone. Logically though, one availability zone can have zero or lots of subnets.

So, one subnet is in one availability zone but one availability zone can have many subnets. Now, the subnet, by default, uses IPv4 for networking, and it's allocated an IPv4 CIDR. And this CIDR is a subset of the VPC CIDR block.

It has to be within the range that's allocated to the VPC. What's more, the CIDR that a subnet uses cannot overlap with any other subnets in that VPC. They have to be non overlapping.

That's another topic which tends to come up all the time in the exam. Now, a subnet can, optionally, be allocated an IPv6 CIDR block as long as the VPC also is enabled for IPv6. The range that's allocated to individual subnets is a /64 range.

And that /64 range is a subset of that /56 VPC. So a /56 IPv6 range has enough space for 256/64 ranges that each subnet can use. Now subnets inside of VPC can, by default, communicate with other subnets in that same VPC.

The isolation of a VPC is at the perimeter of the VPC. Internally, there is free communication between subnets by default. Now we've spoken in previous lessons about sizing.

So, sizes of networks are based on the prefix. For example, a /24 network allows values from zero to 255 in the fourth octet. Now that's a possible 256 possible IPs but inside a subnet, you don't get to use them all.

Some IPs inside every VPC subnet are reserved. So let's look at those next. There are five IP addresses within every VPC subnet that you can't use.

So whatever the size of the subnet, the usable IPs are five less than you would expect. Let's assume for example, that the subnet we're talking about is 10.16.16.0/20, so this has a range of 10.16.16.0 to 10.16.31.255. The first address, which is unusable, is the network address.

The first address of any subnet is the one that represents the network, the starting address of the network and it can't be used. This isn't specific to AWS. It's the case for any other IP networks as well.

Nothing uses the first address on a network. Next, is what's known as the network plus one address, the first IP after the network address. And in AWS, this is used by the VPC router, the logical network device which moves data between subnets and in and out of the VPC if it's configured to allow that.

The VPC router has a network interface in every subnet and it uses this network plus one address. Next, is another AWS specific IP address which can't be used, called the network plus two address. In a VPC, the second usable address of the VPC range is used for DNS and AWS reserve the network plus two address in every subnet.

So, I've put DNS and an asterisk here because I refer to this reservation as the DNS reservation, but strictly speaking, it's the second address in a VPC, which is used for DNS. So, that's a VPC range plus two but AWS do reserve the network plus two address in every single subnet. And so you need to be aware of that.

And there's one more AWS specific address that you can't use and you guessed it. It's a network plus three address. This doesn't have a use yet.

It's reserved for future requirements. And this is the network plus three, and this example 10.16.16.3. And then lastly, the final IP address that can't be used in every VPC subnet is the network broadcast address.

Broadcaster not supported inside of VPC but the last IP address in every subnet is reserved regardless. So, you cannot use this last address. So, this makes a total of five IP addresses in every subnet that you can't use, three AWS specific ones, and then the network and broadcast addresses.

So, if a subnet should have 16 IPs, it actually has 11 usable IPs. So keep this in mind, especially when you are creating smaller VPCs and subnets, because this can quickly eat up IP addresses, especially if you use small VPCs with lots of subnets. Now, a VPC has a configuration object apply to it called a DHCP Options Set.

DHCP stands for dynamic host configuration protocol. It's how computing devices receive IP addresses automatically. Now there's one DHCP options set applied to a VPC at one time and this configuration flows through to subnets.

It controls things like DNS servers, NTP servers, net bios servers, and a few other things. If you've ever managed a DHCP server, this will be familiar. So for every VPC, there's a DHCP option set that's linked to it, and that can be changed.

You can create option sets, but you cannot edit them. So, keep in mind, if you want to change the settings you need to create a new one and then change the VPC allocation to this new one. On every subnet, you can also define two important IP allocation options.

The first option controls if resources in a subnet are allocated a public IPv4 address in addition to that private subnet address automatically. Now I'm going to be covering this in the lesson on routing and internet gateway, because there's some additional theory that you need to understand about public IPv4 addresses, but this is one of the steps that you need to do to make a subnet public. So it's on a per subnet basis that you can set auto assign public IPv4 addresses.

Another related option defined at a subnet level is whether resources deployed into that subnet are also given an IPv6 address and logically for that to work, the subnet has to have an allocation as does the VPC. But both of these options are defined at a subnet level and flow onto any resources inside that subnet. Okay, so now it's time for a demo.

That's all the theory that I wanted to cover in this VPC subnet lesson. So, in the demo lesson, we're going to implement the structure inside the VPC together. We're essentially going to change this skeleton VPC into a multi tier VPC that's configured with all of these subnets.

Now it is going to be a fairly detailed demo lesson. You're gonna have to create all of these 12 subnets manually one by one. And out of all of the lessons, the detail really matters on this one.

We need to make sure that you configure this exactly as required so you don't have any issues in future. Now, if you do make any mistakes, I'm going to make sure that I supply a cloud formation template with the next lesson that allows you to configure this in future automatically. But the first time that you do this lesson, I do want you to do it manually because you need to get used to the process of creating subnets.

So controlling what the IP ranges are, being able to select which availability zone they go in, and knowing how to assign IPv6 ranges to those subnets. So, it is worthwhile investing the time to create each of these 12 subnets manually. And that's what we're going to do in the next demo lesson.

But at this point, go ahead and complete this lesson. And then when you've got the time, I'll see you in the next demo lesson where we'll complete the configuration of this VPC by creating the subnets.

## vpc-implement-multi-tier-vpc-subnets.txt

Welcome back and in this demo lesson you're going to create all of the subnets within the custom VPC for Animals for Life. So we're going to create the subnets as shown on screen now. We're going to be creating four subnets in each Availability Zone.

So that's the Web subnet, the Application subnet, the Database subnet and the Reserved subnet. And we're going to create each of those four in Availability Zone A, B and C. Now before we get started, attached to this lesson is a link to this document.

Now this is a list of all of the details of the subnets that you're going to create in this demo lesson. So we've got a Reserved subnet, a Database subnet, an App subnet and a Web subnet. And we've got each of those in Availability Zone A, B and C.

Now in terms of what this document contains, we have a subnet name, then we have the IP range that subnet will use, the Availability Zone that that subnet is within and then this last value. And we'll talk about what this is very shortly. This relates to IP version 6.

Now you'll notice that for each subnet this is a unique value. You're going to need this to configure the IP version 6 configuration for each of the subnets. Now let's get started.

So let's move to the AWS console and you need to be within the VPC console. So if you're not already there, go ahead and type that in the search box at the top and then click to move to the VPC console. And then click on subnets.

Once you've done that, go ahead and click on Create subnet. Now the newest version of the user interface allows you to create multiple subnets at a time. And so we're going to create all four of the subnets in each Availability Zone.

So we'll do this three times. One for Availability Zone A, one for B and one for C. So we'll get started with Availability Zone A and first we need to select the VPC to use.

So click in the VPC ID drop down and select the Animals for Life VPC. Once you've done that, we're going to start with subnet 1 of 1. So let's move to the subnets document.

So it's these subnets that we're going to create and we'll start with the reserved subnet. So copy the name of this subnet into your clipboard and paste it into subnet name. Then change the Availability Zone to AZA.

And then make sure IPv4 is set to manual and move back to the subnets document and copy the IP range that we're going to use and paste that into this box. Then scroll down again and make sure manual input is selected for IPv6. Then click the drop down and select the IPv6 range for the VPC.

Now the VPC uses a /56 IP version 6 range. Because we need our subnets to fit inside this, we're going to make the individual subnet ranges much smaller. So what I'll need you to do, and you'll need to do this each time, is to click on the down arrow and you'll need to click on the down arrow twice.

The first time we'll change it to a /60 and the second time to a /64. Now note in my case how I have 9600. And if I click on this right arrow, it increments this value by 1 each time.

Now this value corresponds to the value in the subnets document. So in this case, 0 0. By changing this value each time, it means that you're giving a unique IP version 6 range to each subnet.

So in this case start off by leaving this set to 0 0. And once you've done that you can click on add new subnet. And we're going to create the next subnet.

So in this case it's SN-DB-A. So enter that name. Change the availability zone to A.

Manual input for IPv4. Copy the IP range for DB-A into your clipboard. Paste that in.

Manual for IP version 6. Change to the VPC range in the drop down. Click the down arrow twice to set this to /64.

And then change this value to 0 1. And again this matches the IPv6 value in the subnets document. Then we'll do the same process for the third subnet.

So click on add new subnet. This time the name is SN-APP-A. Enter that.

Availability zone A. Manual for IPv4. And then paste in the IP range.

Manual for IPv6. And select the VPC range. And then change the subnet block to /64 by clicking the down arrow twice.

And then click the right arrow twice to set 0 2 as the unique value for the subnet. And again this matches the value in the subnets document. Then lastly we're going to do the same thing for the last subnet in availability zone A.

So click on add new subnet. This time it's Web-A. So copy and paste that into the subnet name box.

Set availability zone A. Manual for IPv4. Copy and paste the range from the subnets document.

Manual for IPv6. Select the IPv6 range for the VPC. Click the down arrow twice to set the appropriate size for the subnet IPv6 range.

And then click on the right arrow to change this value to 0 3. Now that's all of the subnets created. All four of them in availability zone A.

So we can scroll all the way down to the bottom. And click on create subnet. And that's going to create all four of those subnets.

And we can see those in this list. Now we're going to follow that same process for availability zone B. So click on create subnet.

Change the VPC to the Animals Fly VPC. And now we're going to start moving through quicker. So first we're going to do the reserved B subnet.

So copy the name. Paste that in. Set the availability zone this time to B.

Manual for IPv4. Paste in the range. Manual for IPv6.

Select the VPC range in the drop down. Click on the down arrow twice to set to /64. And then click on the right arrow and set 0 4 as the unique value.

Scroll down. Click add new subnet. Next is DBB.

Enter that. Availability zone B. Manual for IPv4.

Enter the appropriate range. And just take note of the IPv6 value because then we don't have to keep switching backwards and forwards to this document. In this case it's 05.

Paste in the IPv4 range. Manual for IPv6. Select the VPC range in the drop down.

Down arrow twice. And then the left arrow and set 05 which is the unique value for this subnet. Click add new subnet.

This time it's APP B. Enter that name. Availability zone B.

Manual for IPv4. You'll need to enter the IP range for APP B. And again pay attention to the fact that the unique value for this subnet is 06.

Manual for IPv6. Select the VPC range in the drop down. Down arrow twice.

Right arrow until it says 06. And then add new subnet again and we're going to do the last one. This time it's WebB.

Enter that in the name. Availability zone B in the drop down. Manual for IPv4.

Copy and paste the IP range. And pay attention to 07 which is the IPv6 unique value. So enter the IPv4 subnet range in this box.

Manual for IPv6. Select the VPC range in the drop down. Down arrow twice.

And then right arrow until it says 07. And now we've done all four subnets in AZB so click on create subnet. And then we're going to do this one last time for availability zone C.

So click on create subnet. Select the animals fly VPC in the drop down. And we're going to follow the same process.

So for subnet 1 it will be SN reserved -C. Availability zone C. You'll need to enter the IPv4 range.

Pay attention to the IPv6 unique value which is 08. Paste in that range in the box. Manual for IPv6.

Select the VPC range. Down arrow twice to set to /64. And then right arrow until it says 08.

Scroll down. Add a new subnet. Next is DBC.

So enter that. Availability zone C. And do the same thing as before.

We'll need the IP range and the IPv6 unique value. So 09. Enter that.

Manual for IPv6. Select the VPC range in the drop down. Down arrow twice.

And then click the right arrow until 09 is selected. Add a new subnet. Then the application subnet.

Copy that. Paste it in. Availability zone C.

Get the IPv4 range and the unique value for IPv6. Now note this is hexadecimal. So 0A directly follows 09.

So pay attention to that. Go back. Paste in the IPv4 range.

Manual for IPv6. Select the VPC range. Down arrow twice to select /64.

And then right arrow until you get 0A. Then one last time. Click on add new subnet.

Go back to the subnets document. Web C. Availability zone C.

Get the IPv4 range and note the unique IPv6 value. Paste that in. Select the IPv6 range for the VPC.

Down arrow twice to select /64. And then right arrow all the way through to 0B. And at that point you can go ahead and click on create subnet.

And that's created all four subnets and availability zone C. And all of the subnets now that are within the Animals for Life VPC. At least those in AZA, AZB and AZC.

Once again we're not going to create the ones in AZD. Which are reserved for future growth. Now there's one final thing that we need to do to all of these subnets.

So each of these subnets is allocated with an IP version 6 range. However it's not set to auto allocate IP version 6 addressing. To anything created within each of these subnets.

Now to do that go ahead and select sn-app-a. Click on actions. And then edit subnet settings.

And I want you to check the box to say enable or to assign IP version 6 addresses. Once you've done that scroll to the bottom and click on save. So that's one subnet that you've done that for.

Next I want you to do it for app B. Follow the same process actions, edit subnet settings. Or to assign IP version 6.

Click on save. Notice how we're not touching the IP version 4 setting. We'll be changing that as appropriate later.

Select sn-app-c. And again edit subnet settings. Enable or to assign IP version 6.

And click on save. Then we're going to do the same for the database subnets. So DBA, edit subnet settings.

Enable IPv6 and save. Then DBB. Check this box.

Save. Then DBC. Edit subnet settings.

Check this box. Save. Now we'll do the reserved.

So reserved A. Then reserved B. And then reserved C.

And then finally we're going to do the web subnets. So we'll start with A. Again make sure you're only changing the IP version 6 box.

Save that. Do the same with web B. And then once that's done we'll scroll down and do the final subnet.

So web C. Same process. IPv6 and save.

And at this point you've gone through the very manual process of creating 12 subnets across three availability zones using the architecture that's shown on screen now. Now in production usage and in the real world you would automate this process. You wouldn't do this manually each and every time.

But I think it's important that you understand how to do this process manually. So you can understand exactly what to select when configuring automation to achieve the same end goal. So whenever I'm using automation I always like to understand how it works manually.

So that I can fully understand what it is that that automation is doing. Now at this point that is everything that I wanted to cover in this demo lesson. We're going to be continually evolving this design as we move through this section of the course.

But at this point that is everything I wanted to do. So go ahead and complete this video and when you're ready I'll look forward to you joining me in the next.

## vpc-vpc-routing-internet-gate-way-bastion-hosts.txt

Welcome back, and in this lesson, I want to talk about how routing works within a VPC and introduce the internet gateway, which is how we can configure a VPC so that data can exit to and enter from the AWS public zone on a public internet. Now this lesson will be theory where I'm going to introduce routing and the internet gateway, so the architecture behind both those things as well as jumpboxes also known as bastion hosts. In the demo lesson which immediately follows this one, you'll get the opportunity to implement an internet gateway yourself in the Animals For Life VPC and fully configured the VPC with public subnets that allow you to connect to that jumpbox.

So let's get started, we've got a lot to cover. A VPC router is a highly available device which is present in every VPC, both default or custom, which moves traffic from somewhere to somewhere else. It runs in all of the availability zones that the VPC uses, you never need to worry about its availability.

It simply works. The router has a network interface in every subnet in your VPC, the network+1 address of the subnet. By default in a custom VPC, without any other configuration, the VPC router simply routes traffic between subnets in that VPC.

If an EC2 instance in one subnet wants to communicate with something in another subnet, the VPC router is the thing that moves the traffic between the two. Now the VPC router is controllable, you create route tables which influence what to do with traffic when it leaves a subnet. So just to be clear, the route table that's associated with a subnet defines what the VPC router will do when data leaves that subnet.

A VPC is created with what's known as a main route table. If you don't explicitly associate a custom route table with a sub-net, it uses the main route table of the VPC. If you do associate a route table that you create with a sub-net, then when you associate that, the main route table is disassociated.

A subnet can only have one route table associated with it at any one time, but a route table can be associated with many subnets. A route table looks like this in the user interface. In this case, this is the main route table for this specific VPC.

And a route table is just a list of routes. This is one of those routes. When traffic leaves the subnet that this route table is associated with, the VPC router reviews the IP packets.

And remember, I said that a packet had a source address and a destination address as well as some data. Well the VPC router looks at the destination address of all packets leaving this subnet, and when it has that address, it looks at the route table and it identifies all of the routes which match that destination address. And it does that by checking the destination field of a route.

This destination field determines what destination the route matches. Now the destination field on a route could match exactly one specific IP address. It could be an IP with a /32 prefix, and remember that means that it matches one single IP.

But the destination field on a route could also be a network match. So matching an entire network of which that IP is part, or it could be a default route. Remember for IP version 4, I mentioned that 0.0.0.0/0 matches all IP version 4 IP addresses, that's known as a default route, a catch-all.

In the case where traffic leaving a subnet only matches one route, then that one route is selected. If multiple routes match, so maybe there's a specific /32 IP match, maybe there's a /60 network match, and maybe there is a 0.0.0.0/0 default match, well then the prefix is used as a priority. The higher the prefix value, the more specific the route is and the higher priority that that route has.

So the higher the prefix, all the way up to the highest priority of /32, that is used to select which route applies when traffic leaves a subnet. Once we get to the point where a single rule in a route table is selected, either the sole route that applies or the one with the highest priority, then the VPC router forwards that traffic through to its destination, which is determined by the target field on the route. And the target field will either point at an AWS gateway or it will say, as with this example, local.

And local means that the destination is in the VPC itself. So the VPC router can forward the traffic directly. All route tables have at least one route, the local route.

This matches the VPC CIDR range and it lets the VPC router know that traffic destined for any IP address in the VPC CIDR range is local and it can be delivered directly. If the VPC is also IP version 6 enabled, it will also have another local route matching the IP version 6 CIDR for the VPC as is the case with this example. That bottom route beginning 2600, that is an IP version 6 local route, that's the IP version 6 CIDR of this specific VPC.

Now these local routes can never be updated, they're always present, and the local routes always take priority. They're the exception to that previous rule about the more specific the route is, the higher the priority. Local routes always take priority.

For the exam, remember that route tables are attached to 0 or more subnets, a subnet has to have a route table. It's either the main route table of the VPC or a custom one that you've created. A route table controls what happens to data as it leaves the subnet or subnets that that route table is associated with.

Local routes are always there, uneditable, and match the VPC IP version 4 or 6 CIDR range. For anything else, higher prefix values are more specific and they take priority. The way that a route works is it matches a destination IP, and for that route, it directs traffic towards a specific target.

Now a default route, which I'll talk about shortly, is what happens if nothing else matches. Now an internet gateway is one of the most important add-on features available within a VPC. It's a regionally resilient gateway which can be attached to a VPC.

I've highlighted the words region and resilient because it always comes up in the exam. You do not need a gateway per availability zone, the internet gateway is resilient by design. One internet gateway will cover all of the availability zones in the region which the VPC is using.

Now there's a one-to-one relationship between internet gateways and the VPC. A VPC can have no internet gateways, which makes it entirely private, or it can have one internet gateway. Those are the two choices.

An internet gateway can be created and not attached to a VPC. So it can have zero attachments but it can only ever be attached to one VPC at a time. At which point it's valid in all of the availability zones that the VPC uses.

Now the internet gateway runs from the border of the VPC and the AWS public zone. It's what allows services inside a VPC which are allocated with public IP version 4 addresses or IP version 6 addresses to be reached from the internet and to connect to the AWS public zone or the internet. And of course the AWS public zone is used if you're accessing S3, SQS, SNS, or any other AWS public services from your VPC.

Now it's a managed gateway and so AWS handles the performance. From your perspective as an architect, it simply works. Now using an internet gateway within a VPC, it's not all that complex.

Here's a simplified VPC diagram. First we create and attach an internet gateway to a VPC. This means that it's available for use inside the VPC, we can use it as a target within route tables.

So then we create a custom route table and we associate it with the web subnet. Then we add IP version 4 and optionally IP version 6 default routes to the route table with the target being the internet gateway. Then finally we configure the subnets to allocate IP version 4 addresses, and optionally, IP version 6 by default.

And at that point, once we've done all of those actions together, the subnet is classified as being a public subnet and any services inside that subnet with public IP addresses can communicate to the internet and vice versa and they can communicate with the AWS public zone as long as there's no other security limitations that are in play. Now don't worry if this seems complex, you'll get to experience it shortly in the upcoming demo lesson. But before that, I want to talk about how IP version 4 addressing actually works inside a VPC because I've seen quite a few difficult questions on the exam based around IP version 4 addressing and I want to clarify exactly how it works.

So conceptually, this is how an EC2 instance might look if it's using IP version 4 to communicate with a software update server of some kind. So we've got the instance on the left with an internet gateway in between, and let's say it's a Linux EC2 instance trying to do some software updates to a Linux update server that's located somewhere in the public internet zone. So the instance has a private IP address of let's say 10.16.16.20.

And it also has an IP version 4 public address that's assigned to it of 43.250.192.20. Only, that's not how it really works. This is another one of those little details which I try to include in my training courses because it really comes in valuable for the exam.

What actually happens with public IP version 4 addresses is that they never touch the actual services inside a VPC. Instead, when you allocate a public IP version 4 address, for example, to this EC2 instance, a record is created which the internet gateway maintains. It links the instance's private IP to its allocated public IP.

So the instance itself is not configured with that public IP. That's why when you make an EC2 instance and allocate it a public IP version 4 address, inside the operating system it only sees the private IP address. Keep this in mind for the exam.

There are questions which will try to trip you up on this one. For IP version 4, it is not configured in the OS with the public IP address. So let's look at the flow of data, how does this work?

Well when the Linux instance wants to communicate with the Linux software update server, it creates a packet of data. Now obviously it probably creates a lot of packets, but let's focus on one for now because it keeps the diagram nice and simple. The packet has a source address of the EC2 instance and a destination address of the Linux software update server.

So at this point the packet is not configured with any public addressing. This packet would not be routeable across the public internet. It could not reach the Linux update server, that's really important to realize.

Now the packet leaves the instance and because we've configured a default route, it arrives at the internet gateway. The internet gateway sees that this packet is from the EC2 instance because it analyzes the source IP address of that packet and it knows that this instance has an associated public IP version 4 address. And so it adjusts the packet.

It changes the packet's source IP address to the public IP address that's allocated to that instance and this IP address, because it's public, is routeable across the internet. So the internet gateway then forwards the updated packet onto its destination. So as far as the Linux software update server's concerned, it's receiving a packet from a source IP address of 43.250.192.20.

It knows nothing of the private IP address of this EC2 instance. Now on the way back, the inverse happens. The Linux software update server wants to send a packet back to our EC2 instance, but as far as it's concerned, it doesn't know about the private address.

It just knows about the public address. So the software update server sends a packet back addressed to the instance's public IP address with its source address. So it thinks that the real IP address at the instance is this 43.250.192.20 address.

Now this IP address actually belongs to the internet gateway, and so it travels over the public internet and it arrives at the internet gateway, which then modifies this packet. It changes it, it changes the destination address of this packet from the 43 address to the original IP address of the EC2 instance, and it does this because it's got a record of the relationship between the private IP and the allocated public IP. So it just changes the destination to be the private IP address of the instance, and then it forwards this packet through the VPC network to the original EC2 instance.

So the reason I wanted to highlight this is because at no point is the operating system on the EC2 instance aware of its public IP. It just has a private IP. Don't fall for any exam questions which try to convince you to assign the public IP version 4 address of an EC2 instance directly to the operating system.

It has no knowledge of this public address. Configuring an EC2 instance appropriately using IP version 4 means putting the private IP address only. The public address never touches the instance.

For IP version 6, all addresses that AWS uses are natively, publicly routeable. And so in the case of IP version 6, the operating system does have the IP address version 6 address configured on it, that's the publicly routeable address, and all the internet gateway does is pass traffic from an instance to an internet server and then back again, it doesn't do any translation. Now before we implement this in the demo lesson I just want to briefly touch up on bastion hosts and jumpboxes.

At a high level, bastion host and jumpboxes are one and the same. Essentially, it is just an instance in a public subnet inside a VPC. And architecturally, they're used to allow incoming management connection.

So all incoming management connections arrive at a bastion host or a jumpbox, and then once connected, you can then go on to access internal-only VPC resources. So bastion hosts and jumpboxes are generally used either as a management point or as an entry point for private-only VPCs. So if your VPC is a highly secure private VPC, you'll generally have a bastion host or a jumpbox being the only way to get access to that VPC.

So it's essentially just an inbound management point. And you can configure these bastion hosts or jumpboxes to only accept connections from certain IP addresses, to authenticate with SSH, or to integrate with your on-premises identity servers. You can configure them exactly how you need, but at a real core architectural level, they are generally the only entry point to a highly secure VPC.

And historically they were the only way to manage private EC2 instances. Now there are alternative ways to do that now but you will still find bastion hosts and jumpboxes do feature on the exam. Okay, so that's all of the theory that I wanted to cover in this lesson, it's now time for a demo.

In the next lesson, we're going to implement the internet gateway in the Animals For Life VPC. We'll create it, we'll attach it to the VPC, we'll create a custom route table for the web subnets, we'll create two routes in that route table, one for IP version 4 and one for IP version 6 and both of these will point at the internet gateway as a target. We'll associate that route table with the web tier subnets, configure those subnets to allocate public IP version 4 addresses, and then launch a bastion host into one of those web subnets.

And if all goes well, we will be able to connect to that instance using our SSH application. So I think this demo lesson is gonna be really interesting and really exciting, and it's the first time that we're going to be stepping through something together that we could qualify as production like. It's something that you could implement and would implement in a production-ready VPC.

So go ahead, complete this video, and when you're ready, join me in the demo lesson.

## vpc-configuring-a4l-public-subnets-and-jumpbox-1.txt

Welcome back, and this demo lesson is going to bring together some really important theory and architecture that you've learned over the past few lessons. What we're starting this demo lesson with is this architecture. We have our VPC, the Animals for Life VPC in US East 1.

It uses the 10.16.0.0/16 side range. It has 12 subnets created inside it, over 3 AZs with 4 tiers. Reserved, DB, Application and Web.

Now currently all of the subnets are private and can't be used for communication with the internet or the AWS public zone. In this demo we're going to reconfigure the VPC to allow that. So the first step is to create an internet gateway and attach it.

And to do that I'm going to move across to my desktop. Now to do this in your environment you'll need the VPC and subnet configuration as you set it up in the previous demo lesson. So that configuration needs to be in place already.

You need to be logged in as the IAM admin user of the management account of the organisation and have the Northern Virginia region selected. So US-East-1. So go ahead and move across to the VPC console.

Now this should already be in the recently visited services because you were using this in the previous demo lesson. But if it's not visible just click in the services dropdown, type VPC and then click to move to the VPC console. Now if you do still have the configuration as it was at the end of the previous demo lesson, you should be able to click on subnets on the menu on the left and see a list of lots of subnets.

So you'll see the ones for the default VPC without a name and if you have the correct configuration you should see a collection of 12 subnets, 3 application subnets, 3 database subnets, 3 reserved subnets and then 3 web subnets. So all of these should be in place within the Animals for Life VPC in order to do the tasks within this demo lesson. So I'm going to assume from this point onwards that you do have all of these subnets created and configured.

Now what we're going to be doing in this demo lesson is configuring the 3 web subnets, so Web A, Web B and Web C to be public subnets. Being a public subnet means that you can launch resources into the subnet, have them allocated with a public IP version 4 address and have connectivity to and from the public IP version 4 internet. And in order to enable that functionality there are a number of steps that we need to perform and I want you to get the practical experience of implementing these within your own environment.

Now the first step to making subnets public is that we need an internet gateway attached to this VPC. So internet gateways as I talked about in the previous theory lesson are highly available gateway objects which can be used to allow public routing to and from the internet. So we need to create one, so let's click on internet gateways on the menu on the left.

There will already be an internet gateway in place for the default VPC, remember when you create a default VPC all this networking infrastructure is created and configured on your behalf. But because we've created a custom VPC for Animals4Life we need to do this manually. So to do that go ahead and click on create internet gateway.

We're going to call the internet gateway A4L, so Animals4Life, VPC1 which is the VPC we're going to attach it to and then IGW for internet gateway, so A4L-VPC1-IGW. Now that's the only information that we need to enter so scroll down and click on create internet gateway. Internet gateways are initially not attached to a VPC and we can tell that because it's initially in the detached state so we need to attach this to the Animals4Life VPC.

So click on actions and then attach to VPC. Inside the available VPCs box just click and then select A4L-VPC1. Once selected go ahead and click on attach internet gateway and that will attach our brand new internet gateway to the Animals4Life VPC and that means that it's now available within that VPC as a gateway object which gives the VPC the capability to communicate to and receive communications from the public internet and the AWS public zone.

Now the next step is that we want to make all of the subnets in the web tier public so that services deployed into these subnets can take advantage of this functionality. So we want the web subnets to be able to communicate to and receive communications from the public internet and AWS public services. Now there are a number of steps that we need to do to accomplish this.

We need to create a route table for the public subnets. We need to associate this route table with the three public subnets so WebA, WebB and WebC and then we need to add two routes to this route table. One route will be a default route for IP version 4 traffic and the other will be a default route for IP version 6 traffic.

And both of these routes for their target will be pointing at the internet gateway that you've just created and attached to this VPC. Now this will configure the VPC router to forward any data intended for anything not within our VPC to the internet gateway. Finally, on each of these web subnets we'll be configuring the subnet to auto-assign a public IP version 4 address and that will complete the process of making them public.

So let's perform all of these sets of configuration. So now that we're back at the AWS console we need to create a route table. So go ahead and click on route tables on the menu on the left and then we're going to create a new route table.

First we'll select the VPC that this route table will belong to and it's going to be the Animals4Life VPC. So go ahead and select that VPC and then we're going to give this route table a name. And I like to keep the naming scheme consistent so we're going to use A4L for Animals4Life and then a hyphen, VPC1 because this is the VPC the route table will belong to and then a hyphen RT for route table and then a hyphen and then web because this route table is going to be used for the web subnets.

So we'll go ahead and create this route table then click route tables on the menu on the left. If we select the route table that we've just created, so that's the one that's called A4L-VPC1-RT-web and then just expand this overview area at the bottom we'll be able to see all of the information about this route table. Now there are a number of areas of this which are important to understand.

One is the routes area which lists all of the routes on this route table and the other is subnet associations. This determines which subnets this route table is associated with. So let's go to subnet associations and currently we can see that it's not actually associated with any subnets within this VPC.

We need to adjust that so go ahead and edit those associations and we're going to associate it with the three web subnets. So you need to select WebA, WebB and WebC. Now notice how all of those are currently associated with the main route table of the VPC.

Remember a subnet can only be associated with one route table at a time. If you don't explicitly associate a route table with a subnet then it's associated with the main route table. We're going to change that, we're going to explicitly associate this new route table with the WebA, WebB and WebC subnets.

So go ahead and save that. So now this route table has been associated with WebA, WebB and WebC. Those subnets are no longer associated with the main route table of the VPC.

So now we've configured the association, let's move to routes. And we can see that this route table has two local routes. We've got the IP version 4-sider of the VPC and the IP version 6-sider of the VPC.

So these two routes on this route table will mean that WebA, WebB and WebC will know how to direct traffic towards any other IP version 4 or IP version 6 addresses within the VPC. Now these local routes can never be adjusted or removed but what we can do is add additional routes. So we're going to add two routes, a default route for IP version 4 and a default route for IP version 6.

So we'll do that and we'll start with IP version 4. So we'll edit those routes and then we'll add a route. Now the format for the IP version 4 default route is 0.0.0.0/0 and this means any IP addresses.

Now I've taught elsewhere in the course how there is a priority to routing within a VPC that a more specific route always takes priority. So this route, the /16, is more specific than this default route. So this default route will only affect IP version 4 traffic which is not matched by this local route.

So essentially anything which is IP version 4 which is not destined for the VPC will use this default route. Now we need to pick the Internet Gateway as the target for this route. So click in the target box on this row, select Internet Gateway.

There should only be one that's highlighted, that's the Animals for Life Internet Gateway you created moments ago. So select that and that means that any IP version 4 traffic which is not destined for the VPC side range will be sent to the Internet Gateway. Now we're going to do the same but for IP version 6.

So go ahead and add another route and the format for IP version 6 default routes is double colon forward slash zero. And this is the same architecture, it essentially means that this matches all IP version 6 addresses but it's less specific than the IP version 6 local route on this top row. So this will only be used for any IP version 6 addresses which are not in the IP version 6 VPC side range.

So go ahead and select target, go to Internet Gateway and select the Animals for Life Internet Gateway. And once you've done both of those go ahead and click on save changes. Now this means that we now have two default routes, an IP version 4 default route and an IP version 6 default route.

So this means that anything which is associated with these route tables will now send any unknown traffic towards the Internet Gateway. But what we need to do before this works is we need to ensure that any resources launched into the WebA, WebB or WebC subnets are allocated with public IP version 4 addresses. To do that go ahead and click on subnets.

In the list we need to locate WebA, WebB and WebC. So we'll start with WebA, so select WebA, click on actions and then edit subnet settings. And this time we're going to modify this subnet so that it automatically assigns a public IP version 4 address.

So check this box and click on save and that means that any resources launched into the WebA subnet will be allocated with a public IP version 4 address. Now we need to follow the same process for the other web subnets. So select the WebB subnet, click on actions and then edit subnet settings.

Enable IP version 4, click on save and then do that same process for WebC. So locate WebC, click on actions and then edit subnet settings. And then enable public IP version 4 addresses and click on save.

So that's all of the networking configuration done. We've created an Internet Gateway. We've associated the Internet Gateway with the Animals for Life EPC.

We've created a route table for the web subnets. We've associated this route table with the web subnets. We've added default routes onto this route table pointing at the Internet Gateway as a default IP version 4 and IP version 6 route.

And then we've enabled the allocation of public IP version 4 addresses for WebA, WebB and WebC. OK, so this is the end of part one of this lesson. It was getting a little bit on the long side and so I wanted to add a break.

It's an opportunity just to take a rest or grab a coffee. Part two will be continuing immediately from the end of part one. So go ahead, complete the video and when you're ready, join me in part two.

## vpc-configuring-a4l-public-subnets-and-jumpbox-2

Welcome back, this is part two of this lesson. We're gonna continue immediately from the end of part one, so let's get started. Now the only thing that remains is just to test out this configuration.

And to do that we're going to launch an EC2 instance into the WebA subnet. So click on services and just type EC2 to move across to the EC2 console. Now once we're on the EC2 console, just click on launch instance, then you'll be taken to the launch instance console.

Into the name box, just go ahead and type A4L-Bastian. Scroll down and we're going to create a Bastian instance using Amazon Linux. So click on Amazon Linux.

In the dropdown below, go ahead and select the latest version of Amazon Linux. Just make sure that it does say free tier eligible on the right of this dropdown. Assuming that's all good, just below that make sure that in the architecture dropdown it's set to 64 bit x86.

Moving down further still, under instance type, just make sure that this is set to a free tier eligible instance. It should default to T2.micro or T3.micro. Depending on your region, either of these could be free tier eligible.

In my case it's T2.micro, but whatever yours shows, just make sure that it's similar sized and says free tier eligible. Now directly below that, under key pair, just click in this box. You should, at this point in the course, have a key pair created called A4L.

If you do, go ahead and select that key pair in the box. If you don't, don't worry. You can just go ahead and click on create new key pair, enter A4L into the key pair name, select RSA, and then select PEM for the private key format and click on create key pair.

This will download the key pair to your local machine and then you can continue following along with this video. So select that from the dropdown. Directly below, under network settings, click on edit.

This instance is going to go into the animals for life VPC. So click on the VPC dropdown and select A4L-VPC1. Directly below that, click in the subnet dropdown and we want to go ahead and look for SN-WEB-A.

So select the WEB-A subnet. This should change both of the dropdowns below. So auto assign public IP and auto assign IPv6 IP to enable.

So just make sure that both of those are set to enable. Directly below this, make sure that create security group is checked. We're going to create a new security group.

Under security group name, just go ahead and enter A4L-BASTIAN-SG and then put that same text in the description box directly below. Now all of these defaults should be good. Just make sure it's set to SSH, source, anywhere.

Make sure that 0.0.0.0/0 and double colon forward slash 0 are both present directly below source. Everything else looks good. We can accept the rest of the defaults.

Just go ahead and click on launch instance. Then click on instances at the top left of the screen. And at this point, the instance is launching and we'll see the A4L-BASTIAN is currently running.

We'll see the status check is showing initializing. So we need to give this instance a few minutes to fully provision. So go ahead and pause this video and we're going to resume it once this instance is ready to go.

And it has two out of two status checks. So our instance is now showing two out of two status checks. And that means everything's good and we're ready to connect.

Now, if you select the instance, you'll see in the details pane below how it has a public IP version four address, a private IP version four address, public and private IP version four DNS. And if we scroll down, you'll see lots of other information about this instance. Now we're only concerned with the public IP version four address.

We're going to go ahead and connect to this instance, this time using a local SSH client on our machine. So right click and then select connect. Now, if we want to quickly connect into this instance, we can choose to use EC2 instance connect, which is a way to connect into the instance using a web console.

Now, this does need an instance with a public IP version four address, but we have allocated a public address. So if we wanted to, we can just make sure that the username is correct. It should be EC2-user.

If we hit connect, it will open up a connection to this instance using a web console. And this is often much easier to connect to EC2 instances if you don't have access to a local SSH client, or if you just want to quickly connect to perform some administration. We can also connect with an SSH client.

If we select SSH client, it gives us the commands to run in order to connect to this EC2 instance. So right at the bottom is an example connect command. So SSH, we pick the key to use, and then we pick the user at, and then the public IP version four DNS.

So if we copy that into our clipboard and then move across to our terminal or command prompt, move into the folder where you downloaded the SSH key pair into, in my case, downloads, and paste in that command and press enter, that should connect us to the EC2 instance. We'll have to verify the fingerprint, so we need to verify the authenticity of this host. For this purpose, we can just go ahead and answer yes and press enter.

Now, if it's the first time we're connecting using a particular key, and if you're running either macOS or Linux, you might be informed that the permissions on the key are too open. In this case, the permissions are 0644, which are too open, and we get this error. Now, it's possible to correct that if we move back to the AWS console.

It also gives us the command to correct these permissions. So chmod 400, space, and then the name of the key. So I'm gonna copy that into my clipboard and move back to my terminal, paste that in and press enter, and that will correct those permissions.

Now, if I get the connection command again, so copy that into my clipboard, and this time I'll paste it in and press enter, and now I will be connected to this EC2 instance. Now, if you're doing this demonstration on Windows 10, you probably won't have to correct those permissions. This is something specific to macOS or Linux.

So whenever you're connecting to EC2 instances which have a public IP version 4 address, you've always got the ability to use either EC2 Instance Connect or a local SSH client. Now, the third option, which is Session Manager, this is a way that you can connect to instances even if they don't have public IP version 4 addressing. And I'll be detailing this product fully later on in the course because there is some additional configuration that's required.

Now, this Bastian host, it's an EC2 instance, and it does fall under the free tier. So because it's a t2.micro or whatever type of instance you picked which falls under the free tier, you're not going to be billed for any usage of this instance in a given month. Now, as a general rule, as you're moving through the course, if you're ever intending to take a break, then you always have the option of deleting all of the infrastructure that you've created within a specific demo lesson.

So most of the more complex demo lessons that you'll have moving through the course, at the end of every demo lesson, there will be a brief set of steps where I explain how to clean up the account and return it into the same state as it was at the start of the lesson. But in certain situations, I might tell you that one option is not to delete the infrastructure. Whether you do delete it or not depends on whether you're intending to complete the next demo straight away or whether you're taking a break.

Now, in this particular case, I'm going to demonstrate exactly how you can clear up this infrastructure. In the next demo lesson, you're going to be continuing using this structure, but I'm going to demonstrate how we can automate the creation using a CloudFormation template. To clear up this infrastructure, though, go ahead, right click on this bastion host, and select terminate instance.

You'll need to click terminate to confirm, and that will terminate and delete the instance. You won't be charged for any further usage of that instance. We need to wait for that instance to fully terminate, so pause the video and wait for it to move into a terminated state, and then we can continue.

So that instance is terminated, and now that that's done, we can click on services and move across to the VPC console, and we're going to delete the entire Animals for Life VPC. And don't worry, in the next demo lesson, I'll explain how we can automate the creation. So from now on in the course, we're going to be using much more automation so that anything that you've done previously, we're going to automate the creation and focus your valuable time only on the things that you've just learned.

So click on your VPCs. It should list two VPCs, the default one and the Animals for Life VPC. Select the Animals for Life VPC, click on actions, and then delete the VPC.

Now this is going to delete all of the resources that are associated with this VPC. So the internet gateway, the route tables, and all of the subnets that you've created as part of the demo lessons to this point in the course. So go ahead and type delete, and then click delete to confirm that process, and that will fully tidy up the account and return it into the same state as it was at the start of the VPC section.

Now with that being said, this is the end of this lesson. You've successfully converted three subnets, so Web A, Web B, and Web C to be public, and you've done that by creating an internet gateway, associating that with the VPC, creating a route table, associating that with those subnets, adding two routes, pointing those routes at the internet gateway, and then configuring those subnets to allocate a public IP version four address to any resources launched into those subnets. So that's the same set of steps that you'll need to do to make any subnets public from an IP version four perspective in future.

So this is going to be the same tasks that you would use in larger production projects, although in production, you would probably automate it, and I'm going to show you how to do that as you move through the course. Now at this point, you've finished everything that you need to do in this demo lesson, so great job, you've actually created something that is production ready and production useful. Over the remainder of this section of the course, we're going to refine the design that we've got and add additional capabilities.

So in the upcoming lessons, I'll be talking about network address translation and how that can be used to give private EC2 instances access to the internet for things like software updates. We'll be talking about the security of subnets using network access control lists known as NACLs and much, much more, but you're doing a fantastic job so far. This is not a trivial thing that you've implemented to this point, so really great job, but at this point, just go ahead and complete the video, and then when you're ready, I'll look forward to you joining me in the next.

## vpc-stateful-vs-stateless-firewalls

Welcome back. And in this video, I want to cover the differences between stateful and stateless firewalls. And to do that, I need to refresh your knowledge of how TCP and IP function.

So let's just jump in and get started. In the networking fundamentals videos, I talked about how TCP and IP worked together. You might already know this if you have networking experience in the real world but when you make a connection using TCP, what's actually happening is that each side is sending IP packets to each other.

These IP packets have a source and destination IP and are carried across local networks and the public internet. Now TCP is a Layer 4 protocol which runs on top of IP. It adds error correction together with the idea of ports.

So HTTP runs on TCP port 80, and HTTPS runs on TCP port 443, and so on. So keep that in mind as we continue talking about the state of connections. So let's say that we have a user here on the left, Bob, and he's connecting to the catagram application running on a server on the right.

What most people imagine in this scenario is a single connection between Bob's laptop and the server. So Bob's connecting to TCP port 443 on the server, and in doing so, he gets information back. In this case, many different cat images.

Now you know that below the surface at Layer 3, this single connection is handled by exchanging packets between the source and the destination. Conceptually though, you can imagine that each connection, in this case, it's an outgoing connection from Bob's laptop to the server, each one of these is actually made up of two different parts. First, we've got the request part where the client requests some information from a server, in this case, some cat images.

And then we have the response part where that data is returned to the client. Now these are both parts of the same interaction between the client and server. But strictly speaking, you can think of these as two different components.

What actually happens as part of this connection setup is this; first, the client picks a temporary port and this is known as an ephemeral port. Now typically, this port has a value between 1024 and 65535, but this range is dependent on the operating system which Bob's laptop is using. Then once this ephemeral port is chosen, the client initiates a connection to the server using a well-known port number.

Now a well-known port number is a port number which is typically associated with one specific popular application or protocol. In this case, TCP port 443 is HTTPS. So this is the request part of the connection.

It's a stream of data to the server. You're asking for something, some cat pictures or a webpage. Next, the server responds back with the actual data.

The server connects back to the source IP of the request part, in this case, Bob's laptop. And it connects to the source port of the request part which is the ephemeral port, which Bob's laptop has chosen. This part is known as the response.

So the request is from Bob's laptop using an ephemeral port to a server using a well-known port. The response is from the server on that well-known port, to Bob's laptop on the ephemeral port. Now it's these values which uniquely identify a single connection.

So that's a source port and source IP and a destination IP and a destination port. Now I hope that this makes sense so far. If not, then you need to repeat this first part of the video again because this is really important to understand.

If it does make sense, then let's carry on. Now let's look at this example in a little bit more detail. This is the same connection that we looked at on the previous screen.

We have Bob's laptop on the left, and the catagram server on the right. Obviously, the left is the client, and the right is the server. I also introduced the correct terms on the previous screen.

So request and response. So the first part is the client talking to the server, asking for something, and that's the request. And the second part is the server responding, and that's the response.

But what I want to get you used to is that the directionality depends on your perspective. And let me explain what I mean. So in this case, the client initiates the request.

And I've added the IP addresses on here for both the client and the server. So what this means is that packets will be sent from the client to the server, and these will be flowing from left to right. These packets are going to have a source IP address of 119.18.36.73, which is the IP address of the client, so Bob's laptop.

And they will have a destination IP of 1.3.3.7, which is the IP address of the server. Now the source port will be a temporary or ephemeral port chosen by the client. And the destination port will be a well-known port.

In this case, we are using HTTPS, so TCP port 443. Now, if I challenge you to take a quick guess, would you say that this request is outbound or inbound? If you had to pick, if you had to define a firewall rule right now, would you pick inbound or outbound?

Well, this is actually a trick question because it's both. From the client perspective, this request is an outbound connection. So if you're adding a firewall rule on the client, you would be looking to allow or deny an outbound connection.

From the server perspective though, it's an inbound connection. So you have to think about perspective when you're working with firewalls. But then we have the response part from the server through to the client.

This will also be a collection of packets moving from right to left. This time, the source IP on those packets will be 1.3.3.7, which is the IP address of the server. The destination IP will be 119.18.36.73, which is the IP address of the client, so Bob's laptop.

The source port will be TCP port 443, which is the well-known port for HTTPS. And the destination port will be the ephemeral port chosen originally by the client. Now, again, I want you to think about the directionality of this component of the communication.

Is it outbound or inbound? Well, again, it depends on perspective. The server sees it as an outbound connection from the server to the client, and the client sees it as an inbound connection from the server to itself.

Now, this is really important because there are two things to think about when dealing with firewall rules. The first is that each connection between a client and a server has two components, the request and the response. So the request is from a client to a server and the response is from a server to a client.

The response is always the inverse direction to the request but the direction of the request isn't always outbound and isn't always inbound. It depends on what that data is, together with your perspective. And that's what I want to talk about a bit more on the next screen.

Let's look at this more complex example. We still have Bob and his laptop and the catagram server but now we have a software update server on the bottom-left. Now the catagram server is inside a subnet, which is protected by a firewall.

And specifically, this is a stateless firewall. A stateless firewall means that it doesn't understand the state of connections. What this means is that it sees the request connection from Bob's laptop to catagram, and the response, so from catagram to Bob's laptop, as two individual parts.

You need to think about allowing or denying them as two parts. You need two rules. In this case, one inbound rule, which is the request; and one outbound rule for the response.

This is obviously more management overhead, two rules needed for each thing; each thing which you as a human see as one connection. But it gets slightly more confusing than that. For connections to the catagram server, so for example, when Bob's laptop is making a request, then that request is inbound to the catagram server.

The response logically enough is outbound, sending data back to Bob's laptop. But it's possible to have the inverse. Consider the situation where the catagram server is performing software updates.

Well in this situation, the request will be from the catagram server to the software update server, so outbound; and the response will be from the software update server to the catagram server, so this is inbound. So when you're thinking about this, start with the request. Is the request coming to you or going to somewhere else?

The response will always be in the reverse direction. So this situation also requires two firewall rules; one outbound for the request, and one inbound for the response. Now there are two really important points I want to make about stateless firewalls.

First, for any servers where they accept connections and where they initiate connections. And this is common with web servers which need to accept connections from clients but where they also need to do software updates. In this situation, you'll have to deal with two rules for each of these and they will need to be the inverse of each other.

So get used to thinking that outbound rules can be both the request and the response, and inbound rules can also be the request and the response. It's initially confusing but just remember, start by determining the direction of the request, and then always keep in mind that with stateless firewalls, you're going to need an inverse rule for the response. Now the second important thing is that the request component is always going to be to a well-known port.

If you're managing the firewall for the catagram application, you'll need to allow connections to TCP port 443. The response though, is always from the server to a client. But this always uses a random ephemeral port.

Because the firewall is stateless, it has no way of knowing which specific port is used for the response. So you'll often have to allow the full range of ephemeral ports to any destination. This makes security engineers uneasy which is why stateful firewalls, which I'll be talking about next, are much better.

Just focus on these two key elements that every connection has a request and a response. And together with those, keep in mind the fact that they can both be in either direction. So a request can be inbound or outbound, and a response will always be the inverse to the directionality of the request.

Also you'll need to keep in mind that any rules that you create for the response will need to often allow the full range of ephemeral ports. That's not a problem with stateful firewalls which I want to cover next. So we're going to use the same architecture.

We've got Bob's laptop on the top-left, the catagram server on the middle-right, and the software update server on the bottom-left. A stateful firewall is intelligent enough to identify the response for a given request. Since the ports and IPS are the same, it can link one to the other.

And this means that for a specific request to catagram from Bob's laptop to the server, the firewall automatically knows which data is the response. And the same is true for software updates. For a given connection to a software update server, the request, the firewall is smart enough to be able to see the response; so the return data from the software update server back to the catagram server.

And this means that with a stateful firewall, you'll generally only have to allow the request or not, and the response will be allowed or not automatically. This significantly reduces the admin overhead and the chance for mistakes, because you just have to think in terms of the directionality and the IPs and ports of the request, and it handles everything else. In addition, you don't need to allow the full ephemeral port range because the firewall can identify which port is being used and implicitly allow it based on it being the response to a request that you allow.

Okay, so that's how stateless and stateful firewalls work. I know it's been a little bit abstract but this has been intentional because I want you to understand how they work conceptually before I go into more detail with regards to how AWS implements both of these different security firewall standards. Now at this point, I've finished with the abstract description.

So go ahead and finish this video. And when you're ready, I'll look forward to you joining me in the next.

## vpc-network-access-control-lists

Welcome back, and by now, you should understand the difference between stateless and stateful security protection. In this lesson, I want to talk about one security feature of AWS VPCs in a little bit more depth, and that's Network Access Control Lists known as NACLs. Now we do have a lot to cover, so let's jump in and get started.

A Network Access Control List can be thought of as a traditional firewall available within AWS VPCs. So let's look at a visual example, a subnet within an AWS VPC which has two EC2 instances; A and B. The first thing to understand, and this is core to how NACLs work within AWS, is that they are associated with subnets.

Every subnet has an associated network ACL, and this filters data as it crosses the boundary of that subnet. In practice this means any data coming into the subnet is affected and data leaving the subnet is affected. But, and this is super important to remember, connections between things within that subnet, such as between instance A and instance B in this example, are not affected by network ACLs.

Each network ACL contains a number of rules, two sets of rules to be precise. We have inbound rules and outbound rules. Now inbound rules only affect data entering the subnet and outbound rules affect data leaving the subnet.

Remember from the previous lesson, this isn't always matching directly to request and response. A request can be either inbound or outbound as can a response. These inbound and outbound rules are focused only on the direction of traffic, not whether it's request or response.

In fact, and they'll cover this very soon, NACLs are stateless, which means they don't know if traffic is request or response. It's all about direction. Now rules match the destination IP or IP range, destination port or port range, together with the protocol, and they can explicitly allow or explicitly deny traffic.

Remember this one, network ACLs offer both explicit allows and explicit denies. Now rules are processed in order. First, a network ACL determines if the inbound or outbound rules apply, then it starts from the lowest rule number.

It evaluates traffic against each individual rule until it finds a match. Then that traffic is either allowed or denied based on that rule and then processing stops. Now, this is critical to understand, because it means that if you have a deny rule and an allow rule which match the same traffic, but if the deny rule comes first, then the allow rule might never be processed.

Lastly, as a catch-all showed by the asterisk in the rule number, and this is an implicit deny. If nothing else matches, then traffic will be denied. So those are the basics.

Next, let's move on to some more complex elements of network ACLs. Now I just mentioned that network ACLs are stateless, and this means that rules are required for both the request and the response part of every communication. You need individual rules for those, so one inbound and one outbound.

Take this example, a multi-tiered application running in a VPC. We've got a web server in the middle and an application server on the left. On the right, we have our user Bob using a laptop and he's accessing the website.

So he makes a connection using HTTPS which is TCP 443, and this is the request, as you know by now, and this is also going to mean that a response is required using the ephemeral port range, and this ephemeral port is chosen at random from the available range decided by the operating system on Bob's laptop. Now to allow for this initial communication, if we're using network ACLs, then we'll need to have one associated with the web subnet, and it will need rules in the inbound and outbound sections of that network ACL. Notice how on the inbound rule set, we have rule number 110, which allows connections from anywhere, and this is signified by 0.0.0.0/0 through this network ACL.

And this is allowed as long as it's using TCP port 443. So this is what allows the request from Bob into the web server. We also have on the outbound rule set, rule number 120, and this allows outbound traffic to anywhere, again 0.0.0.0/0 as long as the protocol is TCP using the port range of 1024 to 65535.

And this is the ephemeral port range which I mentioned in the previous lesson. Now this is not amazingly secure, but with stateless firewalls, this is the only way. Now we also have the implicit denies, and this is denoted by the rules with the star in the rule number.

And this means that anything which doesn't match rule 110 or 120 is denied. Now it's also worth mentioning while I do have rule 110 and 120 number differently, the rule numbers are unique on inbound and outbound. So we could have the single rule number 110 on both rule sets, and that would be okay.

It's just easier to illustrate this if I use unique rule numbers for each of the different rule sets. Now let's move on and increase the complexity a little. So we have the same architecture, we have Bob on the right, the web subnet in the middle, and the application subnet on the left.

You know now that because network ACLs are stateless, each communication requires one request rule and one response rule. This becomes more complex when you have a multi-tiered architecture which operates across multiple subnets. And let's step through this to illustrate why.

Let's say that Bob initiates a connection to the web server. We know about this already because I just covered it. If we have a network ACL around the web subnet, we'll need an inbound rule on the web network ACL.

There's also going to be response traffic. So this is going to use the ephemeral port range, and this is going to need an outbound rule on that same web network ACL. So this should make sense so far.

But also the web server might need to communicate with the app server using some application TCP port. Now this is actually crossing two subnet boundaries; the web subnet boundary and the application subnet boundary. So it's going to need an outbound rule on the web subnet NACL and also an inbound rule on the application subnet NACL.

Then we have the response for that as well from the app server through to the web server, and this is going to be using ephemeral ports. But this also crosses two subnet boundaries. It leaves the application subnet which will need an outbound rule on that NACL, and it enters the web subnet which will also need an inbound rule on that network ACL.

And what if each of those servers needs software updates? It will get even more complex really quickly. You always have to be aware of these rule-pairs, the application port request and the ephemeral response for every single communication.

In some cases, you're going to have multi-tiered architecture, and this might mean that communications go through different subnets. If you need software updates, this will need more. If you use Network Address Translation or NAT, you might need more rules still.

You'll need to worry about this if you use network ACLs within a VPC for traffic to a VPC or traffic from a VPC or traffic between subnets inside that VPC. When a VPC is created, it's created with a default network ACL, and this contains inbound and outbound rule sets which have the default implicit deny, but also a catch-all allow, and this means that the net effect is that all traffic is allowed. So the default within a VPC is that NACLs have no effect.

They aren't used. This is designed to be beginner friendly and reduce admin overhead. AWS prefer using security groups which I'll be covering soon.

If you create your own custom network ACLs though, that's a different story. Custom NACLs are created for a specific VPC, and initially they're associated with no subnets. They only have one rule on both the inbound and outbound rule sets, which is the default deny.

And the result is that if you associate this custom network ACL with any subnets, all traffic will be denied. So be careful with this. It's radically different behavior than the default network ACL created with a VPC.

Now, at this point, I just want to cover some finishing key points which you need to be aware of for any real-world usage and when you're answering exam questions. So Network Access Control List, remember they're known as NACLs, they are stateless, so they view request and response as different things. So you need to add rules, both for the request and for the response.

A NACL only affects data which is crossing the subnet boundary. So communications between instances in the same subnet is not affected by a network ACL on that subnet. Now this can mean that if you do have data crossing between subnets, then you need to make sure that each NACL on both of those subnets has the appropriate inbound and outbound rules.

So you end up with a situation where one connection can in theory need two rules on each NACL if that connection is crossing two different subnet boundaries. Now NACLs are able to explicitly allow traffic and explicitly deny, and the deny is important because as you'll see when I talk about security groups, this is a capability that's unique to network ACLs. So network ACLs allow you to block specific IPs or specific IP ranges which are associated with bad actors.

So they are really good security feature when you need to block any traffic attempting to exploit your systems. Now network ACLs are not aware of any logical resources. They only allow you to use IPs and CODR ranges, ports, and protocols.

You cannot reference logical resources within AWS. And NACLs can also not be assigned to logical resources, they are only assigned to subnets within VPCs within AWS. Now NACLs are very often used together with security groups, as I've just mentioned, to add the capability to explicitly deny bad IPs or bad networks.

So generally you would use security groups to allow traffic and you'd use NACLs to deny traffic, and I'll talk about exactly how this works in the next lesson. Now each subnet within a VPC has one NACL associated with it. It's either going to be the default network ACL for that VPC or a custom one which you create and associate.

A single NACL, though, can be associated with many different subnets. So while a subnet can only have one network ACL, one network ACL can be associated with many different subnets. Now at this point, that is everything that I wanted to cover about network ACLs for this lesson.

So go ahead, complete the video, and when you're ready, I'll look forward to your joining me in the next lesson.

## vpc-security-groups

Welcome back and in this lesson I want to talk in detail about security groups within AWS. These are the second type of security filtering feature commonly used within AWS. The other type being network access control lists which we've previously discussed.

So security groups and NACLs share many broad concepts but the way they operate is very different. and it's essential that you understand those differences and the features offered by security groups for both the exam and real world usage. So let's just jump in and get started.

In the lesson on network access control lists, I explained that they're stateless and by now you know what stateless and stateful mean. Security groups are stateful. They detect response traffic automatically for a given request.

And this means that if you allow an inbound or outbound request, then the response is automatically allowed. You don't have to worry about configuring ephemeral ports. It's all handled by the product.

If you have a web server operating on TCP port 443 and you want to allow access from the public internet, then you will add an inbound security group rule, allowing inbound traffic on TCP port 443. and the response which is using ephemeral ports is automatically allowed. Now security groups do have a major limitation and that's that there is no explicit deny.

You can use them to allow traffic or you can use them to not allow traffic and this is known as an implicit deny. So if you don't explicitly allow traffic then you're implicitly denying it. but you can't, and this is important, you're unable to explicitly deny traffic using security groups and this means that they can't be used to block specific bad actors.

Imagine you allow all source IP addresses to connect to an instance on port 443 but then you discover a single bad actor is attempting to exploit your web server. Well you can't use security groups to block that one specific IP address or that one specific range. If you allow an IP or if you allow an IP range or even if you allow all IP addresses then security groups cannot be used to deny a subset of those and that's why typically you'll use network access control lists in conjunction with security groups where the NACLs are used to add explicit denies.

Now security groups operate above NACLs on the OSI 7 layer stack which means that they have more features. They support IP and CIDR based rules but they also allow referencing AWS logical resources. This includes other security groups and even itself within rules.

I'll be covering exactly how this works on the next few screens. Just know at this stage that it enables some really advanced functionality. An important thing to understand is that security groups are not attached to instances, nor are they attached to subnets.

They're actually attached to specific elastic network interfaces known as ENIs. Now, even if you see the user interface present this as being able to attach a security group to an instance, know that this isn't what happens. When you attach a security group to an instance, what it's actually doing is attaching the security group to the primary network interface of that instance.

So remember, security groups are attached to network interfaces. That's an important one to remember for the exam. Now, at this point, let's step through some of the unique features of security groups, and it's probably better to do this visually.

Let's start with a public subnet containing an EC2 instance, and this instance has an attached primary elastic network interface. On the right side we have a customer, Bob, and Bob is accessing the instance using HTTPS. So this means TCP port 443.

Conceptually think of security groups as something which surrounds network interfaces. In this case the primary interface of the EC2 instance. Now this is how a typical security group might look.

It has inbound and outbound rules just like a network ACL. and this particular example is showing the inbound rules allowing TCP port 443 to connect from any source. The security group applies to all traffic which enters or leaves the network interface and because they're stateful in this particular case because we've allowed TCP port 443 as the request portion of the communication the corresponding response part, the connection from the instance back to Bob is automatically allowed.

Now lastly, and I'm going to repeat this point several times throughout this lesson, security groups cannot explicitly block traffic. This means with this example, if you're allowing 0.0.0.0/0 to access the instance on port TCP port 443, and this means the whole IP version for internet, then you can't block anything specific. Imagine Bob is actually a bad actor.

Well in this situation security groups cannot be used to add protection. You can't add an explicit deny for Bob's IP address. That's not something that security groups are capable of.

Okay so that's the basics. Now let's look at some of the advanced bits of security group functionality. Security groups are capable of using logical references.

Let's step through how this works with a similar example to the one you just saw. We start with a VPC containing a public web subnet and a private application subnet. Inside the web subnet is the 'categram application web instance' and inside the app subnet is the 'backend application instance'.

Both of these are protected by security groups. We have A4L-web and A4L-app. Traffic wise, we have Bob accessing the web instance over port TCP, port 443.

And because this is the entry point for the application, which logically has other users than just Bob, we're allowing TCP port 443 from any IP version four address. And this means we have a security group security group with an inbound rule set which looks like this. In addition to this front end traffic the web instance also needs to connect with the application instance and for this example let's say this is using TCP port 1337 our application is that good.

So how best to allow this communication? Well we could just add the IP address of the web instance into the security group of the application instance or if you wanted to allow our application to scale and change IPs then we could add the CIDR ranges of the subnets instead of IP addresses so that's possible but it's not taking advantage of the extra functionality which security groups provide what we could do is reference the web security group within the application security group so this is an example of the application security group group. Notice that it allows TCP port 1337 inbound but it references as the source a logical resource, the security group.

Now using a logical resource reference in this way means that the source reference, so the A4L-web security group, this actually references anything which has this security group associated with it. So in this example any instances which have the A4L-web security group attached to them can connect to any instances which have the A4L-app security group attached to them using TCP port 1337. So in essence this references this so this logical reference within the application security group references the web security group and anything which has the web security group attached to it.

Now this means we don't have to worry about IP addresses or CIDR ranges and it also has another benefit it scales really well so as additional instances are added to the application subnet and web subnet and as those instances are attached to the relevant security groups they're impacted by this logical referencing allowing anything defined within the security group to apply to any new instances automatically. Now this This is critical to understand, so when you reference a security group from another security group, what you're actually doing is referencing any resources which have that security group associated with them. So this substantially reduces the admin overhead when you have multi-tiered applications.

And it also simplifies security management, which means it's prone to less errors. Now, logical references provide even more functionality. They allow self-referencing.

Let's take this as an example. A private subnet inside AWS with an ever-changing number of application instances. Right now it's three, but it might be three, thirty or one.

What we can do is create a security group like this. This one allows incoming communications on port TCP 1337 from the web security group, but it also has this rule, which is a self referential rule, allowing all traffic. What this means is that if it's attached to all of the instances, then anything with this security group attached can receive communication, so all traffic from this security group.

And this effectively means anything that also has this security group attached to it. So it allows communications to occur to instances which have it attached from instances which have it attached. It handles any IP changes automatically which is useful if these instances are within an auto scaling group which is provisioning and terminating instances based on load on the system.

It also allows for simplified management of any intra-app communications and examples of this might be Microsoft domain controllers or managing application high availability within clusters. So this is everything I wanted to cover about security groups within AWS. So there's a lot of functionality and intelligence that you gain by using security groups versus network ACLs.

But it's important that you understand that while network ACLs do allow you to explicitly deny traffic, security groups don't. and so generally you would use network ACLs to explicitly block any bad actors and use security groups to allow traffic to your VPC based resources. You do this because security groups are capable of this logical resource referencing and that means AWS logical resources, it means security groups or even itself to allow this free flow of communications within a security group.

At this At this point though that is everything I wanted to cover in this lesson so go ahead and complete the video and when you're ready I'll look forward to you joining me in the next lesson.

## vpc-network-address-translation-and-nat-gateway-1

Welcome back in this lesson, I'll be talking about network address translation or NAT. A process of giving a private resource outgoing only access to the internet. And NAT gateway is the AWS implementation that's available within a VPC.

There's quite a bit of theory to cover. So let's get started. So what is NAT?

Well, it stands for network address translation. This is one of those terms, which means more than people think that it does. In a strict sense, it's a set of different processes which can adjust IP packets by changing their source or destination IP addresses.

Now you've seen a form of this already. The internet gateway actually performs a type of NAT known as static NAT. It's how a resource can be allocated with a public IP version 4 address.

And then when the packets of data leave those resources and pass through the internet gateway, it adjusts the source IP address on the packet from the private address to the public, and then sends the packet on. And then when the packet returns it adjusts the destination address from the public IP address to the original private address that's called static NAT, and that's how the internet gateway implements public IP version 4 addressing. Now what most people think of when they think of NAT is a subset of NAT called IP masquerading.

And IP masquerading hides a whole private CIDR block behind a single public IP. So rather than the one private IP to one public IP process that the internet gateway does, NAT is many private IPs to one single IP. And this technique is popular because IP version 4 addresses are running out the public address space is rapidly becoming exhausted.

IP masquerading or what we'll refer to for the rest of this lesson as NAT gives a whole private range of IP addresses outgoing, only access to the public internet and the AWS public zone. I've highlighted outgoing because that's the most important part because many private IPs use a single public IP incoming access doesn't work. Private devices that use NAT can initiate outgoing connections to internet or AWS public space services.

And those connections can receive response data but you cannot initiate connections from the public internet to these private IP addresses when NAT is used, it doesn't work that way. Now AWS has two ways that it can provide NAT services. Historically, you could use an EC2 instances, configured to provide NAT, but there's also a managed service the NAT gateway which you can provision into VPC to provide the same functionality.

So let's look at how this works architecturally. This is a simplified version of the animals for life architecture that we've been using so far. On the left is an application test of NAT in blue.

And it's using the IP range 10.16.32.0/20. So this is a private only subnet. Inside it, a three instances, i-01 which is using the IP 10.16.32.10, i-02 which is using 32.20.

And i-03, which is using 32.30. These IP addresses are private. So they're not publicly routable.

They cannot communicate with the public internet or the AWS public zone services. These addresses cannot be routed across a public style network. Now, if we wanted this to be allowed, if we wanted these instances to perform certain activities using public networking for example, software updates, how would we do it?

Well, we could make the subnets public in the same way that we've done with the public subnets, so the web subnets. But we might not want to do that architecturally with this multi-tiered architecture that we're implementing together, part of the design logic is to have tiers, which aren't public and aren't accessible from the public internet. Now we could also host some kind of software update server inside the VPC, and some businesses choose to do that.

Some businesses run Windows, update services or Linux update services inside their private network but that comes with an admin overhead. NAT offers us a third option and it works really well in this style of situation. We provision a NAT gateway into a public subnet.

And remember the public subnet allows us to use public IP addresses the public subnet has a route table attached to it which provides default IP version 4 routes pointing at the internet gateway. So because the NAT gateway is located in this public web subnet, it has a public IP which is routable across the public internet. So it's now able to send data out and get data back in return.

Now, the private subnet where the instances are located can also have its own route table. And this route table can be different than the public subnet route table. So we could configure it so that the route table that's on the application subnet has a default IP version 4 route, but this time, instead of pointing at the internet gateway, like the web subnet users we configure this private route table so that it points at the NAT gateway.

This means when those instances are sending any data to any IP addresses that do not belong inside the VPC by default, this default route will be used and that traffic will get sent to the NAT gateway. So let's have a look at how this packet flow works. Let's simulate the flow of packets from one of the private instances and see what the NAT gateway actually does.

So first instance one, generates some data. Let's assume that it's looking for software updates. So this packet has a source IP address of instance one's private IP and a destination of 1.3.3.7.

For this example let's assume that's the software update server. Now because we have this default route on the route table of the application subnet that packet is routed through to the Nat gateway. The NAT gateway makes a record of the data packet.

It stores the destination that the packet is for, the source address at the instance sending it and all the details which help it identify the specific communication in future. Remember multiple instances can be communicating at once. And for each instance, it could be having multiple conversations with different public internet hosts.

So the NAT gateway needs to be able to uniquely identify those. And so it records the IP addresses involved, the source and destination, the port numbers, everything it needs into a translation table. So the NAT gateway maintain something called a translation table which records all of this information.

And then it adjusts the packet, the one that's been sent by the instance, and it changes the source address of this IP packet to be its own source address. Now, if this NAT appliance where anywhere but AWS, what it would do right now is it just the packet with a public routable address do this directly, but remember nothing inside a VPC really has directly attached to it, a public IP version 4 address. That's what the internet gateway does.

So the NAT gateway because it's in the web subnet, it has a default route and this default route points at the internet gateway. And so the packet is moved from the gateway to the internet gateway by the VPC router. At this point, the internet gateway knows that this packet is from the NAT gateway.

It knows that the NAT gateway has a public IP version 4 address associated with it. And so it modifies the packet to have a source address of the NAT gateways public address and it sends it on its way. The NAT gateways job is to allow multiple private IP addresses to masquerade behind the IP address that it has.

That's where the term IP masquerading comes from. That's why it's more accurate. So the NAT gateway takes all of the incoming packets from all of the instances that it's managing.

And it records all the information about the communication. It takes those packets, it changes the source address from being those instances to its own IP address, its own external facing IP address. If it was outside AWS, this will be a public address directly.

That's how your internet router works for your home network. All of the devices, internally on your network talk out using one external IP address or your home router users, NAT, but because it's an AWS it doesn't have directly attached a real public IP. The internet gateway translates from its IP address to the associated public one.

So that's how the flow works. If you need to give an instance its own public IP version 4 address then only the internet gateway is required. If you want to give private instances, outgoing access to the internet and the AWS public zone services such as S3, then you need both the NAT gateway to do this many to one translation and the internet gateway to translate from the IP of the NAT gateway to a real public IP version 4 address.

Now let's quickly run through some of the key facts for the NAT gateway product that you'll be implementing in the next demo lesson. First, and I hope this is logical for you by now. It needs to run from a public subnet because it needs to be able to be assigned a public IP version 4 IP address for itself.

So to deploy in NAT gateway, you will already need your VPC in a position where it has public subnets. And for that you need an internet gateway, subnets configured to allocate, public IP version 4 addresses and default routes for those subnets pointing at the internet gateway. Now in NAT gateway actually uses a special type of public IP version 4 address that we haven't covered yet called an elastic IP.

For now just know that these are IP version 4 addresses, which are static, they don't change. These IP addresses are allocated to your account in a region and they can be used for whatever you want until you deallocate them. And NAT gateway use these elastic IPs, the one service which utilizes elastic IPs.

And I'll be talking about elastic IPs later on in the course. Now NAT gateways are an AZ resilient Service. If you read the AWS documentation you might get the impression that they're fully resilient in a region like an internet gateway.

They're not, they're resilient in the AZ that they're in. So they can recover from hardware failure inside an AZ. But if an AZ entirely fails then the NAT gateway will also fail.

For a fully region resilient service. So to mirror the high availability provided by an internet gateway, then you need to deploy one NAT gateway in each AZ that you're using in a VPC and then have a route table for private subnets in that availability zone pointing at the NAT gateway, also in the availability zone. So for every availability zone that you use, you need one NAT gateway and one route table pointing at that NAT gateway.

Now, they aren't super expensive, but it can get costly if you have lots of availability zones which is why it's important to always think about your VPC design. Now NAT gateways are a managed service. You deploy them and AWS handle everything else.

They can scale to 45 gigabits per second in bandwidth and you can always deploy multiple NAT gateways and split your subnets across multiple provision products. So if you need more bandwidth you can just deploy more NAT gateways. For example, you could split heavy consumers across two different subnets in the same AZ have two NAT gateways in the same AZ and just route each of those subnets to a different NAT gateway.

And that would quickly allow you to double your available bandwidth. With NAT gateways, you're billed based on the number that you have. So there's a standard hourly charge for running a NAT gateway and this is obviously subject to change and it differs per region, but it's currently about 4 cents per hour and note, this is actually an hourly charge.

So partial hours are billed as full hours. And there's also a data processing charge. So that's the same amount as the hourly charge around 4 cents currently per gigabyte of processed data.

So you've got this base charge that a NAT gateway consumes while running plus a charge based on the amount of data that you process. So keep both of those things in mind for any NAT gateway related questions in the exam. Don't focus on the actual values just focus on the fact they have two charging elements.

Okay, so this is the end of part, one of this lesson. It was getting a little bit on the long side. And so I wanted to add a break.

It's an opportunity just to take a rest or grab a coffee. Part two we'll be continuing immediately from the end of part one. So go ahead, complete the video and when you're ready, join me in part two.

## vpc-network-address-translation-and-nat-gateway-2

Welcome back. This is part two of this lesson. We're gonna continue immediately from the end of part one, so let's get started.

So focusing specifically on the animals for life scenario, so what we're going to do in the upcoming demo lesson, to implement a truly resilient architecture for NAT services in a VPC. You need a NAT gateway in a public subnet inside each availability zone that the VPC uses. So just like on the diagram that you've got on screen now.

And then as a minimum, you need private route tables in each availability zone. In this example, AZ A, AZ B, and then AZ C. Each of these would need to have their own route table, which would have a default IP version four route, which points at the NAT gateway in the same availability zone.

That way, if any availability zone fails, the others could continue operating without issues. Now this is important. I've seen it in a few exam questions, where it suggests that one NAT gateway is enough, that a NAT gateway is truly regionally resilient.

This is false. A NAT gateway is highly available in the availability zone that it's in. So if hardware fails or it needs to scale to cope with load, it can do so in that AZ.

But if the whole AZ fails, there is no fail-over. You provision a NAT gateway into a specific availability zone, not the region. It's not like the internet gateway, which by default is region resilient.

For NAT gateway, you have to deploy one into each AZ that you use if you need that region resilience. Now my apologies in advance for the small text. It's far easier to have this all on screen at once.

I mentioned at the start of the lesson that NAT used to be provided by NAT instances, and these are just the NAT process running on an EC2 instance. Now I don't expect this to feature on the exam at this point. But if you ever need to use a NAT instance, by default, EC2 filters all traffic that it sends or receives.

It essentially drops any data that is on its network card when that network card is not either the source or the destination. So if an instance is running as a NAT instance, then it will be receiving some data, which the source address will be of other resources in that VPC, and the destination will be a host on the internet. So it will neither be the source nor the destination.

So by default, that traffic will be dropped. And if you need to allow an EC2 instance to function as a NAT instance, then you need to disable a feature called source and destination checks. This can be disabled via the console UI, the CLI, or the API.

The only reason I mentioned this is I have seen this question in the exam before. And if you do implement this in a real world production style scenario, you need to be aware that this feature exist. I don't want you wasting your time trying to diagnose this feature.

So if you just right click on an instance in the console, you'll be able to see an option to disable source and destination checks. And that is required if you want to use an EC2 instance as a NAT instance. Now at the highest level, architecturally, NAT instances and NAT gateways are kind of the same, they both need a public IP address, they both need to run in a public subnet, and they both need a functional internet gateway.

But at this point, it's not really preferred to use EC2 running as a NAT instance. It's much easier to use a NAT gateway, and it's recommended by AWS in most situations. But there are a few key scenarios where you might want to consider using an EC2 based NAT instance.

So let's just step through some of the criteria that you might be looking at when deploying NAT services. If you value availability, bandwidth, low levels of maintenance, and high performance, then you should choose NAT gateways. That goes for both real world production usage, as well as being default for answering any exam questions.

A NAT gateway offers high end performance, it scales, it's custom designed to perform network address translation. A NAT instance in comparison is limited by the capabilities of the instance it's running on. A NAT instance is also general purpose, so it won't offer the same level of custom designed performance as a NAT gateway.

Now availability is another important consideration. A NAT instance is a single EC2 instance running inside an availability zone. It will fail if the EC2 hardware fails.

It will fail if its storage fails or if its networking fails, and it will fail if the AZ itself fails entirely. A NAT gateway has some benefits over a NAT instance. So inside one availability zone, it's highly available, so it can automatically recover.

It can automatically scale. So it removes almost all of the risks of outage, versus a NAT instance, but it will still fail entirely if the AZ fails entirely. You still need to provision multiple NAT gateways spread across all the AZs that you intend to use if you want to ensure complete availability.

For maximum availability, a NAT gateway in every AZ you use. This is critical to remember for the exam. Now if cost is your primary choice, if you're a financially challenged business, or if the VPC that you're deploying NAT services into is just a test VPC or something that's incredibly low volume, then a NAT instance can be cheaper.

It can also be significantly cheaper at high volumes of data. You've got a couple of options. You can use a very small EC2 instance, even ones that are free tier eligible to reduce costs.

And the instances can also be fixed in size, meaning they offer predictable costs. A NAT gateway will scale automatically, and you're billed for both the NAT gateway and the amount of data transferred, which increases as the gateway scales. A NAT gateway is also not free tier eligible.

Now this is really important, because when we deploy these in the next demo lesson, it's one of those services that I need to warn you will come at a cost. So you need to be aware of that fact. You will be charged for NAT gateway, regardless of how small the usage.

NAT instances also offer other niche advantages. Because they're just EC2 instances, you can connect to them just like you would any other EC2 instance. You can multipurpose them, so you can use them for other things, such as bastion hosts.

You can also use them for port-forwarding. So you can have a port on the instance externally that can be connected to over the public internet, and have this forwarded onto an instance inside the VPC, maybe port 80 for web or port 443 for secure web. You can be completely flexible when you use NAT instances.

With a NAT gateway, this isn't possible because you don't have access to manage it. It's a managed service. Now this comes up all the time in the exam.

So try and get it really clear in your memory. A NAT gateway cannot be used as a bastion host. It cannot do port-forwarding, because you cannot connect to its operating system.

Now finally, and this is again, one focused on the exam. NAT instances are just EC2 instances. And so you can filter traffic using either network ACLs on the subnet the instance is in, or security groups directly associated with that instance.

NAT gateways don't support security groups. You can only use NACLs with NAT gateways. This one comes up all the time in the exam.

So it's worth noting down and maybe making a flashcard with. Now a few more things before we finish up. What about IP version six?

Well, NAT is not required for IP version six. The main focus of NAT is to allow private IP version four addresses to be used to connect in an outgoing only way to the AWS public zone and public internet. Inside AWS, all IP version six addresses are publicly routable.

So this means that you do not require NAT when using IP version six. The internet gateway works directly with IP version six addresses. So if you choose to make an instance in a private subnet, have a default IP version six route to the internet gateway, it will become a public instance.

As long as you don't have any NACLs or any security groups, any IP version six IP address in AWS can communicate directly with the AWS public zone and the public internet. So the internet gateway can work directly with IP version six. NAT gateways do not work with IP version six.

They're not required, and they don't function with IP version six. So for the exam, if you see any questions, which mention IP version six and NAT gateways, you can exclude the answer. NAT gateways do not work with IP version six.

I need to repeat it because I really want it to stick in your memory. So with any subnet inside AWS, which has been configured for IP version six, if you add the IP version six default route, which is ::/0, if you add that route and you point that route at the internet gateway as a target, that will give that instance bi-directional connectivity to the public internet, and it will allow it to reach the AWS public zone and public services. One service that we'll be talking about later on in the course when I cover more advanced features of VPC is a different type of gateway known as an Egress-Only Internet Gateway.

This is a specific type of internet gateway that works only with IP version six, and you use it when you want to give an IP version six instance outgoing only access to the public internet and the AWS public zone. So don't worry, we'll be covering that later in the course. But I want to get it really burned into your memory, that you do not use NAT, and you do not use NAT gateways with IP version six.

It will not work. Now to get you some experience of using NAT gateways, it's time for a demo. In the demo lesson, I'm gonna be stepping you through what you need to do to provision a completely resilient NAT gateway architecture.

So that's using a NAT gateway in each availability zone, as well as configuring the routing required to make it work. It's going to be one of the final pieces to our multi-tier VPC, and it will allow private instances to have full outgoing internet access. Now I can't wait for us to complete this together.

It's gonna be a really interesting demo, one that would be really useful if you're doing this in the real world, or if you have to answer exam questions related to NAT or NAT gateway. So go ahead, complete the video. And when you're ready, join me in the demo.

## vpc-implementing-private-internet-access-using-nat-gateways

Welcome back, and in this demo lesson, you're going to evolve the infrastructure which you've been using throughout this section of the course. In this demo lesson, you're going to add private internet access capability using NAT gateways. So you're going to be applying a CloudFormation template which creates this base infrastructure.

It's going to be the Animals for Life VPC with infrastructure in each of three availability zones. So there's a database subnet, an application subnet, and a web subnet in availability zone A, B, and C. Now to this point, what you've done is configured public subnet internet access and you've done that using an internet gateway together with routes on these public subnets.

In this demo lesson, you're going to add NAT gateways into each availability zone, so A, B, and C and this will allow this private EC2 instance to have access to the internet. Now you're going to be deploying NAT gateways into each availability zone so that each availability zone has its own isolated, private subnet access to the internet. It means that if any of the availability zones fail, then each of the others will continue operating because these route tables which are attached to the private subnets, they point at the NAT gateway within that availability zone.

So each availability zone A, B, and C, has its own corresponding NAT gateway which provides private internet access to all of the private subnets within that availability zone. Now, in order to implement this infrastructure, you're going to be applying a one click deployment and that's going to create everything that you see on screen now apart from these NAT gateways and the Route Table configurations. So let's go ahead and move across to our AWS Console and get started implementing this architecture.

Okay, so now we're at the AWS Console. As always, just make sure that you're logged in to the General AWS account as the iamadmin user, and you'll need to have the Northern Virginia region selected. Now, at the end of the previous demo lesson, you should have deleted all of the infrastructure that you've created up until that point.

So the Animals for Life VPC as well as the Bastion host and the associated networking. So you should have a relatively clean AWS account. So what we're going to do first is use a one-click deployment to create the infrastructure that we'll need within this demo lesson.

So attached to this demo lesson is a one-click deployment link. So go ahead and open that link. That's going to take you to a quick create stack screen.

Everything should be pre-populated. The stack name should be A4L. Just scroll down to the bottom, check this capabilities box, and then click on Create Stack.

Now this will start the creation process of this A4L Stack and we will need this to be in a create complete state before we continue. So go ahead, pause the video, wait for your stack to change and to create complete and then we are good to continue. Okay, so now this stack's moved into a create complete state, then we are good to continue.

So what we need to do before we start is make sure that all of our infrastructure has finished provisioning. To do that, just go ahead and click on the resources tab of this CloudFormation Stack and look for A4L internal test. This is an EC2 instance, a private EC2 instance.

So this doesn't have any public internet connectivity and we're going to use this to test on NAT gateway functionality. So go ahead and click on this icon under physical id and this is going to move you to the EC2 console and you'll be able to see this A4L hyphen internal hyphen test instance. Now, currently in my case, it's showing as running but the status check is showing as initializing.

Now we'll need this instance to finish provisioning before we can continue with the demo. What should happen is this status check should change from initializing to two out of two status checks and once you're at that point, you should be able to right click and select connect and choose Session Manager and then have the option of connecting. Now you'll see that I don't because this instance hasn't finished its provisioning process.

So what I want you to do is to go ahead and pause this video, wait for your status checks to change to two out of two checks, and then just go ahead and try to connect to this instance using Session Manager. Only resume the video once you've been able to click on connect under the Session Manager tab and don't worry if this takes a few more minutes after the instance finishes provisioning before you can connect to Session Manager. So go ahead and pause the video and when you can connect to the instance, you're good to continue.

Okay, so in my case, it took about five minutes for this to change to two out of two checks passed and then another five minutes before I could connect to this EC2 instance. So I can right click on here and put connect. I'll have the option now of picking Session Manager and then I can click on connect and this will connect me into this private EC2 instance.

Now, the reason why you're able to connect to this private instance is because we're using Session Manager and I'll explain exactly how this product works elsewhere in the course, but essentially it allows us to connect into an EC2 instance with no public internet connectivity and it's using VPC interface endpoints to do that which I'll be explaining elsewhere in the course. But what you should find when you are connected to this instance, if you try to ping any internet IP address, so let's go ahead and type ping and then a space 1.1.1.1 and press enter. You'll note that we don't have any public internet connectivity and that's because this instance doesn't have a public IP version four address and it's not in a subnet with a route table which points at the internet gateway.

This EC2 instance has been deployed into the application A subnet, which is a private subnet and it also doesn't have a public IP version four address. So at this point, what we need to do is go ahead and deploy on NAT gateways and these NAT gateways are what will provide this private EC2 instance with connectivity to the public IP version four internet. So let's go ahead and do that.

Now to do that, we need to be back at the main AWS Console, click in the services search box at the top, type VPC, and then right click and open that in a new tab. Once you've done that, go ahead and move to that tab. Once you're there, click on NAT gateways and create a NAT gateway.

Okay, so once you're here, you'll need to specify a few things. You'll need to give the NAT gateway a name. You'll need to pick a public subnet for the NAT gateway to go into and then you'll need to give the NAT gateway an elastic IP address, which is an IP address which doesn't change.

So first we'll set the name of the NAT gateway and we'll choose to use A4L for Animals for Life hyphen VPC1, hyphen NAT GW, and then hyphen uppercase A. Because this is going into Availability Zone A. Next we'll need to pick the public subnet that the NAT gateway will be going into.

So click on the subnet dropdown and then select the web A subnet, which is the public subnet in availability zone A. So SN hyphen web hyphen A. Now we need to give this NAT gateway an elastic IP.

It doesn't currently have one, so we need to click on allocate elastic IP, which gives it an allocation. Don't worry about the connectivity type. We'll be covering that elsewhere in the course.

Just scroll down to the bottom and create the NAT gateway. Now this process will take some time and so we need to go ahead and create the two other NAT gateways. So click on NAT gateways at the top and then we're going to create a second NAT gateway.

So go ahead and click on create NAT gateway again. This time we'll call the NAT gateway A4L hyphen VPC1, hyphen NAT GW hyphen B and this time we'll pick the web B subnet. So SN hyphen web hyphen B, allocate it an elastic IP again and click on create NAT gateway.

Then we'll follow the same process a third time. So click create NAT gateway, use the same naming scheme but with hyphen C, pick the web C subnet from the list, allocate an elastic IP, and then scroll down and click on create NAT gateway. And at this point we've got the three NAT gateways that are being created, they're all in a pending state.

If we go to elastic IPs, we can see the three elastic IPs which have been allocated to the NAT gateways and we can scroll to the right or left and see details on these IPs. And if we wanted, we could release these IPs back to the account once we'd finished with them. Now at this point, you need to go ahead and pause the video and resume it once all three of those NAT gateways have moved away from a pending state, we need them to be in an available state ready to go before we can continue with this demo.

So go ahead and pause and resume once all three have changed to an available state. Okay, so all these are now in an available state so that means they're good to go, they're providing service. Now, if you scroll to the right in this list, you're able to see additional information about these NAT gateways.

So you can see the elastic and private IP address, the VPC, and then the subnet that each of these NAT gateways are located in. What we need to do now is configure the routing so that the private instances can communicate via the NAT gateways. So right click on route tables and open in a new tab.

And we need to create a new Route Table for each of the availability zones. So go ahead and click on create Route Table. First we need to pick the VPC for this Route Table.

So click on the VPC dropdown and then select the Animals for Life VPC, so A4L hyphen VPC one. Once selected, go ahead and name the Route Table. We're going to keep the naming scheme consistent.

So A4L hyphen VPC1, hyphen RT for Route Table, hyphen Private A. So enter that and click on create. Then close that dialogue down and create another Route Table.

This time we'll use the same naming scheme, but of course this time it will be RT hyphen Private B, select the Animals for Life VPC, and click on create. Close that down. And then finally click on create Route Table again, this time A4L hyphen VPC1, hyphen RT hyphen Private C.

Again, click on the VPC dropdown and select the Animals for Life VPC, and then click on create. So that's going to leave us with three route tables, one for each availability zone. What we need to do now is create a default route within each of these route tables.

And that route is going to point at the NAT gateway in the same availability zone. So select the Route Table Private A and then click on the routes tab. Once you've selected the routes tab, click on edit routes, and we're going to add a new route.

It's going to be the IP version four, default route of 0.0.0.0 slash zero and then click on target and pick NAT gateway. And we're going to pick the NAT gateway in availability zone A. And because we named them, it makes it easy to select the relevant one from this list.

So go ahead and pick A4L hyphen VPC1, hyphen NAT GW hyphen A. So because this is the Route Table in availability zone A, we need to pick the same NAT gateway. So save that and close.

And now we'll be doing the same process for the Route Table in availability zone B, make sure the route tab is selected and click on edit routes. Click on add route again, 0.0.0.0 slash zero. And then for target, pick NAT gateway, and then pick the NAT gateway that's in availability zone B, so NAT GW hyphen B.

Once you've done that, save the route table. And then next, select the route table in availability zone C. So select RT hyphen Private C.

Make sure the routes tab is selected and click on edit routes. Again, we'll be adding a route. It will be the IP version four, default route.

So 0.0.0.0 slash zero. Select a target, go to NAT gateway, and pick the NAT gateway in availability zone C. So NAT GW hyphen C.

Once you've done that, save the route table. And now our private EC2 instance should be able to ping 1.1.1.1 because we have the routing infrastructure in place. So let's move back to our private instance and we can see that it's not actually working.

Now the reason for this is that although we have created these routes, we haven't actually associated these route tables with any of the subnets. Subnets in a VPC, which don't have an explicit route table association, are associated with the main route table. Now we need to explicitly associate each of these route tables with the subnets inside that same AZ.

So let's go ahead and pick RT hyphen Private A. We'll go through in order. So select it, click on the subnet associations tab, and edit subnet associations.

And then you need to pick all of the private subnets in AZ A. So that's the reserved subnet. So reserved hyphen A, the app subnet, so app hyphen A, and the DB subnet, so DB hyphen A.

So all of these are the private subnets in availability zone A. Notice how all the public subnets are associated with this custom route table you created earlier but the ones we're setting up now are still associated with the main route table. So we're going to resolve that now by associating this route table with those subnets.

So click on save and this will associate all of the private subnets in AZ A with the AZ A Route Table. So now we're going to do the same process for AZ B and AZ C and we'll start with AZ B. So select the Private B Route Table, click on subnet associations, edit subnet associations.

So select application B, database B, and then reserved B. And then scroll down and save the associations and then select the Private C Route Table. Click on subnet associations, edit subnet associations, and then select reserved C, database C, and then application C, and then scroll down and save those associations.

And now that we've associated these route tables with the subnets and now that we've added those default routes, if we go back to Session Manager where we still have the connection open to the private EC2 instance, we should see that the ping has started to work. And that's because we now have a NAT gateway providing service to each of the private subnets in all of the three availability zones. Okay, so that's everything you needed to cover in this demo lesson.

Now it's time to clean up the account and return it to the same state as it was at the start of this demo lesson. From this point on within the course, you're going to be using automation and so we can remove all of the configuration that we've done inside this demo lesson. So the first thing we need to do is to reverse the route table changes that we've done.

So we need to go ahead and select the RT hyphen Private A Route Table. Go ahead and select subnet associations and then edit the subnet associations. And then just uncheck all of these subnets and this will return these to being associated with the main route table.

So scroll down and click on save. Do the same for RT hyphen Private B. So deselect all of these associations and click on save.

And then the same for RT hyphen Private C. So select it, go to subnet associations, and then edit them and remove all of these subnets and click on save. Next, select all of these private route tables.

These are the ones that we created in this lesson. So select them all, click on the actions drop down, and then delete route table and confirm by clicking delete route tables. Go to NAT gateways on the left and we need to select each of the NAT gateways in turn.

So A, and then click on actions and delete NAT gateway, type delete, click delete. Then select B and do the same process, actions, delete NAT gateway, type delete, click delete. And finally the same for C.

So select the C NAT gateway, click on actions, and delete NAT gateway. You'll need to type delete to confirm, click on delete. Now we're going to need all of these to be in a fully deleted state before we can continue.

So hit refresh and make sure that all three NAT gateways are deleted. If yours aren't deleted, if they're still listed in a deleting state, then go ahead and pause the video and resume once all of these have changed to deleted. At this point, all of the NAT gateways have deleted.

So you can go ahead and click on elastic IPs and we need to release each of these IPs, so select one of them and then click on actions and release elastic IP addresses and click release and do the same process for the other two. Click on release. Then finally, actions, release IP, click on release.

Once that's done, move back to the CloudFormation console, select the stack which was created by the one click deployment at the start of the lesson and click on delete and then confirm that deletion and that will remove the CloudFormation stack and any resources created as part of this demo. And at that point, once that finishes deleting, the account has been returned into the same state as it was at the start of this demo lesson. So I hope this demo lesson has been useful.

Just to reiterate what you've done, you've created three NAT gateways for a region resilient design. You've created three route tables, one in each availability zone, added a Default IP version four route pointing at the corresponding NAT gateway and associated each of those route tables with the private subnets in those availability zones. So you've implemented a regionally resilient NAT gateway architecture.

So that's a great job. That's a pretty complex demo but it's gonna be functionality that will be really useful if you are using AWS in the real world or if you have to answer any exam questions on NAT gateways. With that being said, at this point, you have cleared up the account, you've deleted all the resources.

So go ahead, complete this video, and when you're ready, I'll see you in the next.

