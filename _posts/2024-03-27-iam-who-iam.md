---
title: "AWS SAA-C03 part 3: IAM"
categories:
  - exams
tags:
  - aws-saa-c03
---

Still having that cold. Been about a week of not being able to breathe. Living alone sounds VERY compelling right about now. No one to sneeze in my face...

## iam-identity-policies

Welcome back, and in this lesson, I want to start off by covering an important part of how AWS handles security. And I want to talk about IAM policies in this lesson. IAM policies are a type of policy which get attached to identities inside AWS.

And as you've previously learned, identities are IAM users, IAM groups, and IAM roles. Now, you'll use IAM policies constantly. You'll need to understand them for the exam, as well as if you design and implement solutions inside AWS.

Policies, once you understand them, are actually pretty simple. So I want to step you through the components and give you an opportunity to experiment with them inside your own AWS account. Understanding policies comes in three main stages.

First, you'll need to understand their architecture and how they work. Second, you need to gain the ability to read and understand the policy. And then finally, you'll need to learn to write your own.

For the exam, understanding their architecture and being able to read them is enough. So that's what I'll be focusing on in this lesson. You'll gain the ability to write them as you work through the course and get more practical exposure.

So let's jump in and get started. An IAM identity policy or an IAM policy is just a set of security statements to AWS. It grants access or denies access to AWS products and features to any identity which uses that policy.

Identity policies, also known as policy documents, are created using JSON. So it will help a lot if you've already experienced JSON before. If not, don't worry, it'll just need a little bit more time and effort.

This is an example of an identity policy document, and this is the type of thing that you would use with a user, group, or a role. At a high level, a policy document is just one or more statements. So inside this statement block, there are multiple statements.

Each of them is inside a pair of curly braces. And it's these statements which grant or deny permissions to AWS services. When an identity attempts to access AWS resources, that identity needs to prove who it is to AWS.

A process known as authentication. Once authenticated, that identity is known as an authenticated identity AWS knows which policies an identity has, and it could be multiple. And each of these policies can have multiple statements in it, so AWS has a collection of all of the statements which apply to a given identity.

AWS also knows which resource or resources you're attempting to interact with, as well as what actions you want to perform on those resources. AWS then works through all of the statements one by one and it reviews any that apply to a particular identity accessing a particular resource in a particular way. So let's step through what makes up a statement.

The first part of a statement is a statement ID, or a SID. And this is an optional field which lets you identify a statement and what it does. See how in this case it states full access?

In the second statement, it states DenyCatBucket. And that's just a way that we can inform the reader what this statement actually does. It's best practice to always use these, regardless of how big or small a policy document is.

Every interaction that you have with AWS is a combination of two main things, the resource that you're interacting with, and the actions that you're attempting to perform on that resource. So an example might be that you're attempting to interact with an S3 bucket and the action you might be attempting to perform is to add an object into that bucket. A statement only applies if the interaction that you're having with AWS match the action and the resource.

The action part of a statement matches one or more actions. It can be very specific and list a specific individual action. The format is service colon and then the operation.

So S3, colon, and then the operation is an example. Or, as shown on screen, you can use wild cards. So a wild card can match any S3 operations, if it's listed in the format s3:*.

Alternatively, actions could be a list of individual actions. So you've got three options. You have a specific individual action, a wild card, or a list of multiple independent actions.

Now, resources is the same, only it matches AWS resources. Now, you can use wild cards here too. So specify individual AWS resources, or you can specify lists of AWS resources, as with the second example.

Now you can use wild cards to refer to every resource, but if you do refer to either individual resources or lists of resources, use the ARN format or Amazon Resource Name, and I'll talk in a little bit more detail about that in the next lesson. Now, lastly, we have effect, and effect is either allow or deny. Effect controls what AWS does if the action and the resource parts of the statement match the operation that you're attempting to do with AWS.

So if you're attempting to access an S3 bucket, and the action and resource part of the statement match and the effect is allow, then AWS will allow you to access that resource using those actions. If the effect is deny, such as the one that's highlighted now, then if you're attempting to perform an action on a resource, it will be denied. Now it is possible that you could be allowed and denied at the same time.

So take this example that's on screen now. Imagine that you're attempting to access either the catgifs bucket or an object in the catgifs bucket. Well, the top statement will apply because that matches any S3 actions on any resource.

So if you're attempting to access the catgifs bucket, it will apply and it will allow that access. But the bottom statement denies any S3 actions on a specific S3 bucket. Understanding policies where there's only one allow or one deny is easy because there's no overlap.

The challenge is when you do have this overlap, and you'll fairly often see questions related to this in the exam. So let's take a look at that in more detail. For this example now, let's assume that an entity is attempting to access an object in the catgifs bucket, and that identity has this policy attached to it.

So the one that's on the screen now. Visually we can show this as a Venn-style graphic. The first statement is pretty wide.

It allows full access to all of the S3 service. It's all S3 actions on all resources. So with this statement on its own, you could access any object in any bucket in S3.

You could perform operations on any object or any bucket or even create and delete buckets. Essentially, with this statement, you're an S3 administrator. The second statement denies access to a small portion of S3.

In this case, it's the catgifs bucket and any objects in that bucket. One of the most important security concepts in AWS for the exam and for the real world is how to handle this overlap-style situation. If there are multiple statements which apply to an operation in AWS, as with this example, then both of the statements are processed.

So in this case, you're both allowed access to all of S3 and denied access to this specific bucket. Now, luckily there are a set of consistent rules which make things pretty easy to remember. If you remember the rule, it'll always make sense.

We start with the first priority. The first priority are explicit denies. What that means is that if you have a statement which explicitly denies access to something, then that's it.

It wins. It overrules everything else. The policy denies access to a particular resource and action combination, and nothing can overrule that.

In this example, accessing the catgifs bucket or any object in that bucket is explicitly denied. That's it, nothing can overrule that. The second priority are explicit allows.

And in this example, this statement explicitly allows access to all S3 actions on any resource. And these take effect unless, and this is the really important part, unless there is also an explicit deny. If you're explicitly allowed access to something, which the top statement does, and you're also explicitly denied access to something, as the bottom statement does, the deny always wins.

Explicit denies always take priority. Lastly, if neither of those apply, so if you're attempting to do something for which you have no explicit allow and no explicit deny, then the default implicit deny takes effect. With the exception of the Account Root User, AWS identities start off with no access to any AWS resources.

It's really important for you to understand this. If they're not allowed access, they have no access. Get used to repeating this rule.

Deny, allow, deny. Say it while cooking, while cleaning, while working out. Even try to say it while you're sleeping.

Just this one rule will mean that you can answer questions much quicker in the exam. It's the same rule, if one statement applies or 10. If one policy document applies, or 10.

It doesn't matter. If there are no allows, which apply to a specific action on a particular resource, then you have no access. If there is an explicit allow, then you do have access, unless there is an explicit deny.

If you have an explicit deny on anything, that always wins. So the rule is deny, allow, deny. Now, it can be more complex because there might be multiple policies involved.

Take Sally, for example. She's a developer and she's trying to access a resource inside AWS. Sally has two policies which apply to her, policy one and policy two.

But Sally is also a member of a group. That group is called the Developers Group. So she's a member of that group, and that group also has a policy associated with it.

So Sally attempts to access an AWS resource, and that AWS resource might also have a policy associated with it. All of these policies will have one or more statements inside them. And the way that AWS handles this is when a given identity accesses a resource, it collects all of the statements in all of the policies which apply.

So the users directly, the groups the users are in, and any resource policies on the resources that they're attempting to access, it collects all of these together and evaluates them all at the same time. But the same rule applies, deny, allow, deny. If there's ever an explicit deny, that's it, game over.

If there's an explicit allow, then you're allowed access, unless there is a deny. And if none of those apply, there is always the default implicit deny. Now, there's one more thing I want to cover before I finish up this lesson, and that's that there are two main types of policies, inline policies, and managed policies.

Now, they're the same thing. They're JSON policy documents. The difference is how they're managed.

Let's say we have a hundred staff in our business and of these 100 staff, we're gonna use an example focusing on three. We've got Sally from the previous example and she's a developer. Miles in accounts and Mike in production.

So let's say you're running a secret project and you want to grant these three access to the resources for that project. Then you could do it in one of two main ways. First, you could design a policy that grants access to the resources needed for that project and then assign that JSON individually on three separate accounts.

Now, that's known as an inline policy. Crucially, what you're doing there is you're applying the JSON to each account individually. It becomes three isolated bits of JSON.

Now, this would work in this situation, but it's not best practice. Because it's three individual inline policies, each of which is an individual piece of JSON, changing the access rights would mean changing it on all three of these inline policies. Doing this for three staff might sound easy, but what about 300?

And then if you needed to change the policy that's applied to those 300 staff, well, you'd have to edit 300 inline policies because they're unique to each identity. Another option is to use what's known as a managed policy, and managed policies are created as their own object. First, you'd create the managed policy which is just a piece of JSON with some statements in, and then you'd attach that policy to any identities who you wanted to gain those access rights.

Now, managed policies are great for two main reasons. First, they're reusable. So in this example, I can use the same managed policy for three identities or for 300.

So for access rights that you want to grant to large numbers of users, groups, and roles, you should definitely use managed policies. Managed policies should be used for the normal default operational rights in your business. So if you've got a set of common access rights that you want to give to lots of people, then you should use managed policies.

Now, secondly, managed policies are low management overhead. So if you do need to change the JSON in a managed policy, then it immediately impacts all of the identities it's attached to. So the question is when would you use an inline policy?

Well, generally, this is for exceptions to the normal access rights that you want to grant, so special circumstances, exceptional access rights. When you need to ensure that a specific set of rights, either giving an individual more access rights or blocking certain permissions for one individual identity, then you can use inline policies, apply those to one particular user, and then influence the permissions on that user. So generally, when you're using inline policies, it's for special or exceptional allows or denies.

Now, there are two main types of managed policies. AWS managed policies, which are created and managed by AWS. Now, you don't need to manage these, but they might not fit your exact needs.

And then you have customer managed policies which you can create and manage so you can define them as per the exact requirements of your business. Now, I do want to give you the chance to gain practical experience of how to use these different types of permissions within identity policies in AWS. So elsewhere in this section, there's going to be an opportunity for you to gain some practical experience.

But initially, I just want to introduce the theory. Now at this point, that's everything that I want you to do in this lesson. So go ahead and complete the video, and when you're ready, I look forward to you joining me in the next.

## iam-users-and-arns

Welcome back. And in this lesson, I want to finish my coverage of IAM users. You already gained some exposure to IAM users earlier in the course.

Remember, you created an IAM admin user in both your general and production AWS accounts. As well as creating these users, you secured them using MFA, and you attached an AWS managed policy to give this IAM user admin rights in both of those accounts. So for now, I just want to build upon your knowledge of IAM users by adding some extra detail that you'll need for the exam.

So let's get started. Now, before I go into more detail, let's just establish a foundation. Let's use a definition.

Simply put, IAM users are an identity used for anything requiring long-term AWS access. For example, humans, applications or service accounts. If you need to give something access to your AWS account, and if you can picture one thing, one person or one application.

So James from accounts, Mike from architecture, or Miles from development, 99% of the time you would use an IAM user. If you need to give an application access to your AWS account, for example a backup application running on people's laptops, then each laptop generally would use an IAM user. If you have need for a service account, generally a service account which needs to access AWS, then generally this will use an IAM user.

If you can picture one thing, a named thing, then 99% of the time, then correct identity to select is an IAM user. And remember this because it will help in the exam. IAM starts with a principal.

And this is a word which represents an entity trying to access an AWS account. At this point, it's unidentified. Principals can be individual people, computers, services or a group of any of those things.

For a principal to be able to do anything, it needs to authenticate and be authorized. And that's the process that I want to step through now. A principal, which in this example, is a person or an application, makes requests to IAM to interact with resources.

Now, to be able to interact with resources, it needs to authenticate against an identity within IAM. An IAM user is an identity which can be used in this way. An authentication is this first step.

Authentication is a process where the principal on the left proves to IAM that it is an identity that it claims to be. So an example of this is that the principal on the left might claim to be Sally, and before it can use AWS, it needs to prove that it is indeed Sally. And it does this by authenticating.

Authentication for IAM users is done either using username and password or access keys. These are both examples of long-term credentials. Generally, username and passwords are used if a human is accessing AWS and accessing via the console UI.

Access keys are used if it's an application, or as you experienced earlier in the course, if it's a human attempting to use the AWS Command Line tools. Now, once a principal goes through the authentication process, the principal is now known as an authenticated identity. An authenticated identity has been able to prove to AWS that it is indeed the identity that it claims to be.

So it needs to be able to prove that it's Sally. And to prove that it's Sally, it needs to provide Sally's username and password, or be able to use Sally's secret access key, which is a component of the access key set. If it can do that, then AWS will know that it is the identity that it claims to be, and so it can start interacting with AWS.

Once the principal becomes an authenticated identity, then AWS knows which policies apply to the identity. So in the previous lesson, I talked about policy documents, how they could have one or more statements, and if an identity attempted to access AWS resources, then AWS would know which statements apply to that identity. That's the process of authorization.

So once a principal becomes an authenticated identity, and once that authenticated identity tries to upload to an S3 bucket or terminate an EC2 instance, then AWS checks that that identity is authorized to do so. And that's the process of authorization. So they're two very distinct things.

Authentication is how a principle can prove to IAM that it is the identity that it claims to be using username and password or access keys, and authorization is IAM checking the statements that apply to that identity and either allowing or denying that access. Okay, let's move on to the next thing that I want to talk about, which is Amazon Resource Names, or ARNs. ARNs do one thing, and that's to uniquely identify resources within any AWS accounts.

When you're working with resources, using the command line or APIs, you need a way to refer to these resources in an unambiguous way. ARNs allow you to refer to a single resource, if needed, or in some cases, a group of resources using wild cards. Now, this is required because things can be named in a similar way.

You might have an EC2 instance in your account with similar characteristics to one in my account, or you might have two instances in your account but in different regions with similar characteristics. ARNs can always identify single resources, whether they're individual resources in the same account or in different accounts. Now, ARNs are used in IAM policies which are generally attached to identities, such as IAM users, and they have a defined format.

Now, there are some slight differences depending on the service, but as you go through this course, you'll gain enough exposure to be able to confidently answer any exam questions that involve ARNs. So don't worry about memorizing the format at this stage, you will gain plenty of experience as we go. These are two similar, yet very different ARNs.

They both look to identify something related to the catgifs bucket. They specify the S3 service. They don't need to specify a region or an account, because the naming of S3 is globally unique.

If I use a bucket name, then nobody else can use that bucket name in any account worldwide. The difference between these two ARNs is the forward slash star on the end at the second one. And this difference is one of the most common ways mistakes can be made inside policies.

It trips up almost all architects or admin at one point or another. The top ARN references an actual bucket. If you wanted to allow or deny access to a bucket or any actions on that bucket, then you would use this ARN which refers to the bucket itself.

But a bucket and objects in that bucket are not the same thing. This ARN references anything in that bucket, but not the bucket itself. So by specifying forward slash star, that's a wild card that matches any keys in that bucket, so any object names in that bucket.

This is really important. These two ARNs don't overlap. The top one refers to just the bucket and not the objects in the bucket.

The bottom one refers to the objects in the bucket but not the bucket itself. Now, some actions that you want to allow or deny in a policy they operate at a bucket level or actually create buckets. And this would need something like the top ARN.

Some actions work on objects, so it needs something similar to the bottom ARN. And you need to make sure that you use the right one. In some cases, creating a policy that allows a set of actions will need both.

If you want to allow access to create a bucket and interact with objects in that bucket, then you would potentially need both of these ARNs in a policy. ARNs are collections of fields split by a colon. And if you see a double colon, it means that nothing is between it.

It doesn't need to be specified. So in this example, you'll see a number of double colons because you don't need to specify the region or account number for an S3 bucket because the bucket name is globally unique. A star can also be used, which is a wild card.

Now, keep in mind they're not the same thing. So not specifying a region and specifying star don't mean the same thing. You might use a star when you want to refer to all regions inside an AWS account.

Maybe you want to give permissions to interact with EC2 in all regions, but you can't simply omit this. The only place you'll generally use the double colon is when something doesn't need to be specified, you'd use a star when you want to refer to a wild card collection of a set of things. So they're not the same thing.

Keep that in mind, and I'll give you plenty of examples as we go through the course. So the first field is the partition, and this is the partition that the resource is in. For standard AWS regions, the partition is AWS.

If you have resources in other partitions, the partition is AWS hyphen partition name. This is almost never anything but AWS. But for example, if you do have resources in the China Beijing region, then this is AWS-cn.

The next part is service. And this is the service name space that identifies the AWS product. For example, S3, IAM, or RDS.

The next field is region. So this is the region that the resource you're referring to resides in. Some ARNs do not require a region, so this might be omitted, and certain ARNs require wild card.

And you'll gain exposure through the course as to what different services require for their ARNs. The next field is the account ID. This is the account ID of the AWS account that owns the resource.

So for example, 123456789012. So if you're referring to an EC2 instance in a certain account, you will have to specify the account number inside the ARN. Some resources don't require that, so this example is S3 because it is globally unique across every AWS account.

You don't need to specify the account number. And then at the end, we've got resource or resource type. And the content of this part of the ARN varies depending on the service.

A resource identifier can be the name or ID of an object. For example, user forward slash Sally or instance forward slash and then the instance ID, or it can be a resource path. But again, I'm only introducing this at this point.

You'll get plenty of exposure as you go through the course. I just want to give you this advanced knowledge so you know what to expect. So let's quickly talk about an exam PowerUp.

I tend not to include useless facts and figures in my course but some of them are important. This is one such occasion. Now first, you can only ever have 5,000 IAM users in a single account.

IAM is a global service, so this is a per account limit, not per region. And second, an IAM user can be a member of 10 IAM groups. So that's a maximum.

Now, both of these have design impacts. You need to be aware of that. What it means is that if you have a system which requires more than 5,000 identities, then you can't use one IAM user for each identity.

So this might be a limit for internet scale applications with millions of users, or it might be a limit for large organizations which have more than 5,000 staff, or it might be a limit when large organizations are merging together. If you have any scenario or a project with more than 5,000 identifiable users, so identities, then it's likely that IAM users are not the right identity to pick for that solution. Now, there are solutions which fix this.

We can use IAM roles or Identity Federation, and I'll talking about both of those later in the course. But in summary, it means using your own existing identities rather than using IAM users. And I'll be covering the architecture and the implementation of this later in the course.

At this stage, I want you to take away one key fact and that is this 5,000 user limit. If you are faced with an exam question which mentions more than 5,000 users, or talks about an application that's used on the internet which could have millions of users, and if you see an answer saying create an IAM user for every user of that application, that is the wrong answer. Generally with internet scale applications, or enterprise access or company mergers, you'll be using Federation or IAM roles.

And I'll be talking about all of that later in the course. Okay, so that's everything I wanted to cover in this lesson. So go ahead, complete the video and when you're ready, I'll look forward to you joining me in the next.

## iam-demo-simple-identity-permissions-in-aws

Welcome back and in this demo lesson we're going to explore IAM users. This is the first type of identity that we've covered in AWS. We're going to use the knowledge that we gained in the IAM policy documents lesson and assign an IAM user some permissions in our AWS account.

Now to get started you'll need to be logged in as the IAM admin user to the general AWS account and you'll also need to have the Northern Virginia region selected. Now attached to this lesson are two links. The first is a one-click deployment link which will deploy the infrastructure that you'll need for this demo.

And the second is a link which will download the files you'll need for this demo. So go ahead and click the demo files link to start that download. And then click the one-click deployment link to begin the deployment.

Now earlier in the course you've already created an IAM user that you should be logged into this account with. So I'm not going to step through the process again of creating an IAM user. Instead we're going to use CloudFormation to apply a template and this template is going to create an IAM user called Sally and it's also going to create two S3 buckets that we'll be using in this demonstration together with a managed policy that we'll also be using.

Then you'll need to enter as a parameter the password for the Sally user that this CloudFormation stack will create. We'll only be using this user for this lesson so you should probably make it something that's reasonably secure but you don't need to make it a massively random password just use something that you can remember and something that you can type. Now this password does need to meet the password policy that's assigned to your AWS account.

Most AWS accounts come with a password policy where the minimum password length is eight characters and it also includes a minimum of three of the following mix of character types so uppercase, lowercase, numbers and certain special characters. Additionally it cannot be identical to your AWS account name or email address. So enter that password, scroll down, check this capabilities box and click on create stack.

Now all that creates, I just want to switch I switch over to my text editor and this is what this template does. So it essentially asks for a parameter, so Sally's password, and then it creates a number of resources. We've got a logical resource called 'catpix', which is an S3 bucket, a logical resource called 'animalpix', again, which is an S3 bucket.

We've also got a logical resource called 'Sally', which is an IAM user and I want to draw your attention to a number of key things. The first is that this IAM user has a managed policy attached to it. So that's what this part of the configuration does.

This references an ARN for a managed policy that I'll show you once the stack's complete and applying. It also sets the login profile and this is how we set the password and this references the parameter at the top of the template and it also sets so that you need to reset the password upon first login. And then the last thing that I want to talk about quickly is this policy logical resource, which is a managed policy.

And if you recall, when I've been talking about permissions in the last few lessons, I demonstrated a particular policy document that allowed access to all S3, but then denied access to a CatPix S3 bucket. And that is what's defined here. So this creates a managed policy that will allow access to S3, but won't allow access to the CatPix bucket.

So that's all that this does. If I just quickly now switch back over to the console and then just refresh. Yep, this is completed now.

So I can click on Resources and see that we've got four resources that have been created. The AnimalPix S3 bucket, the CatPix S3 bucket, the IAM Managed Policy, and the Sally IAM User. Now note that I didn't set any particular explicit hard-coded names here.

And so what CloudFormation does in that circumstance is it automatically generates resource names. And the way that it generates these names is to take the name of the stack, which is "I am", the name of the logical resource defined in the template, so "animal_pics", "cat_pics", and "sally", and then it puts on the end some randomness. So you're always guaranteed that the physical ID that CloudFormation generates will always be unique.

So now this has finished creating, I just want to go ahead and open up the Sallie IAM user. So I'm going to click on that link under Resources. And I want to draw your attention to the fact that Sallie has this attached managed policy called IAM User Change Password.

Remember in previous lessons I talked about the different types of managed policy. If I go to Policies here, these are all of the managed policies inside the account at the moment. And most of these are AWS managed policies, so policies created and managed by AWS.

And one of those is that policy that's been assigned to the SALLU user. So that allows an IAM user to change his or her password upon first login. So that's something that we're going to utilize now.

So what I'm going to ask you to do is to click on Dashboard and just make sure that you've got this IAM users sign-in link on your clipboard. Next, you need to either open a private browser tab or a separate browser completely. I'm going to go ahead and use an add-on for Firefox, and I'm going to open a temporary container.

Now you need this to be separate from the browser that you're currently logged in. We don't want to be logged out of our IAM admin user. So ideally a separate browser, or if you've got Firefox, or if you know that you can create isolated tabs, then go ahead and do that.

And once you've got that, just paste in the IAM sign in link for the general account. That's the one that you just copied onto your clipboard. So this is the IAM sign in page for the general AWS account.

So I need to go back and get the username for Sally. So I'm going to go back to CloudFormation. I'm going to click on outputs and I'm just going to copy the username for Sally.

The template also had an output section and this is the easiest way to get the username for Sally. So I'm going to copy that into my clipboard and paste that in to the I am username box here, and then I'll need to enter the password that I chose for Sally. So remember when you created the CloudFormation stack, you were prompted for a password.

So go ahead and enter that. And then click on sign in. So now we logged into Sally's I am user and we need to change the password.

So enter the old password and then choose a new password, a secure password. And the reason you can do this is because of that managed policy that's assigned to Sally that gives her just enough permissions to change her own password. So do that and click on confirm password change and then you'll be logged in to the console UI as the Sally IAM user.

Now just to demonstrate the permissions that Sally has we're going to move to the EC2 console and just try to interact with EC2. You might see some API errors straight away. If I change across to the S3 console we'll see the same thing.

We won't have any permissions to list any S3 buckets, even though we know that we have got at least two buckets because they were created by the CloudFormation template. So that just proves that an IAM user has no permissions when they first get created in an AWS account. They generally start off with this managed policy that allows them to change their password, but outside that they don't have any permissions.

Now at the start of the demo you downloaded a link which is the demo files for this demo. That's a zip file, so I want you to go ahead and locate that file and then extract it. It will create a folder containing all the files that you'll need from this point onward.

Within this folder there's a specific file that we're going to open and look at next, and it's called S3_FullAdminJSON. So go ahead and open that file, and this is a JSON policy document that grants full access to any S3 actions, so S3 colon star, on any S3 resource. So this is an ARN that represents any S3 resource.

And the first thing I'm going to have you do is assign this to Sally as an inline policy. So to do that, just open this file up and then copy it into your clipboard. Go back to the console.

Open the tab or the browser that you've got logged into IAM Admin and you're on the IAM area of the console and just open the Sally user. Make sure you're on the Permissions tab, then Add Permissions, Create Inline Policy. Now you can go through this wizard type interface of selecting Services, Actions, and Resources.

That's often quite easy to make sure that you've got a correct policy applied, but you can also select the JSON tab and enter raw JSON. And that's what I'm going to do. So I want you to do this as well.

Select the JSON document that exists already and just delete that and then paste in that JSON document that you've just copied into your clipboard. So this has one statement that allows all S3 actions on all S3 resources. So that looks good.

Go ahead and hit Review Policy. Give it a name, call it S3 Admin Inline. All one word, so S3 Admin Inline, and hit Create Policy.

So Sally now has, in addition to the I am user change password managed policy, She also has this S3 admin in-line. So now if you either go to the separate browser or the separate isolated tab that you're logged into using Sally, if you hit refresh, you should be able to then see the S3 buckets. So there we go.

We've got the IAM Animal Picks bucket and the IAM Cat Picks bucket. Now just to demonstrate that we have full access over both of these buckets, if you go into the IAM Animal Picks bucket and click on Upload, Select Add Files, locate the folder containing the files for this demo that you downloaded and extracted earlier. Go in there and there's a thor.jpg file.

Select it and click on Open and then upload that to this bucket. So that proves that the Sallie user has permissions to upload to the AnimalPix bucket. So go back to the S3 console, go into CatPix, click on Upload.

This time, if you go into the CatPix folder and there's a file in there called merlin.jpg, Go ahead and upload that to this bucket. And there we go, we can see that Sally's got the ability to upload to the cat pics bucket as well. So now to make sure that we can read from the cat pics bucket, just go ahead and click on merlin.jpg and then select open.

And there we go, we can see Merlin and he is definitely approving of your AWS skills. It looks very approval, serious cat. So that proves that we can access that bucket.

So now I want you to switch to the other browser that you've got, the one that's logged in as the IAM admin user and for me it's this separate tab. Open up the SALLU user, you should still have it open, and just delete the S3 admin inline policy that we added moments ago. So that will return the SALLU user to having no access rights over S3.

And if we return to the other browser window, in my case it's the other tab, and refresh it, again we'll get the access denied error. So that's good, that's what we expect. So now go back to the other browser window again, the one that's logged in as imadmin.

We're still open in the Sallie user. This time click on add permissions and it's here where we can attach a managed policy. So select attach policies directly, and this is where you can attach a managed policy.

Now you should see the one that's been created by the CloudFormation template, which is allow all S3 except cats. So select that one, click 'Next' and then 'Add Permissions' and this will attach this Managed Policy to the SALLU user. So if you expand that, you'll be able to see what this Managed Policy is.

So it's a slightly different policy. This time it's got two statements. Remember, a policy document is a list of statements.

So this particular one has two. We've got this first statement which allows any S3 actions on any resource. So that's essentially S3 admin.

And we've got the second statement which denies any S3 actions on just the catpix bucket and any objects in the catpix bucket. Now remember deny, allow, deny. An explicit deny always takes priority.

So the top statement will allow us access to everything in S3 that's an explicit allow. But this bottom statement will explicitly deny us access to a certain area of S3. And because of Deny, Allow, Deny, and Explicit, Deny always overrides everything else.

So what this should do now, if we return to the Sall user is we should be able to interact with any other bucket in S3 apart from the CatPix bucket and anything that's inside the CatPix bucket. So let's test that out. You'll need to move back to your other browser in my case the other tab that's logged in as Sally, hit refresh.

Because we've got this permission to be able to interact with the entire S3 you'll be able to do a bucket list. But if you go into the Catpix bucket you'll get an access denied because you can't perform any operations on the Catpix bucket now. So unfortunately you won't be able to see Merlin approving of your AWS skills anymore.

What you will be able to do though, if you go back to the S3 console and go in Animal Picks, you'll be able to open this object. So if I click on this object and go to open, you'll be able to see Thor and Thor is a stand-in for Merlin and Thor definitely approves of your growing AWS skills. So this has just been a simple demonstration of being able to apply different types of policies to an IAM user.

We've applied an inline policy that grants full admin rights over S3. We've removed that. We've attached a managed policy which has a mixture of an explicit allow and an explicit deny.

And you've seen how these various bits and pieces affect the effective permissions that Sally has. So that's everything that I wanted to cover in this demo. We're going to be using the Sally IAM user over the next couple of lessons just to further demonstrate some features of I am.

So I am groups and how permissions work with groups. But because we're using CloudFormation and because I want you to gain the experience of cleaning up resources after demo lessons, we're going to delete everything that we've created in this lesson. So let's get started.

First, you'll need to delete this managed policy attachment from Sally. So I'll go ahead and do that and then as the IAM admin user, that's important, go to the S3 console select the catpix bucket and then click on empty. You'll need to copy and paste or type permanently delete into the text field and then click on empty.

Once you've done that click on exit to return to the S3 console and then do the same with the animal pix bucket. So select it, click on empty, type in permanently delete and and then click on empty and then click on exit to return back to the console. And then if you do both of those, then you can go back to CloudFormation, you can select the IAM stack and hit delete.

And that will clean up everything that's been created by this stack. But that's everything that I wanted to cover, so go ahead, complete this video and when you're ready, join me in the next.

## iam-groups

Welcome back. In this lesson, I want to briefly cover IAM groups, so let's get started. IAM groups, simply put, are containers for IAM users.

They exist to make organizing large sets of IAM users easier. You can't login to IAM groups and IAM groups have no credentials of their own. The exam might try to trick you on this one, so it's definitely important that you remember you cannot log into a group.

The question or the answer suggests logging into a group, it's just simply wrong. IAM groups have no credentials and you cannot log into them. So they're used, solely, for organizing IAM users to make management of IAM users easier.

So let's look at a visual example. We've got an AWS account and inside it we've got two groups: Developers and QA. In the Developers group, we've got Sally and Mike.

In the QA group, we've got Nathalie and Sally. Now the Sally user, so the Sally in Developers and the Sally in the QA group, that's the same IAM user. An IAM user can be a member of multiple IAM groups.

So that's important, as well, to remember for the exam. Groups give us two main benefits. First, they allow effective, administration-style management of users.

So we can make groups that represent teams, or projects, or any other functional groups inside a business and we can put IAM users into those groups, so it helps us organize. Now, the second benefit, which builds off the first, groups can actually have policies attached to them, and this is both inline policies and managed policies. In the example that's on screen now, the Developers group have a policy attached as do the QA group, and there's also nothing to stop IAM users, which are themselves within groups, also having their own inline or managed policies.

And this is the case with Sally. Now, when an IAM user such as Sally is added as a member of a group, and let's say the Developers group, that user gets the policies that are attached to that group. So Sally gains the permissions of any policies that are attached to the Developers group and any other groups that that user is a member of.

So Sally also gets the policies attached to the QA group, and Sally has any policies that she has directly. With this example, Sally is a member of the Developers group, which has one policy attached, a member of the QA group with an additional policy attached, and she has her own policy, so AWS merges all of those into a set of permissions. So effectively, she has three policies associated with her user, one directly, and one from each of the group memberships that her user has.

When you're thinking about the allow or denies in policy statements for users that are in groups, you need to think about those which apply directly to the user and their group memberships. So collect all of the policy allows and denies that a user has directly and from their groups, collect them all up and apply the same deny-allow-deny rule to them as a collection. So evaluating whether you're allowed or denied access to a resource, it doesn't specifically get any more complicated.

It's just the source of those allows and denies can broaden when you've got users that are in multiple IAM groups. Now, I mentioned last lesson that an IAM user can be a member of 10 groups and there was a 5,000 IAM user limit for an account. Neither of those are changeable.

They're hard limits. There's no effective limit for the number of users in a single IAM group. So you could have all 5,000 IAM users in an account being a member of a single IAM group.

Another common area of trick questions in the exam is around the concept of an all-users group. There isn't actually a built-in all-users group inside IAM so you don't have a single group that contains all of the members of that account like you do with some other identity management solutions. In the case of IAM, you could create a group and add all of the users in that account into the group, but you would need to create and manage it yourself.

So that doesn't exist natively. Another really important limitation of groups is that you can't have any nesting. You can't have groups within groups.

IAM groups contain users and IAM groups can have permissions attached. That's it. There's no nesting and groups cannot be logged into; they don't have any credentials.

Now, there is a limit of 300 groups per account but this can be increased with a support ticket. Now, there's also one more point that I want to make at this early stage in the course. This is something that many other courses tend to introduce later on or at a professional level, but it's important, I think, that you understand this from the very start.

I'll show you, later in the course, how policies can be attached to resources, for example, S3 buckets. These policies, known as resource policies, they can reference identities, so, for example, a bucket could have a policy associated with that bucket and that policy could allow Sally access to that bucket. So that's a resource policy.

It controls access to a specific resource and it allows or denies identities to access that bucket. Now it does this by referencing these identities and it references these identities using an ARN, or Amazon resource name. Users and IAM roles which I'll be talking about later in the course, can be referenced in this way.

So a policy on a resource can reference IAM users and IAM roles by using the ARN. So a bucket could give access to one or more users or it could give access to one or more roles but groups are not a true identity. They can't be referenced as a principal in a policy.

A resource policy cannot grant access to an IAM group. So you can grant access to IM users. and those users can be in groups, but a resource policy cannot grant access to an IAM group.

It can't be referred to in this way. So you couldn't have a resource policy on an S3 bucket and grant access to the Developers group and then expect all of the developers to access it. That's not how groups work.

Groups are just there to group up IAM users and allow permissions to be assigned to those groups, which the IAM users inherit. So this is an important one to remember, whether you are answering an exam question which involves groups, users, and roles or resource policies, or whether you're implementing real world solutions. It's easy to overestimate the features that a group provides.

Don't fall into the trap of thinking that a group offers more functionality than it does. It's simply a container for IM users. That's all it's for.

It can contain IM users. It can have permissions associated with it; that's it. You can't logon to them and you can't reference them from resource policies.

Okay, so that's everything I wanted to cover in this lesson. Go ahead, complete the video, and when you're ready, I'll look forward to you joining me in the next.

## iam-demo-permissions-control-using-iam-groups

Welcome back and welcome to this demo of the functionality provided by IAMGroups. What we're going to do in this demo is use the same architecture that we had in the IAM users demo, so the SALLI user and those two S3 buckets, but we're going to migrate the permissions that the SALLI user has from the user to a group that SALLI is a member of. Before we get started just make sure that you are logged in as the IAM admin user of the general AWS account and as always you'll need to have the Northern Virginia region selected.

Now attached to this video is a demo files link that will download all of the files you're going to use throughout the demo. So to save some time go ahead and click on that link and just start that file downloading. Once it's finished go ahead and extract it and it will create a folder which contains all of the files You'll need as you move through the demo now You should have deleted all of the infrastructure that you used in the previous demo lesson So at this point we need to go ahead and recreate it now to do that attached to this lesson is a one-click Deployment link so go ahead and click that link Everything is pre-populated, so you need to make sure that you put in a suitable password Which doesn't breach any password policy on your account So I've included a suitable default which includes some substitution So that should be okay for all common password policies So just go ahead scroll down to the bottom click on the capabilities checkbox and then create stack That'll take a few moments to create So I'm going to pause the video and resume it once that stack create has completed Okay, so that's created now.

So click on services and open the S3 console in a new tab This can be a normal tab Go to the cat pics bucket click upload add file locate the demo files folder that you downloaded and extracted Earlier inside that folder should be a folder called cat pics go in there and then select merlin.jpg Click on open and upload wait for that to finish once it's finished back to the console go to animal pics Upload again, add files. This time inside the AnimalPix folder, upload thaw.jpg again. And click upload.

Once that's done, go back to CloudFormation, click on Resources, click on the Sally user. Inside the Sally user, click on Add Permissions, Attach Policies Directly, Select the "Allow all S3 except cats", click on Next, and and add permissions. So that brings us to the point of where we were in the IAM users demo lesson.

So that's the infrastructure set back up in exactly the same way as we left the IAM users demo. So now we can click on dashboard. You'll need to copy the IAM signing users link for the general account.

So copy that into your clipboard. And again you're going to need ideally a separate browser, a fully separate browser, or you can potentially use a private browsing tab in your current browser but it is just easier to understand probably for you at this point in your learning if you have a separate browser window. I'm going to use an isolated tab because it's easier for me to show you and you'll need to paste in this IAM URL because now we're going to sign into this account using the Sallie user.

So go back to CloudFormation, click on outputs and you'll just need the Sallie username. So copy that into your clipboard. go back to this separate browser window and paste that in.

Then back to CloudFormation, Parameters tab and get the password for the Sally user. And then enter the password that you chose for Sally when you created the stack. Then move across to the S3 console and just verify that the Sally user has access to both of these buckets.

The easiest way of doing that is to just open both of these animal pictures. So we'll start with Thor. Thor's a big doggo, so it might take some time for him to load in.

There we go, he's loaded in. And the catpix bucket. And we get access denied because remember, Sally doesn't have access to the catpix bucket.

That's as intended. So now we'll go back to our other browser window, the one where we logged into the general account as the IAM admin user. And this is where we're going to make the modifications to the permissions.

We're going to change the permissions over to using a group rather than directly on the Sally user. So click on the Resources tab first and select Sally to move across to the Sally user. Now note how Sally currently has this managed policy directly attached to her user.

So step one is we're going to remove that. So remove this managed policy from Sally. So detach that.

That now means that Sally has no permissions on S3. And if we go back to the separate browser window that we've got Sally logged into, and then hit refresh, see she doesn't have any permissions now on S3. So now back to the other browser, back to the one where we logged in as IAM admin, and then we'll click user groups.

And then we're going to create a developers group. So click on create new group and call it developers. So that's the group name.

Then down at the bottom here, this is where we can attach a managed policy to this group. So we're going to attach the same managed policy that Sally had previously directly on her user. So allow all S3 accept cats.

So type allow into the filter box and press enter. And then check the box to select this managed policy. We could also directly at this stage add users to this group, but we're not going to do that.

We're going to do that as a separate process. So click on 'Create Group'. So that's the developer's group created.

So notice how there's not that many steps to create a group simply because it doesn't offer that much in the way of functionality. So open up the group. The only options that you see here are 'User Membership' and any attached permissions.

Now, as with a user, you can attach inline policies or attach managed policies, and we've got the managed policy. But what we're going to do next is click on Users, and then Add Users to Group. And we're going to select the Sally IAM user, and click on Add User.

So now our IAM user Sally is a member of the Developers group, and the Developers group has this attached managed policy that allows them to access everything on S3 except the CatPix bucket. So now if I move back to my other browser window where I've got the Sally user logged into and then refresh, now that the Sally user has been added to that group we've got permissions again over S3. If I try to access the catpix bucket I won't be able to because that managed policy that the development team have doesn't include access for this.

But if I open the animal pix bucket and open Thor again It's a big doggo so it'll take a couple of seconds, but it will load in that picture absolutely fine. So there we go, there's Thor. And that's pretty much everything I wanted to demonstrate in this lesson.

It's been a nice, quick demo lesson. All we've done is create a new group called Developers. We've added Sally to this Developers group, and we've removed the Manage Policy giving access to S3 from Sally directly, and added it to the Developers group that she's now a member of.

and you'll note that no matter whether the policy is attached to Sally directly or attached to a group that Sally is a member of, she still gets those permissions. And that's everything that I wanted to cover in this demo lesson, so before we finish up, let's just tidy our account up. So what we need to do is go to developers and then detach this managed policy from the developers group.

So detach it, then go to groups and just delete that developers group because it wasn't created as part of the CloudFormation template. And then as the IAM admin user, open up the S3 console. And we need to empty both of these buckets.

So select CatPix, click on Empty. You'll need to type or copy and paste 'Permanently Delete' into that box and confirm the deletion. Then click Exit.

Then select the AnimalPix bucket and do the same process. Copy and paste 'Permanently Delete'. and then confirm by clicking on empty and then exit.

Now we've done that, we should have no problems by opening up CloudFormation and selecting the IAM stack and then hitting delete. And again, note if you do have any errors deleting this stack then just go into the stack, select events and see what the status reason is for any of those deletion problems. And it should be fairly obvious if it can't delete the stack because it can't delete one or more resources and it will give you the reason why.

That being said, at this point, assume the stack deletions worked successfully, we've cleaned up our account. So that's everything I wanted to cover in this demo lesson. Go ahead, complete this video, and when you're ready, I'll see you in the next lesson.

