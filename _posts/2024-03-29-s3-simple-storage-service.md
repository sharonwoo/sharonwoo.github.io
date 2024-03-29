---
title: "AWS SAA-C03 part 3: IAM"
categories:
  - exams
tags:
  - aws-saa-c03
---

*STILL* having that cold. Since December I've spent about half the time unable to breathe freely. This........ sucks. (Pun fully intended.)

## s3-security-resource-policies-and-acls

Welcome back, and in this lesson, I want to start talking about S3 security in more detail, starting with bucket policies which are a type of AWS resource policy. So by now, you know the drill, let's jump in and get started. Now, before we start, I want to repeat one thing and you will have heard me say this before, but I'm going to say it again over and over.

S3 is private by default. Everything that we can do to control S3 permissions is based on this starting point. The only identity which has any initial access to an S3 bucket is the account root user of the account which owns that bucket, so the account which created it.

Anything else, so any other permissions, have to be explicitly granted. And there are a few ways that this can be done. The first way is using an S3 bucket policy.

And an S3 bucket policy is a type of resource policy. A resource policy is just like an identity policy, but as the name suggests, they're attached to resources instead of identities. In this case, an S3 bucket.

Resource policies provide a resource perspective on permissions. The difference between resource policies and identity policies is all about this perspective. With identity policies, you're controlling what that identity can access.

With resource policies, you're controlling who can access that resource. So it's from an inverse perspective. One is identities and one is resources.

Now, identity policies have one pretty significant limitation. You can only attach identity policies to identities in your own account. And so identity policies can only control security inside your account.

With identity policies, you have no way of giving an identity in another account access to an S3 bucket. That would require an action inside that other account. Resource policies allow this.

They can allow access from the same account or different accounts because the policy is attached to the resource and it can reference any other identities inside that policy. So by attaching the policy to the resource and then having flexibility to be able to reference any other identity whether they're in the same account or different accounts, resource policies therefore are a great way of controlling access for a particular resource no matter what the source of that access is. Now, think about that for a minute because that's a major benefit of resource policies.

The ability to grant other accounts access to resources inside your account. They also have another benefit. Resource policies can allow or deny anonymous principals.

Identity policies by design have to be attached to a valid identity in AWS. You can't have one attached to nothing. Resource policies can be used to open a bucket to the world by referencing all principals even those not authenticated by AWS.

So that's anonymous principals. So bucket policies can be used to grant anonymous access. So two of the very common uses for bucket policies are to grant access to other AWS accounts and anonymous access to a bucket.

Let's take a look at a simple visual example of a bucket policy, because I think it will help you understand how everything fits together. There's a demo lesson coming up soon where you'll implement one as part of the mini project. So you will get some experience soon enough of how to use bucket policies.

Let's say that we have an AWS account, and inside this account is a bucket called secretcatproject. Now, I can't say what's inside this bucket because it's a secret, but I'm sure that you can guess. Now, attached to this bucket is a bucket policy.

Resource policies have one major difference to identity policies, and that's the presence of an explicit principal component. The principal part of a resource policy defines which principals are affected by the policy. So the policy is attached to a bucket in this case, but we need a way to say who is impacted by the configuration of that policy.

Because a bucket policy can contain multiple statements, there might be one statement which affects your account and one which affects another account as well as one which affects a specific user. The principal part of a policy, or more specifically, the principal part of a statement in a policy, defines who that statement applies to, which identities, which principals. Now, in an identity policy, this generally isn't there because it's implied that the identity which the policy is applied to is the principal.

That's logical, right? Your identity policy by definition applies to you, so you are the principal. So a good way of identifying if a policy is a resource policy or an identity policy is the presence of this principal component.

If it's there, it's probably a resource policy. In this case, the principal is a wild card, a star, which means any principal. So this policy applies to anyone accessing the S3 bucket.

So let's interpret this policy. Well, first the effect is allow and the principal is star, so any principal. So this effect allows any principal to perform the action S3 GetObject on any object inside the secretcatproject S3 bucket.

So in effect, it allows anyone to read any objects inside this bucket. So this would equally apply to identities in the same AWS account as the bucket, it could also apply to other AWS account, so a partner account, and crucially, it also applies to anonymous principals, so principals who haven't authenticated to AWS. Bucket policies should be your default thought when it comes to granting anonymous access to objects in buckets, and they're one way of granting external accounts that same access.

They can also be used to set the default permissions on a bucket. If you want to grant everyone access to Boris's picture for example, and then grant certain identities extra rights or even deny certain rights, then you can do that. Bucket policies are really flexible, they can do many other things.

So let's quickly just look at a couple of common examples. Bucket policies can be used to control who can access objects, even allowing conditions which block specific IP addresses. In this example, this bucket policy denies access to any objects in the secretcatproject bucket unless your IP address is 1.3.3.7.

The condition block here means this statement only applies if this condition is true. So if your IP address, the source IP address is not 1.3.3.7, then the statement applies and access is denied. If you're IP address is 1.3.3.7, then this condition is not met because it's a not IP address condition.

So if your IP address is this IP address, the condition is not matched and you get any other access that's applicable. Essentially, this statement which is a deny does not apply. Now, bucket policies can be much more complex.

In this example, one specific prefix in the bucket, remember, this is what a folder really is inside a bucket, so one specific prefix called Boris is protected with MFA. It means that accesses to the Boris folder and the bucket are denied if the identity that you're using does not use MFA. The second statement allows read access to objects in the whole bucket.

Because an explicit deny overrides an allow, the top statement applies to just do that specific prefix in the bucket, so just Boris. Now, I won't labor on about bucket policies because we'll be using them a fair bit throughout the course, but they can range from simple to complex. I will include a link in the lesson description with some additional examples that you can take a look through if you're interested.

In summary, though, a resource policy is associated with a resource. A bucket policy, which is a type of resource policy, is logically associated with a bucket which is a type of resource. Now, there can only be one bucket policy on a bucket, but it can have multiple statements.

If an identity inside one AWS account is accessing a bucket also in that same account, then the effective access is a combination of all of the applicable identity policies plus the resource policy, so the bucket policy. For any anonymous access, so access by an anonymous principal, then only the bucket policy applies because logically, if it's an anonymous principal, it's not authenticated, and so no identity policies apply. Now, if an identity in an external AWS account attempts to access a bucket in your account, your bucket policy applies, as well as anything that's in their identity policies.

So there's a two step process if you're doing cross account access. The identity in their account needs to be able to access S3 in general and your bucket, and then your bucket policy needs to allow access from that identity, so from that external account. Now, there is another form of S3 security.

It's used less often these days, but I wanted to cover it anyway. Access Control Lists or ACLs are ways to apply security to objects or buckets. They're a sub-resource of that object or of that bucket.

Remember in the S3 introduction lesson earlier in the course, I talked about sub-resources, well, this is one of those sub-resources. Now, I almost didn't want to talk about ACLs because they are legacy. AWS don't even recommend their use and prefer that you use bucket policies or identity policies.

But as a bare minimum, I want you to be aware of their existence. Now, part of the reason that they aren't used all that often and that bucket policies have replaced much of what they do is that they're actually inflexible and only allow very simple permissions. They can't have conditions like bucket policies, and so you're restricted to some very broad conditions.

Let me show you what I mean. This is an example of what permissions can be controlled using an ACL. Now, apologies for the wall of text, but I think it's useful to visualize it all at once.

There are five permissions which can be granted in an ACL: READ, WRITE, READ_ACP, WRITE_ACP and FULL_CONTROL. That's it. So it's already significantly less flexible than an identity or a resource policy.

What these five things do depend on if they're applied to a bucket or an object. READ permissions for example on a bucket allow you to list all objects in that bucket, whereas WRITE permissions on a bucket allow the grantee, which is the principal being granted those permissions, the ability to overwrite and delete any object in that bucket. READ permissions on an object allow the grantee just to read the object specifically as well as its metadata.

Now, with ACLs, you either configure an ACL on the bucket, or you configure the ACL on an object, but you don't have the flexibility of being able to have a single ACL that affects a group of objects. You can't do that, that's one of the reasons that a bucket policy is significantly more flexible. It is honestly so much less flexible than a bucket policy to the extent where I won't waste your time with it anymore.

It's legacy, and I suspect at some point it won't be used anymore. If there are any specific places in the course which do require knowledge of ACLs, I'll mention it. Otherwise, it's best to almost ignore the fact that they exist.

Now, before we finish up, one final feature of S3 permissions, and that's the Block Public Access settings. In the overall lifetime of the S3 product, this was actually added fairly recently. And it was added in response to lots of public PR disasters where buckets were being configured incorrectly and being set so that they were open to the world.

This resulted in a lot of data leaks. And the root cause was a mixture of genuine mistakes or administrators who didn't fully understand the S3 permissions model. So consider this example.

An S3 bucket with resource permissions granting public access. Until Block Public Access was introduced, if you had public access configured, the public could logically access a bucket. Public access in this sense is read only to any objects defined in a resource policy on a bucket.

So there's no restrictions. Public access is public access. Block Public Access added a further level of security, another boundary.

And on this boundary is the Block Public Access settings which apply no matter what the bucket policies say. But they apply to just the public access, so not any other defined AWS identities. So these settings will only apply to an anonymous principal, somebody who isn't an AWS identity attempt to access a bucket using these public access configurations.

Now, these settings can be set when you create the bucket and adjusted afterwards. They're pretty simple to understand. You can choose the top option which blocks any public access to the bucket no matter what the resource policy says.

It's a full override, a fail safe. Or you can choose the second option, which allows any public access granted by any existing ACLs when you enable the setting, but it blocks any new ones. The third option blocks any public access granted by ACLs no matter if it was enabled before or after the Block Public Access settings were enabled.

The fourth setting allows any existing public access granted by bucket policies or access point policies. So anything enabled at the time when you enable this specific Block Public Access setting, they're allowed to continue, but it blocks any new ones. The fifth option blocks both existing and new bucket policies from granting any public access.

Now, they're simple enough and they function as a final fail safe. If you're ever in a situation where you've granted some public access and it doesn't work, these are probably the settings which are causing that inconsistency. And don't worry, I'll show you where these are accessed in the demo lesson.

Now, before we finish up, just one final thing I want to cover, and this is an exam powerup. So these are just some key points on how to remember all of the theory that I've discussed in this lesson. When I first started in AWS, I found it hard to know from instinct when to use identity policies versus resource policies versus ACLs.

Choosing between resource policies and identity policies much of the time is a preference thing. So do you want to control permissions from the perspective of a bucket, or do you want to grant or deny access from the perspective of the identities accessing a bucket? Are you looking to configure one user accessing 10 different buckets, or 100 users accessing the same bucket?

It's often a personal choice, a choice on what makes sense for your situation and business. So there's often no right answer. But there are some situations where one makes sense over the other.

If you're granting or denying permissions on lots of different resources across an AWS account, then you need to use identity policies because not every service supports resource policies. And beside, you would need a resource policy for each service. So that doesn't make sense if you're controlling lots of different resources.

If you have a preference for managing permissions all in one place, that single place needs to be IAM, so identity policies would make sense. IAM is the only single place in AWS you can control permissions for everything. You can sometimes use resource policies, but you can use IAM policies all of the time.

If you're only working with permissions within the same account, so no external access, then identity policies within IAM are fine because with IAM, you can only manage permissions for identities that you control in your account. So there are a wide range of situations where IAM make sense and that's why most permissions control is done within IAM. But there are some situations which are different.

You can use bucket policies or resource policies in general if you're managing permissions on a specific product. So in this case, S3. If you want to grant a single permission to everybody accessing one resource or everybody in one account, then it's much more efficient to use resource policies to control that base level permission.

If you want to directly allow anonymous identities or external identities from other AWS accounts to access a resource, then you should use resource policies. Now, finally, and I know this might seem like I'm anti-Access Control List, which is true, but so are AWS, never use ACLs unless you really need to. And even then, consider if you can use something else.

At this point in time, if you are using an ACL, you have to be pretty certain that you can't use anything else, because they're legacy and they're inflexible and AWS are actively recommending against their use. So keep that in mind. Okay, well, that's all of the theory that I wanted to cover in this lesson.

I know it's been a lot, but we do have to cover this detailed level of security because it's needed in the exam and you'll be using it constantly throughout the rest of this section and the wider course. At this point, though, go ahead and complete this video. And when you're ready, you can join me in the next, where I'm going to be talking about another exciting feature of S3.

## s3-static-hosting

Welcome back! In this lesson I want to talk about a feature of S3 which I use all the time, both personally and when I'm doing consulting work for clients. And that is S3 static website hosting.

Until this point we've been accessing S3 via the normal method which is using the AWS APIs. You might not have realised that, but that's how the AWS CLI tools and the console UI work behind the scenes. For instance, to access any objects within S3, we're using the S3 APIs, and assuming we're authenticated and authorized, we use the GetObject API call to access those resources.

Now accessing S3 using APIs, that's useful in certain situations because it's secure and flexible. But using static website hosting can make S3 infinitely more useful, because it allows access via standard HTTP by individuals using a web browser. So you can use it to host almost anything.

For example, a simple blog. Using static website hosting is pretty simple. You enable it, and in doing so you have to set an index document and an error document.

When you're using a website, if you access a particular page, say for example catsareamazing.html, then you will get access specifically to that page. If you don't specify a page, for example Netflix.com, you get what's called an index page, which is a default page returned to you when you aren't asking for anything specific. This is the entry point to most websites.

So when enabling static website hosting on an S3 bucket, we have to point the index document at a specific object in the S3 bucket. The error document is the same, but it's used when something goes wrong. So if you access a file which isn't there, or there is another type of server-side error, that's when the error document is shown.

Now both of these need to be HTML documents because the static website hosting feature delivers HTML files. When you enable this feature on a bucket, AWS creates a static website hosting endpoint. And this is a specific address that the bucket can be accessed from using HTTP.

Now the exact name of this endpoint is influenced by the bucket name that you choose and the region that the bucket is in. You don't get to select this name, it's automatically generated by those two things. Now you can use your own custom domain for a bucket, but if you do want to do that, then your bucket name matters.

You can only use a custom domain with a bucket if the name of the bucket matches the domain. So if I wanted to have a website called top10.animalsforlife.org, then my bucket name would need to be called top10.animalsforlife.org. And that's why I mentioned at the start of the course to get into the habit of reserving your website names by creating S3 buckets using those names.

So static website hosting is great for things like hosting static websites such as blogs. But it's also good for other things. Let's take a look at two common examples.

There are two specific scenarios which are perfect for S3. Offloading and out of band pages. With offloading, let's say you have a website which has a top 10 leaderboard of all of the best animals and it runs on a compute service.

Let's assume this is EC2 for now. The compute service does a few things. It delivers a dynamic HTML page and it delivers static media, in this example, images.

That dynamic HTML page might need access to a database, so that's not suitable for static S3 hosting. But the static media? That's sitting there waiting to be delivered.

And in most cases it probably makes up over 95% of the data volume that the compute service is delivering, and likely almost all of the storage space. Compute services tend to be relatively expensive, so we can offload a lot of this to S3. What we can do is we can take all of the images, so all of the media that the compute service hosts, and we can move that media to an S3 bucket that uses static website hosting, so one which has static website hosting enabled.

Then, when the compute service generates the HTML file and delivers this to the customer's browser this HTML file points at the media that's hosted on the S3 bucket so the media is retrieved from S3, not the compute service. S3 is likely to be much cheaper for the storage and delivery of any media versus a compute service. S3 is custom designed for the storage of large data at scale.

And so generally, whenever you've got an architecture such as this, you should always consider offloading any large data to S3. Now the other benefit that I wanted to specifically highlight is out-of-band pages. Now out-of-band is an old telecommunications term.

In an IT context, it generally means a method of accessing something that is outside of the main way. So for example, you might use out-of-band server management, and this lets you connect to a management card that's in a server, using the cellular network. That way, if the server is having networking issues with the normal access method, so the normal network, then you can still access it.

In the context of this example, so top10.animalsforlife.org, it might refer to an error or a status notification system. For example, with this example, the Favourite Animals page for Animals for Life, if that service was hosted on a compute service such as EC2, and we wanted a maintenance page to show during scheduled or unscheduled maintenance periods, it wouldn't make much sense to have this on the same server, because if the server is being worked on, then it's inherently offline. Additionally, putting it on a different EC2 instance is also risky, because if EC2 itself has issues, it might not let us show the status page.

So what we do is we use out-of-band pages, in this context another service. So if the server was offline for maintenance or it was experiencing stability or performance bugs, then we could change our DNS and point customers at a backup static website hosted on S3 and this could provide a status message or maybe the details for our businesses support team. Now the pricing structure for S3, once you understand it, is very simple but it's formed of a number of major components.

First we've got the cost to store data on S3 and this is generally expressed as a per gigabyte month fee. So to store a gigabyte of data on S3 for one month there's a certain cost and if you store data for less than one month then you only pay that component and if you store less than one gig you only pay that component so it's a per gig month charge. Now there's also a data transfer fee so for every gigabyte of data that you transfer in and out of S3 there's a cost.

Now to transfer data in to S3 is always free so you never charge for transferring data into S3. To transfer data out of S3 there is a per gigabyte charge Now for storage and data transfer, they are both incredibly cheap. It's some of the cheapest storage that's available, especially if you're storing large amounts of data.

But there is also a third component that you do need to be aware of, and this is especially important when you're using static website hosting. And this is that you're charged a certain amount for requesting data. So every time you perform an operation, every time you get, every time you list, every time you put, That's classed as an operation and different operations in S3 have different costs per 1000 operations.

Now the reason I mention this is if you're using static website hosting, you're generally not going to store a lot of data. You're also generally not going to transfer a lot of data because what's stored in the S3 bucket is likely to be very small. But if you have a large customer base and if this out of band website or this offloading bucket is actually being used heavily by a system then you could be using a lot of requests and so you need to be aware of the request charge for S3.

Now in terms of what's provided in the free tier you're given 5 gig of monthly storage inside S3, you're allowed 20,000 get requests and 2,000 put requests. So that will cover us for the demo lesson that we're going to do inside this course and probably most of the other activities that we'll do throughout the course. But if you're going to use S3 for any real-world usage then you will be billed for that usage.

Now I run a personal blog, Cantrol.io, and that runs from S3 using the static website hosting feature. And because I post certification articles it does get some fairly heavy use. Now in the entire time that I've ran my personal blog I think the most that I've ever been charged for S3 usage is 17 cents in one month.

So when I talk about being charged for S3 I'm going to mention it whenever we go beyond this free tier but keep in mind that often I'm talking about really tiny amounts of money relative to the value that you're getting so you can store a lot in S3 and use it to deliver a lot of data and often be charged a really tiny amount of money, often something that isn't noticeable on the bill of a production AWS account. Okay, that's enough on the theory of static website hosting, so now it's time for a demo and in this demo we're going to be using S3 to create a simple static website. Now I think this demo is going to be a useful one because it brings together a few of the theory concepts that I've been talking about over the last few lessons.

So go ahead, mark this video as complete and when you're ready, you can join me in the next demo lesson.

## s3-demo-creating-a-static-website-with-s3

Welcome back and in this demo lesson you're going to get some experience using the S3 static website hosting feature which I talked about in the previous lesson. Now to get started just make sure that you're logged in to the management account of the organization and that you're using the IAM admin user. So this just makes sure that you have admin permissions over the general or management account of the organization.

Also, make sure that you have the Northern Virginia region selected, which is US-East-1. Normally with S3, when you're interacting with the product, you're doing so using the AWS Console UI or the S3 APIs. And in this demo lesson, you'll be enabling a feature which allows S3 to essentially operate as a web server.

It allows anybody with a web browser to interact with an S3 bucket, to load an index page and load pictures or other media that are contained within that bucket using standard HTTP. So that's what we're going to do and to get started we need to move across to the S3 console. So either use S3 in recently visited services or you can click on the services dropdown, type S3 and then click it in this list.

Now that we're at the S3 console we're going to create an S3 bucket. Now if you chose to register a domain earlier in the course like I did, so I registered animalsforlife.io, then we're going to connect this S3 bucket with the custom domain that we registered so we can access it using that domain. If you chose not to use a domain then don't worry you can still do this demo.

What you need to do is to go ahead and click on create bucket. Now for the bucket name, if you are not using a custom domain, then you can enter whatever you want in this bucket name as long as it's unique. If you did register a custom domain and you want to use this bucket with that domain, then you need to enter a DNS formatted bucket name.

So in my case I'm going to create a bucket which is called Top 10. It's going to store the world's best cat pictures, the top 10 cat pictures in the world ever. and it's going to be part of the animalsforlife.io domain and so at the end of this I'm going to add dot and then animalsforlife.io and if you've registered your own custom domain then obviously you need to add your own domain at the end you can't use the same name as me once you've entered that name then just scroll down and uncheck 'Block all public access' this is a safety feature of S3 but because we're intentionally creating an S3 bucket to be used as a static website we need to uncheck this box.

Now, unchecking this box means that you will be able to grant public access. It doesn't mean that public access is granted automatically when you uncheck this box, they're separate steps. You will though need to acknowledge that you understand the risks of unticking that box.

So check this box just to confirm that you understand, we'll be carefully configuring the security so you don't have to worry about any of those risks. And once you've set that we can leave everything else as default. So just scroll all the way down to the bottom and click on 'Create Bucket'.

So the bucket's been created, but right now this only allows access using the S3 APIs or the console UI. So we need to enable static website hosting. Now to do that, we're going to click on the bucket.

Once we have the bucket open, we're going to select the properties tab. On the properties tab, scroll all the way down to the bottom. And right at the very bottom we've got static website hosting.

And you need to click on the edit button next to that. It's a simple yes or no choice at this point so check the box to enable static website hosting. There are a number of different types of hosting.

You can either just host a static website which is what we'll choose. Or you can redirect requests for an object. So this allows you to redirect to a different S3 bucket.

We'll be covering this later in the course. now just leave this selected so host a static website. Now in order to use the static website hosting feature you'll need to provide S3 with two different documents.

The index document is used as the home or default page for the static website hosting so if you don't specify a particular object when you're browsing to the bucket for example winky.jpg if you just browse to the bucket itself then the index document is used and we're going to specify index.html. So this means that an object called index.html will be loaded if we don't specify one. Now the error document is used whenever you have any errors.

So if you specify that you want to retrieve an object from the bucket which doesn't exist, the error document is used. And for the error document, we're going to call this error.html. So these two values always need to be provided when you enable static website hosting.

So now we've provided those we can scroll down and click on save changes. Now that that feature is enabled if we just scroll all the way down to the bottom you'll see that we have a URL for this bucket. So go ahead and copy that into your clipboard we're going to need this shortly so this is the URL that you'll use by default to browse to this bucket.

Now next what we need to do is to upload some objects to the bucket which this static website hosting feature is going to use. Now to To do that, scroll all the way to the top and just click on objects and then click on upload. So this is the most recent UI version for S3.

And so you have the ability to add files or add folders. Now we're going to use both of these. We're going to use the add files button to add the index.html and the error.html.

And we're going to use the add folder to add a folder of images. So first let's do the add files. So click on add files.

Now attached to this video is a link which downloads all of the assets that you'll need for this demo. So go ahead and click on that link to download the zip file and then extract that zip file to your local machine. And you'll need to move to the folder that you extracted from this zip file.

It should be called static_website_hosting. So go to that folder. And then again, there should be a folder in there called website_files.

So go ahead and click on there to go into that folder. Now there are three things inside this folder. Index.html, Error.html, and IMG.

So we'll start by uploading both of these HTML documents. So select Index.html and Error.html, and then click on Open. And that will add both of these to this upload table.

Next, click on Add Folder, and then select the IMG folder, and click on Upload. So this has prepared all of these different objects ready to upload to this S3 bucket. If we scroll down we'll see that the destination for these uploads is our S3 bucket and your name here will be different as long as it's the same as the name you picked for the bucket that's fine.

Go all the way to the bottom and then go ahead and click on upload and that will upload the index.html, the error.html and then the folder called "img" as well as the contents of that folder. So at this point that's all of the objects uploaded to the S3 bucket and we can go ahead and click on close. So now let's try browsing to this bucket using static website hosting.

So go ahead and click on properties, scroll all the way down to the bottom and here we've got the URL for this S3 bucket. So go ahead and copy this into your clipboard, open a new tab and then open this URL or click on this symbol to open it in a new tab. What you'll see is a 403 forbidden error and this is an access denied.

You're getting this error because you don't have any permissions to access the objects within this S3 bucket. Remember, S3 is private by default and just because we've enabled static website hosting doesn't mean that we have any permissions to access the objects within this S3 bucket. We're accessing this bucket as an anonymous or unauthenticated user so we have no method providing any credentials to S3 when we're accessing objects via static website hosting so we need to give permissions to any unauthenticated or anonymous users to access the objects within this bucket.

So that's the next thing we need to do we need to grant permissions to be able to read these objects to any unauthenticated user. So how do we do that? The preferred method is to use a bucket policy.

So that's what I'm going to demonstrate in order to to grant access to these objects. Now to add a bucket policy, we need to select the Permissions tab, so click on Permissions, and then below Block Public Access, there's a box to specify a bucket policy. So click on Edit, and we need to add a bucket policy.

Now also in the folder that you extracted from this lesson's zip file, is a file called bucket_policy.json, and this is a generic bucket policy. So this bucket policy has an effect of allow and it applies to any principle because we have this star wildcard. And because the effect is allow it grants any principle the ability to use the S3 get object action, which allows anyone to read an object inside an S3 bucket and it applies to this resource.

So this is a generic template. We need to update it, but go ahead and copy it into your clipboard. Go back to the S3 console and paste it into this box.

Now we need to replace this generic ARN, so this example bucket ARN. So what I want you to do is to copy this bucket ARN at the top of the screen. So copy this into your clipboard.

And we need to replace part of this template ARN with what we've just copied. Now an important point to highlight is that this ARN has forward slash star on the end. because this ARN refers to any objects within this S3 bucket.

So we need to select only the part before the forward slash. So starting at the A and then ending at the end of example bucket and then just paste in the ARN of our bucket that we just copied into our clipboard. What you should end up with is this full ARN with the name of the bucket that you created and then forward slash star.

And once you've got that, go ahead and click on Save Changes. This applies a bucket policy which allows any principal, so even unauthenticated principals, the ability to get any of the objects inside this bucket. So this means that any principal will be able to read objects inside this bucket.

At this point, assuming everything's okay, if you've still got the tab open to the bucket, then go back to that tab and hit Refresh. And what you should see is the top 10 animals in the world. So at position number one, we've got Merlin.

At position number two, we've got Merlin again. Position number three, another Merlin. Four, still Merlin.

And then Merlin again at number five. At number six, we've got Boris, so the token non-Merlin cat. Number seven, Samson, another token non-Merlin cat.

And then at number eight, we've got different cat one. He looks quite a lot like Merlin. Number nine, different cat two, again, kinda looks like Merlin.

And then number 10, we've got the family. And then you might not have guessed this, but this entire top 10 contest was judged by, you guessed it, Merlin. So what you're loading here is the index.html document inside the bucket.

So we haven't specified an object to load, and because of that, it's using the index document that we specified on the bucket. We can load the same object by typing specifically index.html on the end, and that will load in the same object. Now if we specify an object which doesn't exist, so let's say we used wrong index.html, then instead of the index document, now it's going to load the error document.

So this is the error document that you specified, which is loading error.html. So this is just an example of how you can configure an S3 bucket to act as a standard static website. So what it's doing is loading in the index.html object inside the bucket and that index.html is loading in images which are also stored in the bucket.

So if I right-click and copy the image location and open this in a new tab, this is essentially just loading this image from the same S3 bucket. So it's loading it from this folder called "img" and it's called "merlin.jpg". It's just an object loading from within the bucket.

Now if I go back to the S3 console and just move across to the properties tab and then scroll down, so far in this lesson you've been accessing this bucket using the bucket website endpoint. So this is an endpoint that's derived from the name of the bucket. Now your URL will be different because you will have called your bucket name something else.

Now if you chose to register a custom domain name at the start of this course, you can customize this further. As long as you call the bucket the same as the DNS name that you want to use, you can actually use Route 53 to assign a custom DNS name for this bucket. So this part of the demo you'll only be able to do if you've registered a domain within Route 53.

If you haven't, you can skip to the end of this demo where we're going to tidy up. But if you do want to customize this using Route 53, then you can click on the services dropdown and type route 53 and then click to move to the route 53 console. Once you're there, you can click on hosted zones and you should have a hosted zone that matches the domain that you registered at the start of the course.

Go inside that and click on create record. Now we're going to be creating a simple routing record, so make sure that's selected and then click on next and we're going to define a simple record. Now I'm going to type the first part of the name of the bucket.

So I used top 10 dot animals for life dot IO as my bucket name. So I'm going to put top 10 in this box. Now, because we want to point this at our S3 bucket, we need to choose an end point in this dropdown.

So clicking this dropdown and then scroll down and we're going to pick alias to S3 website endpoint. So select that. Next you need to choose the region and you should have created the S3 bucket in the US East 1 region because this is the default for everything that we do in the course.

So go ahead and type US-East-1 and then select US East Northern Virginia. And you should be able to click in Enter S3 endpoint and select your bucket name. Now if you don't see your bucket here, then either you've picked the wrong region or you've not used the same name in this part of the record name as you picked for your bucket.

So make sure this entire name, so this component plus the domain that you use, matches the name that you selected for the bucket. Assuming it does, you should be able to pick your bucket in this dropdown. Once you've selected it, go ahead and click on Define Simple Record.

And once that's populated in the box, click on Create Records. Now once this record's created, you might have to wait a few moments, but you should find that you can then open this bucket using this full DNS name. So there we go, you can see that it opens up the same bucket.

So we've used Route 53 and we've integrated it using an alias to our S3 endpoint. Now again, you can only do this if you create a bucket with the same name as the fully qualified domain name that we've just configured. So this is an example of a fully qualified domain name.

Now this is the host component of DNS and this is the domain component. So together they make up a fully qualified domain name. And for this to work you need to create an S3 bucket with the same bucket name as this fully qualified domain name.

And that's what I did at the start of this lesson which is why it works for me. And as long as you've done the same, as long as you've registered a custom domain, as long as you've called the bucket the same as what you're creating within Route 53, then you should be able to reference that bucket and then access it using this custom URL. At this point, we're going to tidy up.

So go back to the Route 53 console and select this record that you've created and then click on Delete. You'll need to confirm it by clicking Delete again. Then we need to go back to the S3 console, select the bucket that you've created, click on Empty, and you'll need to either type or copy and paste, permanently delete into this box, and then click on Empty.

It'll take a few minutes to empty the bucket. Once it's completed, click on Exit, and with the bucket still selected, click on Delete to delete the bucket. And you'll need to confirm that by either typing or copy and pasting the name of the bucket, and then click Delete Bucket.

Now at this point, that's everything that you need to do in this lesson. It's just an opportunity to experience the theory that you learned in the previous lesson. Now there's a lot more that you can do with static website hosting and I'll be going into many more complex examples later on in the course.

But for now this is everything that you need to do so go ahead and complete this video and when you're ready I'll look forward to you joining me in the next.

