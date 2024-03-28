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

## iam-roles-the-tech

Welcome back. Over the next two lessons, I'll be covering a topic which is usually one of the most difficult identity-related topics in AWS to understand, and that's IAM roles. In this lesson, I'll step through how roles work, their architecture, and how you technically use a role.

In the following lesson, I'll compare roles to IAM users and go into a little bit more detail on when you generally use a role, so some good scenarios which fit using an IAM role. My recommendation is that you watch both these lessons, back to back, in order to fully understand IAM roles. So let's get started.

A role is one type of identity which exists inside an AWS account. The other type, which we've already covered, are IAM users. Remember the term, principal, that I introduced in the previous few lessons?

This is a physical person, application, device, or process which wants to authenticate with AWS. And we defined or authentication as proving to AWS that you are who you say you are. And if you authenticate, and if you are authorized, you can then access one or more resources.

Now, I also previously mentioned that an IAM user is generally designed for situations where a single principal uses that IAM user. I've talked about the way that I decide if something should use an IAM user, is that if I can imagine a single thing, one person, or one application, who uses an identity, then generally under most circumstances, I'd select to use an IAM user. IAM roles are also identities but they're used much differently than IAM users.

A role is generally best suited to be used by an unknown number or multiple principals, not just the one. So this might be multiple AWS users inside the same AWS account, or it could be humans, applications, or services inside outside of your AWS account who make use of that role. If you can't identify the number of principals which use an identity, then it could be a candidate for an IAM role.

Or if you have more than 5,000 principals, because of the number limit for IAM users, it could also be a candidate for an IAM role. Roles are also something which is generally used on a temporary basis. Something becomes that role for a short period of time and then stops.

The role isn't something that represents you. A role is something which represents a level of access inside an AWS account. It's a thing that can be used, short term, by other identities.

These identities assume the role for a short time, they become that role, they use the permissions that that role has, and then they stop being that role. It's not like an IAM user, where you login and it's a representation of you, long term. With a role, you essentially borrow the permissions for a short period of time.

I want to make a point of stressing that distinction. If you're an external identity, a mobile application, maybe, and you assume a role inside my AWS account, then you become that role and you gain access to any access rights that that role has for a short time. You essentially become an identity in my account for a short period of time.

Now, this is the point where most people get a bit confused, and I was no different when I first learned about roles. What's the difference between logging into a user and assuming a role? In both cases, you get the access rights that that identity has.

Now, before we get to the end of this pair of lessons, so this one and the next, I think it's gonna make a little bit more sense, and definitely, as you go through the course and get some practical exposure to roles, I know it's gonna become second nature. IAM users can have identity permissions policies attached to them, either inline JSON, or via attached managed policies. We know now that these control what permissions the identity gets inside AWS.

So whether these policies are inline or managed, they're properly referred to as permissions policies, policies, which grant, so allow or deny, permissions to whatever they're associated with. IAM roles have two types of policies which can be attached: the trust policy and the permissions policy: The trust policy controls which identities can assume that role. With the onscreen example, identity A is allowed to assume the role because identity A is allowed in the trust policy.

Identity B is denied because that identity is not specified as being allowed to assume the role in the trust policy. Now, the trust policy can reference different things. It can reference identities in the same account, so other IAM users, other roles, and even AWS services such as EC2, and a trust policy can also reference identities in other AWS accounts.

As you'll learn later in the course, it can even allow anonymous usage of that role and other types of identities, such as Facebook, Twitter, and Google. If a role gets assumed by something which is allowed to assume it, then AWS generates temporary security credentials and these are made available to the identity which assumed the role. Temporary credentials are very much like access keys, which I covered earlier in the course, but instead of being long term, they're time-limited, so they only work for a certain period of time before they expire.

Once they expire, the identity will need to renew them by reassuming the role and at that point, new credentials are generated and given to the identity again, which assumed that role. Now, these temporary credentials will be able to access whatever AWS resources are specified within the permission's policy. Every time the temporary credentials are used, the access is checked against this permissions policy.

If you change the permissions policy, the permissions of those temporary credentials also change. Now, roles are real identities and, just like IAM users, roles can be referenced within resource policies. So if a role can access an S3 bucket because a resource policy allows it or because the role permissions policy allows it, then anything which successfully assumes the role can also access that resource.

Now, you'll get chance to use roles later in this section when we talk about AWS organizations. We're going to take all the AWS accounts that we've created so far and join them into a single organization, which is AWS's multi-account management product. Roles are used within AWS organizations to allow us to login to one account in the organization and access different accounts without having to login again.

So they become really useful when managing large number of accounts. Now, when you assume a role, temporary credentials are generated by an AWS service called STS, or the Secure Token Service, and this is the operation that's used to assume the role and get the credentials, so sts:AssumeRole. In this lesson, I focused on the technical aspect of roles, so mainly how they work.

I've talked about the trust policy, the permissions policy, and how, when you assume a role, you get temporary security credentials. In the next lesson, I want to step through some example scenarios of where roles are used and I hope by the end of that, you're gonna be clearer on when you should and shouldn't use roles. So go ahead, finish up this video, and when you're ready, you can join me in the next lesson.

## iam-when-to-use-iam-roles

Welcome back. In this lesson, I want to continue immediately from the last one by discussing when and where you might use IAM roles. By talking through some good scenarios for using roles, I want to make sure that you're comfortable with selecting these types of situations where you would choose to use an IAM role and where you wouldn't, because that's essential for a real world AWS usage and for answering exam questions correctly.

So let's get started. Now, one of the most common uses of roles within the same AWS account are for AWS services themselves. AWS services operate on your behalf and they need access rights to perform certain actions.

An example of this is AWS Lambda. Now, I know I haven't covered Lambda yet, but it's a function as a service product. What this means is that you give Lambda some code and create a Lambda function.

This function, when it runs, might do things like start and stop EC2 instances, or it might perform backups, or it might be running real time data processing. What it does exactly isn't all that relevant for this lesson. The key thing though, is a Lambda function, as with most AWS things, has no permissions by default.

A Lambda function is not an AWS identity. It's a component of a service, and so it needs some way of getting permissions to do things when it runs. And running a Lambda function is known as a function invocation or a function execution using Lambda terminology.

So anything that's not an AWS identity, this might be an application or a script running on a piece of compute hardware somewhere, you know now that you need to give that application or that script permissions on AWS using access keys. Rather than hard coding some access keys into your Lambda function, there's actually a better way. To provide these permissions, we can create an IAM role known as a Lambda execution role.

Now, this execution role has a trust policy which trusts the Lambda service. And this means that Lambda is allowed to assume that role whenever a function is executed. This role has a permissions policy which grants access to AWS products and services.

Now, when the function runs, it uses the sts:AssumeRole operation, and then the secure token service generates temporary security credentials and then the runtime environment that the Lambda function runs in can use these temporary credentials to access AWS resources based on whatever permissions the roles permissions policy has. So the code is running in a runtime environment, and it's the runtime environment that assumes the role. The runtime environment gets these temporary security credentials, and then the whole environment, which the code is running inside, can use these credentials to access AWS resources.

So why would you use a role for this? What makes this scenario perfect for using a role? Well, if we didn't use a role, you would need to hard-code permissions into the lamb function by explicitly providing access keys for that function to use, and where possible, you should avoid doing that, because A, it's a security risk and B, it causes problems if you ever need to change or rotate those access keys.

It's always better for AWS products and services, where possible to use a role, because when a role is assumed, it provides a temporary set of credentials with enough time to complete a task and then these are discarded. Now also, for a given Lambda function, you might have one copy running at once, zero copies, 50 copies, a hundred copies, or even more. Because you can't determine this number, because it's unknown, if you remember my rule that I talked about in the previous lesson, if you don't know the number of principles, if it's multiple, or if it's an uncertain number, then it suggests a role might be the most ideal identity to use.

In this case, it is the ideal way of providing Lambda with these credentials is to use a role and allow it to get these temporary credentials. It's always the preferred option when using AWS services to do something on your behalf, use a role, because you don't need to provide any static credentials. Okay, so let's move on to the next scenario.

Another situation where roles are useful are emergency or out of the usual situations. And here's a pretty familiar situation that you might find in a workplace. So this is Wayne, and Wayne works in a business's service desk team.

This team is given read-only access to a customer's AWS account so that they can keep an eye on performance. The idea is that anything more riskier than this read-only level of access is handled by a more senior technical team. We don't want to give Wayne's team long-term permissions to do anything more destructive than this read-only access, but there are always going to be situations which occur when we least want them, normally 3:00 a.m.

on a Sunday morning when a customer might call with an urgent issue where they need Wayne's help to maybe stop or start an instance, or maybe even terminate an EC2 instance and recreate it. So 99% of the time, Wayne and his team are happy with this read-only access, but there are situations when he needs more. And this is a break glass style situation, which is named after this.

The idea of break glass in the physical world is that there is a key for something behind glass. It might be a key for a room that a certain team don't normally have access to. Maybe it's a safe or a filing cabinet.

Whatever it is, the glass provides a barrier, meaning that when people break it, they really mean to break it. It's a confirmation step. So if you break a piece of glass to get a key to do something, there needs to be an intention behind it.

Anyone can break the glass and retrieve the key, but having the glass results in the action only happening when it's really needed. At other times, whatever the key is for remains locked. And you can also tell when it's been used and when it hasn't.

A role can perform the same thing inside an AWS account. Wayne can assume an emergency role when absolutely required. When he does, he'll gain additional permissions based on the role's permission policy.

For a short time, Wayne will, in effect, become the role. Now, this access will be logged and Wayne will know to only use the role under exceptional circumstances. Wayne's normal permissions can remain at read-only which protects him and the customer, but he can obtain more, if required when it's really needed.

So that's another situation where a role might be a great solution. Another scenario when roles come in handy is when you're adding AWS into an existing corporate environment. You might have an existing physical network and an existing provider of identities, known as an identity provider, that your staff use to log into various systems.

And for the sake of this example, let's just say that it's Microsoft Active Directory. In this scenario, you might want to offer your staff single sign-on known as SSO, allowing them to use their existing logins to access AWS. Or you might have upwards of 5,000 accounts.

Remember, there's the 5,000 IAM user limit. So for a corporate, with more than 5,000 staff, you can't offer each of them an IAM user. That is beyond the capabilities of IAM.

Roles are often used when you want to reuse your existing identities for use within AWS. Why? Because external accounts can't be used directly.

You can't access an S3 bucket directly using an Active Directory account. Remember this fact. External accounts or external identities cannot be used directly to access AWS resources.

You can't directly use Facebook, Twitter or Google identities to interact with AWS. There is a separate process which allows you to use these external identities, which I'll be talking about later in the course. Now, architecturally, how this works is you allow an IAM role inside your AWS account to be assumed by one of the external identities, which is in Active Directory, in this case.

When the role is assumed, temporary credentials are generated and these are used to access the resources. Now, there are ways that this is hidden behind the console UI so that it appears seamless, but that's what happens behind the scenes. I'll be covering this in much more detail later in the course when I talk about identity federation, but I wanted to introduce it here, because it is one of the major use cases for IAM roles.

Now, why roles are so important when an existing ID provider such as Active Directory is involved, is that, remember, there is this 5,000 IAM user limit in an account. So if your business has more than 5,000 accounts, then you can't simply create an IAM user for each of those accounts, even if you wanted to. 5,000 is a hard limit.

It can't be changed. Even if you could create more than 5,000 IAM users, would you actually want to manage 5,000 extra accounts? Using a role in this way, so giving permissions to an external identity provider and allowing external identities to assume this role is called ID Federation.

It means you have a small number of roles to manage and external identities can use these roles to access your AWS resources. Another common situation where you might use roles is if you're designing the architecture for a popular mobile application. Maybe it's a ride sharing application which has millions of users.

The application needs to store and retrieve data from a database product in AWS, such as DynamoDB. Now, I've already explained two very important but related concepts on the previous screen. Firstly, that when you interact with AWS resources, you need to use an AWS identity.

And then secondly, that there's this 5,000 IAM user limit per account. So designing an application with this many users which needs access to AWS resources, if you could only use IAM users or identities in AWS, it would be a problem because of this 5,000 user limit. It's a hard limit and it can't be raised.

Now, this is a problem which can be fixed with a process called Web Identity Federation, which uses IAM roles. Most mobile applications that you've used, you might have noticed they allow you to sign in using a web identity. This might be Twitter, Facebook, Google, and potentially many others.

Now, if we utilize this architecture for our web application, we can trust these identities and we can allow these identities to assume an IAM role. And this is based on that role's trust policy. So they can assume that role, gain access to temporary security credentials and use those credentials to access AWS resources, such as DynamoDB.

This is a form of Web Identity Federation, and I'll be covering it in much more detail later in the course. The use of roles in this situation has many advantages. First, there are no AWS credentials stored in the application, which makes it a much more preferred option from a security point of view.

If an application is exploited for whatever reason, there's no chance of credentials being leaked and it uses an IAM role, which you can directly control from your AWS account. Secondly, it makes use of existing accounts that your customers probably already have, so they don't need yet another account to access your service. And lastly, it can scale to hundreds of millions of users and beyond.

And it means you don't need to worry about the 5,000 user IAM limit. This is really important for the exam. There are very often question on how you can architect solutions which will work for mobile applications.

Using ID Federation, so using IAM roles is how you can accomplish that. And again, I'll be providing much more information on ID Federation later in the course. Now, one scenario I want to cover before we finish up this lesson, and that is cross-account access.

In an upcoming lesson, I'll be introducing AWS organizations and you will get to see this type of usage in practice. It's actually how we work in a multi-account environment. Picture the scenario that's on screen now.

Two AWS accounts, yours and a partner account. Now, let's say your partner organization offers an application which processes scientific data and they want you to store any data inside an S3 bucket that's in their account. Your account has thousands of identities and the partner IT team don't want to create IAM users in their account for all of your staff.

In this situation, the best approach is to use a role in the partner account. Your users can assume that role, get temporary security credentials and use those to upload objects. Because the IAM role in the partner account is an identity in that account, then using that role means that any objects that you upload to that bucket are owned by the partner account.

So it's a very simple way of handling permissions when operating between accounts. Now, roles can be used cross account to give access to individual resources like S3 in the onscreen example, or you can use roles to give access to a whole account. And you'll see this in the upcoming AWS organization demo lesson.

In that lesson, we're going to configure it so a role in all of the different AWS accounts that we'll be using for this course can be assumed from the general account. And it means you won't need to log in to all of these different AWS accounts. It makes multi-account management really simple.

Now, I hope by this point, you start to get a feel for when roles are used. Even if you're a little vague, you will learn more as you go through the course. For now, just a basic understanding is enough.

Roles are difficult to understand at first, so you're doing well, if you're anything but confused at this point. I promise you, as we go through the course, and you get more experience, it will become second nature. So at this point, that's everything I wanted to cover.

Thanks for watching. Go ahead and complete this video and when you're ready, join me in the next lesson.

## iam-service-linked-roles-and-passrole

Welcome to this lesson, where I'm going to very briefly talk about a special type of IAM role, and that's service-linked roles. Now, luckily there isn't a great deal of difference between service-linked roles and IAM roles. They're just used in a very specific set of situations.

So let's jump in and get started. So simply put, a service-linked role is an IAM role linked to a specific AWS service. They provide a set of permissions which is predefined by a service.

So they provide permissions that a single AWS service needs to interact with other AWS services on your behalf. Now, service-linked roles might be created by the service itself, or the service might allow you to create the role during the setup process of that service, or service-linked roles might also get created within IAM. Now, the key difference between service-linked roles and normal roles is that you can't delete a service-linked role until it's no longer required.

And that means that it's no longer used within that AWS service. So that's the one key difference. Now, in terms of permissions that you need to create a service-linked role, this is an example of a policy which allows you to create a service-linked role.

So you'll notice a few key elements of this. So in terms of the top statement, it's an allow statement. The action is iam:CreateServiceLinkedRole.

And then for resource, it has this SERVICE-NAME.amazonaws.com. Now, the important thing here is do not try to guess this because different services express this in different ways, the formatting is different, and you're not going to be able to guess this by knowing the name of the service. I've included a link which contains an overview of these attached to this lesson.

But the key thing is the format can differ, and it is case-sensitive. So when you're creating this type of policy to give somebody the ability to create service-linked roles, you have to be careful about making sure you do not guess this element of a statement. Now, another important consideration with service-linked roles is that of role separation.

So when I talk about role separation, I'm not using it in a technical sense. I'm talking about it in a job role sense. So role separation is where you might give one group of people the ability to create roles and another group of people the ability to use them.

So in this case, we might want to give Bob, who is one of our users, the ability to use a service-linked role with an AWS service. So that's using this architecture. So being able to take a service-linked role and assign it to a service.

And if you wanted to give Bob the ability to use a preexisting role with a service but not create that role or edit that role, then you'd need to provide Bob with the PassRole permissions. So this is an example. This allows Bob to pass an existing role into an AWS service.

It's an example of role separation. It means that Bob could configure a service with a role which is already being created by a member of the security team. He'd just need this ListRole and PassRole permissions on that specific role.

Now, this is the same type of architecture as when you use a pre-created role, for example with a CloudFormation stack. You might not have done this lesson yet, but by default, when you're creating a CloudFormation stack, CloudFormation uses the permissions of your identity to interact with AWS, which means not only do you need permissions to create a stack, but you also need permissions to create the resources that that stack creates. So that's the default method.

But what you can do is give, for example, a user Bob the ability to pass a role into CloudFormation. That role could have permissions which exceed those which Bob directly has. So a role that Bob uses could have the ability to create AWS resources where Bob does not.

So Bob might have access to create a stack and to pass in a role, but this role is what provides CloudFormation with the permissions it needs to interact with AWS. So PassRole is a method inside AWS which gives you the ability to implement role separation, and it's something which you can also use with service-linked roles. This is something I just wanted to reiterate so that you understand that passing a role is a very important AWS security architecture.

Now, that is everything I wanted to cover in this very brief lesson. It's really just an extension of what you've already learned about IAM roles, and it's something that you're going to be using in demo lessons elsewhere in the course. For now, I just want you to be aware of how service-linked roles are different than normal roles and how the PassRole architecture works.

But with that being said, that's everything I wanted to cover in this video. So go ahead and complete the video, and when you're ready, I look forward to you joining me in the next.

## iam-aws-organizations

Welcome to this lesson where I'll be introducing AWS Organizations. AWS Organizations is a product which allows larger businesses to manage multiple AWS accounts in a cost-effective way with little to no management overhead. Organizations is a product which has evolved a lot over the past few years, and it's worthwhile stepping through that evolution to help you understand all of the different features.

Now we've got a lot to cover, so let's jump in and get started. Without AWS Organizations, many large businesses would face a situation where they need to manage many AWS accounts. Now, there are four onscreen in this example, but I've worked with some larger enterprises with hundreds of accounts and heard of ones with even more.

Without AWS Organizations, these accounts would each have their own pool of IAM users as well as separate payment methods, and beyond 5 to 10 accounts, this becomes unwieldy very quickly. AWS Organizations is a simple product to understand. First, you take a single AWS account which I'll refer to as a standard AWS account from now on.

So a standard AWS account is an AWS account which is not within an organization. So with this standard AWS account, you create an AWS Organization. And it's important that you understand the organization isn't created in this account; you're just using the account to create the organization.

This standard AWS account that you created the organization with then becomes the Management Account for the organization. Now the Management Account used to be called the Master Account. So if you hear either of these terms, so Management Account or Master Account, just know that it means the same thing.

Now this is a key point to understand with regards to AWS Organizations because the Management Account is special for two reasons, and I'll explain both of those in this lesson. For now, I'll add a crown to this account to indicate that it's the Management Account and help you distinguish between it and any other AWS accounts. Now using this Management Account, you can invite other exist standard AWS accounts into the organization.

Because these are existing accounts, they'll need to approve the invites to join the organization. And assuming they do, those Standard Accounts will then become part of that AWS Organization. When standard AWS account join an AWS Organization, then they change from being Standard Accounts to being Member Accounts of that organization.

Organizations have one and only one Management or Master Account and then they have zero or more Member Accounts. You can create a structure of AWS accounts within an organization, and this is useful if you have lots of accounts and you need to group them by things such as business units, function, or even development stage of an application. Now the structure within AWS Organizations is hierarchical, so it's an inverted tree.

At the top of this tree is the root container of the organization. Now this is just a container for AWS accounts which exists at the top of this organizational structure. Don't confuse this with the Account Root User which is the admin user of an AWS account.

This root, so the organizational root, is just a container within an AWS Organization, which can contain AWS accounts, and this means Member Accounts or the Management Account. As well as containing accounts, the organizational root can also contain other containers, and these are known as organizational units or OUs. And these organizational units can contain AWS accounts or Member Accounts or the Management Account or they can contain other organizational units so you can build a complex nested AWS account structure within Organizations.

You have the root container at the top and then potentially multiple levels of organizational units. Now, again, please don't confuse the organizational root that we're talking about now with the AWS Account Root User. The AWS Account Root User is something specific to every AWS account that you create.

It's something which you can log into and have full permissions over that specific AWS account. The root of an AWS Organization is just a container for AWS accounts and organizational units. So the organizational root is just the top of this tree within AWS Organizations.

It's the top level of this hierarchical structure which allows you to manage AWS accounts within Organizations. One important feature of AWS Organizations which you need to be aware of is consolidated billing. With the example that's onscreen now, there are four AWS accounts, each with their own billing information.

Now because these have been added to an AWS Organization, this changes. The individual billings methods are removed for the Member Accounts within the organization. The Member Accounts instead pass their billing through to the Management Account of the organization.

Now you might see this referred to in the context of consolidated billing as the Payer Account, and the Payer Account is just the AWS account that contains the payment method for the organization. So at this point, if you see Master Account, Management Account, or Payer Account, know that within AWS Organization, they all refer to the same thing, the account that was used to create the organization and the account that contains the payment method for all of the accounts within the AWS Organization. Now using consolidated billing within an AWS Organization means that you get a single monthly bill which is contained within the Management Account.

And this single monthly bill covers the Management Account and all of the Member Accounts of the organization. So one bill contains all of the billable usage of all of the accounts within the AWS Organization. For larger businesses, this removes a significant amount of financial admin overhead.

This alone would be worth creating an organization for most larger enterprises. But it gets better. With AWS, certain services get cheaper the more usage you have, and for certain services you can pay in advance in exchange for cheaper rates.

When using Organizations, these benefits are pooled, and so the organization can benefit as a whole for the spending of each of the AWS accounts within the organization. AWS Organizations also feature a service called Service Control Policies, or SCPs, and this lets you actually restrict what AWS accounts within the organization can do. Now these are important, and so I'm going to be covering them in their own dedicated lesson, which is coming up soon.

But I wanted to mention it at this point as a feature of AWS Organizations. Now, before we go through a demo where we're going to be creating at AWS Organization and creating the final account structure, which we'll be using throughout this course, I wanted to cover two other concepts of Organizations. As well as being able to invite existing accounts into an organization, you can all also create new accounts directly within it.

All you need is a valid unique email address for this new account which you want to create within the organization, and AWS will handle the rest. Adding accounts in this way, so creating them directly within the organization, means that there isn't an invite process. Remember, for existing accounts, you need to invite them, and then that account needs to accept it.

If you create accounts directly within the organization, then this is a single step. You just create the account in the organization. Now using an AWS Organization changes what is best practice in terms of user logins and permissions.

With Organizations, you don't need to have IAM Users inside every single AWS account. Instead, IAM roles can be used to allow IAM Users to access other AWS accounts, and we're going to implement this in the following demo lesson. So best practice is that you have a single account which is used to log into, and I've shown this on this diagram as the Management Account of the organization.

Now larger enterprises will often keep the Management Account of the organization clean and have a separate account dedicated to handle logins. Both of these are fine, but just be aware that the architectural pattern is to have a single AWS account which contains all of the identities which are logged into. Larger enterprises might also have their own existing identity system, and they might want to use those existing identities and use Identity Federation to access this single identity account.

So you can either have your own internal AWS identities using IAM or you can configure AWS to allow Identity Federation so your on-premises identities can be used to access this designated login account. From then, we can use this account with these identities and use a feature called role switch, and we can role switch from this account into other Member Accounts of the organization. And behind the scenes, this actually assumes roles in these other AWS account.

And this can be done from the console UI, and so a lot of the technical aspects are hidden, but I want you to know how this works. So essentially, you either log in directly to this login account or you use Identity Federation. Then once we log into this account, we can role switch into the other accounts within the organization, And this is actually a way that the user interface presents, assuming a role within the other account.

So essentially, you either log in directly to this login account using IAM identities or you use Identity Federation to gain access to this particular login account, and then you role switch from this login account into other accounts within the organization. And behind the scenes, this is essentially assuming a role which is inside these other AWS accounts. And this is how you effectively manage identities using AWS Organizations.

Now I'll be talking about this in-depth as we move through the course. And the next lesson is a demo where you're going to implement this yourself and create the final AWS account structure you'll be using for the remainder of the course. Okay, so at this point, it's time for a demo.

And as I just mentioned, you're going to be creating the account structure you'll be using for the remainder of the course. At the start of the course, I demoed the process of creating AWS accounts. You created some AWS accounts you'll be using for the course.

You should have created a general AWS account and a production AWS account. In the next lesson, I'm going to be step you through how to create an AWS Organization using this general account. So we'll be creating the organization, and this general account will become the Management Account for the AWS Organization.

Then you're going to invite the existing production account into the organization, and this will become a Member Account of the organization. And then finally, you're going to create a brand new account within the organization, which is going to be the Development Account. Now I can't wait.

It's going to be fun and it's going to be really useful for the exam. So go ahead and finish this video. And when you're ready, I look forward to your joining me in the next lesson, which is going to be a demo.

## iam-demo-aws-organizations

Welcome back and in this demo lesson you're going to create the AWS account structure which you'll be using for the remainder of the course. Now at this point what we need to do is to log in to the general AWS account. So I'm currently logged in as the IAM admin user of my general AWS account and I've got the Northern Virginia region selected.

You're also going to need either two different web browsers or a web browser such as Firefox which is capable of using different sessions because we're going to be logged in to multiple AWS accounts at once. So the first thing that we're going to need to do is create the AWS organization. So because I'm logged in to the general AWS account I'm logged into an account which is a standard AWS account.

It isn't part of an AWS organization and so it's not a management account and it's not a member account. So what we need to do is to move it to the AWS organizations part of the console and create the organization. So let's do that.

So to do that go to find services and just start typing organizations and then click to move to the AWS organizations console. Once we're here go ahead and click on create organization. This is going to start the process of creating this AWS organization and as part of that it will convert this standard account to be the management account of the organization.

So go ahead and click on create organization and that will complete the process. So now we have the AWS organization and within it this one single AWS account so the general account has now been converted to the management account of this AWS organization. Now you might see a message saying that we've sent a verification email to this email address so this is the email address that's associated with the general AWS account which is now the management account of the organization and you'll need to click the link within this email to verify this address so you can continue using AWS organization.

So if you do have that notification on screen, go ahead and verify that email before continuing. If you don't have a notification, you're good to continue. Now at this point, what I'll need you to do is to open a brand new web browser or a web browser such as Firefox, which is capable of handling different sessions.

And I'll want you to log in to the production AWS account. So just be careful at this point. You need to make sure that this is a completely separate session and if in doubt use a completely different web browser because we need to maintain logins to both this management account and the production account.

So I'm going to go ahead and log in to the IAM admin user of the production AWS account. So now I'm logged into the production AWS account with this separate browser session so either you'll use a separate browser session or a completely different browser. At this point you're going to need the account ID for the production AWS account.

So click on the account dropdown and make sure that you copy this account ID into your clipboard. And it needs to be the account ID for the production AWS account. Once you've got that, go back to the browser or the session where you have the general account open.

So this is now the management account of the AWS organization. And we're going to invite the production AWS account into this organization. So currently the only account which is a member of this organization is the general account which is the management account of the organization.

We're going to invite the production account. So go ahead and click on add account. We're going to be inviting an existing account into this organization.

So click on invite account and you'll need to provide either the email address of the production account which you used while signing up or the account ID. And I've just demonstrated getting the account ID of the production account from this dropdown, so I'm going to enter this account ID into the box. Now if you're inviting an account which you administer, you don't have to put any notes.

But optionally, if you're inviting an account that's administered by somebody else, then it might be nice to type a message. In either case, once you've entered the email or the account ID, just scroll down and click on 'Send Invitation'. Now depending on your specific AWS account it is possible that you might receive an error message at this point telling you there are too many accounts within the organisation.

Different AWS accounts are created with different account quotas and so it's possible that you might get an error at this point. If you do you just need to log a support request asking for an increase in the number of AWS accounts which can be part of an AWS organisation. If you don't get an error message, then this invite process has started.

What we need to do now is to accept this invite from the production AWS account. So let's go back to this other tab and move across to the organizations console. So in the find services box, just type organizations and then click to move to the organizations console and towards the middle left, you should see this heading saying invitations.

If you just click on invitations, you'll be able to see an overview of all of the invitations which apply to this production AWS account. So this is the invite that we just sent from the general AWS account, which is the management account for our organization. So go ahead and click on accept and this completes the process of joining the organization.

So now the production account is a member of the AWS organization and we can verify that by returning to the tab where we logged in to the general AWS account, which is now the management account for this organization and just hit refresh. And now we should see two AWS accounts, the general account and the production account. So next I'm going to demonstrate how we can roll switch into this production AWS account, which is now a member of the organization.

So when you add an account to an organization, you can do it in two ways. can either invite an existing account or you can create an account within the organization. If you create an account within the organization, then a role is created within that account, which can be role switched into by other accounts within the organization.

If you invite an existing AWS account into the organization, then you need to manually add this role. And that's what we're going to do next. So this only applies if you're inviting existing accounts into the organization.

So what we're going to do is to move across to the browser or session where you're logged in to the production AWS account, click in the services search box at the top of the screen and type IAM and then we're going to move to the IAM console because this is where we create IAM roles. So move to IAM and then go to roles and we're going to create a role which can be from the general account. So click on create role, and the type of trusted entity is going to be another AWS account.

So select this box, and then for the account ID, we need the account ID of the general AWS account, which is now the management account of the organization. So move back to the browser or the session where you're open in the general account, and you need to copy down the account ID of the general AWS account. Make sure you get the general account, not the production account.

Once you've got that in your clipboard, we're going to paste this into this account ID box, and this is going to mean that the general AWS account is trusted to assume this role. So enter that into the box and click next. This role is going to have administrator access attached because it's going to be an administration role.

So look in the policies and look for administrator access, check that box, Scroll to the bottom and click on next to move to the next screen. And we need to give this role a name. So this role is going to be used when we're logged into the general account and we want to role switch into the production account to perform administrative functions.

Now we're going to give this role a very specific name. It's a standard name. This is the same name which AWS use when they automatically create the equivalent role within accounts that you create within the organization.

So I like to keep things consistent. So the name of the role is going to be organization account access role with uppercase O A A and R and note that it's the U S spelling of organization. So make sure you use a Z rather than an S once you've done that, go ahead and click on create role.

Now, if we look inside this role, so select the role and then click on trust relationships, you'll be able to see that this role trusts the account ID of your general AWS account. And this will be different for you. This will be the account ID of your general AWS account.

And this is what will allow identities within the general account to assume this role. So the account that's now the management account of the AWS organization. So now I'm going to show you how we can use this role to switch from the general account to the production account.

And we're going to need to copy down the account ID for the production AWS account because we're going to switch in to that account using role switch. So copy down the account ID of the production AWS account. You'll need to make sure you're logged into the IAM admin user of the general account.

This will only work with IAM identities. Before we do role switch just move back to the main part of the AWS console. So we've got the main console selected and then click on the account drop-down and then select switch roles.

Now this starts the process of role switching from the general account to the production AWS account. So to start that, go ahead and click on switch role. We need to provide the account ID of the production AWS account.

So that should be in your clipboard. Just go ahead and paste that in. Next, we need to provide the name of the role within the production account, which we want to switch to.

This is the role that you just created. So the role, which is called organization account access role with uppercase O A A and R and the US spelling of organization. So we need to enter that into the role name.

Now we need to give this role switch a display name. So the way that this works is that when you initially do a switch role, it's going to create an entry within the console UI and this is stored in your browser. So this is nothing to do with AWS.

This is just creating a shortcut. so you can easily access this in the future. So you need to give it a suitable display name.

I suggest 'Prod' for production. You also need to pick a colour and I try to be consistent with this. So if I'm creating a role switch which is going into a production AWS account, then I pick red so I know that this is an important account.

So select red, make sure it's called 'Prod', double check the spelling of the role name and make sure this account ID is for the production AWS account and then click on switch role. Now at this point this is role switching into the production AWS account. It's actually using the assume role API call to assume the role that you just created within the production AWS account and you can see that we've switched role because at the top here it's got the color red and it has the display name of prod so this means that we've switched into this switch role shortcut that we just created.

Now let's go back to the general account by clicking on switch back. So this now takes us back into the general AWS account and if we click on the account drop down again we can see a role history section. Now when we were just creating this switch role I mentioned how it creates a shortcut and this is that shortcut.

So now if I click on prod again it's going to automatically do a switch roles into the organization account access role within the production account so by clicking this we go back to the production AWS account. What happens behind the scenes is that we assume the role we're provided with temporary credentials that that role grants when we assume it and then the console UI automatically handles this move across to the production account so now we're interacting with the production account using the temporary credentials that we gained by assuming the role. Role switching makes it easy to administer multiple AWS accounts within an AWS organization.

Currently we only have the one but the process would be the same if we had hundreds of AWS accounts. Now let's go back to the general account by clicking on switchback because now we're going to create the development AWS account within our organization. This is going to the third and final account that's a member of this organization and this will complete the account structure you'll be using throughout the course.

This point you can close down the browser window which you have open to the production AWS account or the separate tab because we won't be needing that anymore. Next we're going to create a brand new account within this organization. So go back to the AWS organizations console, click on add account.

This time though we're going to create an account within the organization. So click on create account. You need to give the account a name.

And so I'm going to keep the same naming structure that I've used so far only using development instead of general or production, and you should do the same. You also need to provide a unique email address, which is going to be associated with this development AWS account. So every AWS account, even those created within an organization, they all need to have unique email addresses.

Now, keep in mind the trick that I talked about at the start of the course, where you can create an unlimited number of unique email addresses for one single Gmail account. But each account does need a unique email address. Now, for the accounts that I've previously created as part of this structure, I've used my name, so Adrian and then plus and then training AWS and then the name of the account.

So I'm going to use that same structure here. So Adrian Plus and then Training AWS Development, and you should use the same structure of emails you've been using so far, but use one for the Development AWS account. In this box, you can provide the name of the role which will be created within this brand new AWS account.

Now this is the same role that you just created manually for the production account, But this is created automatically by AWS because when you create an account within an organization, the only method that you have to access this account is by switching role into that account. So we need to give the role a name. Now the default is organization account access role with uppercase O, A, A and R with the US spelling, so with a Z, and we're going to use that default.

And then I'll scroll down and click on create and you should do the same. and at this point it will create this development account within the AWS organization. Now again, if you get an error message at this point saying you've got too many accounts within the organization, then you might have to lodge a support request to have the limit of the number of accounts within an organization increased.

In my case, I haven't had that error and the development account is being created within the organization and that can take a few minutes. But if we refresh this after a few minutes, we should see this populated with values. There we go, we can see the development account has been created and it's been allocated with its own individual account ID.

Now I want you to go ahead and copy this account ID into your clipboard because we're going to go ahead and create a new entry in this switch role dialogue to allow us to connect to the development AWS account which is now a member of this organization. So click on the account dropdown and select switch roles. We're going to follow the same process that we did for the production AWS account.

First, we'll need to enter the account ID for this new development account that we've just created. You'll need to enter the role name. So assuming you picked all of the defaults, this should be organization account access role with uppercase O A A and R and the U S spelling.

So with a Z for the display name this time we're going to put dev for development and rather than picking red my Standard for any development accounts is to pick yellow So this indicates to us that we should still be careful, but we can be less careful than for a production account Which is in red So once you've entered all that information just go ahead and click on switch role and this will follow the same Process as before so now it's switched role into the development AWS account So if we move to the main AWS console, this is now a completely new account, the development account. We can click on the dropdown and see that we've got a new entry in the role history. We could switch back to general.

We could move across to the production AWS account. We can move directly to the development account. So we don't have to go back to the general account before moving to the development account.

We can just use these role switch shortcuts to move directly between accounts. So now that we're in the development account, if we just go to the IAM console, I want to point out that even though we didn't directly create it, by creating a brand new account within this organisation, AWS has created this organisation account access role on our behalf. And if we click on it and then go to Trust Relationships, this role trusts the same general account ID.

So this is the general or the management account of the organization. So by creating this account directly within the organization, AWS has created this role on our behalf that we can switch into from the general AWS account. So at this point, that's everything that I wanted to cover in this demo lesson.

Now you have three different AWS accounts. You have the general AWS account, which was originally a standard AWS account, which is now the management account of this AWS organization that we've just created. In addition to this management account, we've invited the production AWS account into this organization, and we've manually created the role, allowing us to switch role into the production account.

And then finally, we've created a brand new account directly within the organization, which is the development account and AWS automatically on our behalf has created the role within the development account that we can switch role into. So now we have these three AWS accounts. We have the management account, the production account and the development account, and that's everything which I wanted you to do in this demo lesson.

So go ahead and complete this video. And when you're ready, I'll look forward to you joining me in the next.

## iam-service-control-policies

Welcome back, and in this lesson, I'll be talking about service control policies or SCPs. Now, SCPs are a feature of AWS organizations which can be used to restrict AWS accounts. They're an essential feature to understand if you are involved in the design and implementation of larger AWS platforms.

Now, we've got a lot to cover, so let's jump in and get started. At this point, this is what our AWS account setup looks like. We've created an organization for Animals4life, and inside it, we have the general account, which from now on I'll be referring to as the management account, and then two member accounts, so production, which we'll call prod and development which we'll be calling dev.

All of these AWS accounts are within the root container of the organization. That's to say they aren't inside any organizational units. In the next demo lesson, we're going to be adding organizational units, one for production and one for development and we'll be putting the member accounts inside their respective organizational units.

Now, let's talk about service control policies. The concept of a service control policy is simply enough. It's a policy document, so a JSON document, and these service control policies can be attached to the organization as a whole by attaching them to the root container, or they can be attached to one or more organizational units.

And lastly, they can even be attached to individual AWS accounts. Service control policies inherit down the organization tree. So this means if they're attached to the organization as a whole, so the root container of the organization, then they affect all of the accounts inside the organization.

If they're attached to an organizational unit, then they impact all accounts directly inside that organizational unit, as well as all accounts within OUs inside that organizational unit. So if you have nested organizational units, then by attaching them to one OU, they affect that OU and everything below it. If you attach service control policies to one or more accounts, then they just directly affect those accounts that they're attached to.

Now, I mentioned in an earlier lesson that the management account of an organization is special. One of the reasons it's special is that even if the management account has service control policies attached, either directly via an organizational unit, or on the root container of the organization itself, then the management account is never affected by service control policies. Now, this can be both beneficial and it can be a limitation, but as a minimum, you need to be aware of it as a security practice because the management account can't be restricted using service control policies, then generally in production, I avoid using the management account for any AWS resources.

It's the only AWS account within AWS organizations which can't be restricted using service control policies. As a takeaway, just remember that the management account is special and it's unaffected by any service control policies, which are attached to that account either directly or indirectly. Now, service control policies are account permissions boundaries.

And what I mean by that is they limit what the AWS account can do, including the Account Root User within that account. Now, I talked earlier in the course about how you can't restrict an Account Root User. And that is true.

You can't directly restrict what the Account Root User of an AWS account can do. The Account Root User always has full permissions over that entire AWS account, but with a service control policy, you're actually restricting what the account itself can do, specifically any identities within that account. And so you're indirectly restricting the Account Root User because you're reducing the allowed permissions on the account, you're also reducing what the effective permissions on the Account Root User are.

So this is a really fine detail to understand. You can never restrict the Account Root User. It will always have a 100% access to the account, but if you restrict the account, then in effect, you're also restricting the Account Root User.

Now, you might apply a service control policy to prevent any usage of that account outside a known region, for example, us-east-1. You might also apply a service control policy which only allows a certain size of EC2 instance to be used within the account. Service control policies are a really powerful feature for any larger, more complex AWS deployments.

The really critical thing though, to understand about service control policies is they don't grant any permissions. Service control policies are just a boundary. They define the limit of what is and isn't allowed within the account, but they don't grant permissions.

You still need to give identities within that AWS account, permissions to AWS resources, but any SCPs will limit the permissions that can be assigned to individual identities. Now, you can use service control policies in two ways. You can block by default, and allow certain services, which is an allow list.

Or you can allow by default and block access to certain services, which is a deny list. Now, the default is a deny list. When you enable SCPs on your organization, AWS apply a default policy, which is called full AWS access.

And this is applied to the organization and all OUs within that organization. This policy means that in the default implementation, service control policies have no effect since nothing is restricted. As a reminder, service control policies don't grant permissions, but when SCPs are enabled, there is an implicit default deny, just like IAM policies.

If you had no initial allow, then everything would be denied. So the default is this full access policy, which essentially means no restrictions. It has the effect of making SCPs a deny list architecture, so you need to add any restrictions that you want to any AWS accounts within the organization.

An example is that you could add another policy, such as this one, called DenyS3. And this adds a deny policy for the entire S3 set of API operations, effectively denying S3. You need to remember that SCPs don't actually grant any access rights, but they establish which permissions can be granted in an account.

So the same priority rules apply. Deny, allow, deny. Anything explicitly allowed in an SCP is a service which can have access granted to identities within that account, unless there's an explicit deny within an SCP, then a service cannot be granted.

Explicit deny always wins. And in the absence of either, if we didn't have this full AWS access policy in place, then there would be an implicit deny, which blocks access to everything. Now, the benefit to using deny lists is that because your foundation is to allow wild card access, so all actions on all resources, as AWS extends the amounts of products and services which are available inside the platform, this allow list constantly expands to cover those services, so it's fairly low admin overhead.

You simply need to add any services which you want to deny access to via an explicit deny. Now, in certain situations, you might need to be more conscious about usage in your accounts, and that's where you'd use allow lists. To implement allow lists, it's a two-part architecture.

One part of it is to remove the AWS full access policy. And this means that only the implicit default deny is in place and active and then you would need to add any services which you want to allow into a new policy. In this case, S3 and EC2.

So in this architecture, we wouldn't have this full AWS access. We would be explicitly allowing S3 and EC2 access. So no matter what identity permissions identities in this account are provided with, they would only ever be allowed to access S3 and EC2.

Now, this is more secure because you have to explicitly say which services can be allowed access for users in those accounts, but it's much easier to make a mistake and block access to services, which you didn't intend to. It's also much more admin overhead because you have to add services as your business requirements dictate. You can't simply have access to everything and deny services you don't want access to.

With this type of architecture, you have to explicitly add each and every service which you want identities within the account to be able to access. Generally, I would normally suggest using a deny list architecture, because simply put, it's much lower admin overhead. Now, before we go into a demo, I want to visually show you how SCPs affect permissions.

This is visually how SCPs impact permissions within an AWS account. In the left orange circle, this represents the different services that have been granted access to identities in an account using identity policies. On the right in red, this represents which services an SCP allows access to.

So the SCP states that the three services in the middle and the service on the right are allowed access as far as the SCP is concerned, and the identity policies which were applied to identities within the account, so the orange circle on the left, grant access to four different services, the three in the middle and the one on the left. Now, only permissions which are allowed within identity policies in the account and are allowed by a service control policy are actually active. On the right, this access permission has no effect, because while it's allowed within an SCP, an SCP doesn't grant access to anything, it just controls what can and can't be allowed by identity policies within that account.

Because no identity policy allows access to this resource, then it has no effect. On the left, this particular access permission is allowed within an identity policy, but it's not effectively allowed because it's not allowed within an SCP. So only things which are involved, the identity policy and an SCP are actually allowed.

In this case, this particular access permission on the left has no effect because it's not within a service control policy, so it's denied. Now, at an associate level, this is what you need to know for the exam. It's just simply understanding that your effective permissions for identities within an account are the overlap between any identity policies and any applicable SCPs.

Now, this is going to make more sense if you experience it with a demo, so this is what we're going to do next. Now that you've set up the AWS organization for the Animals4life business, it's time to put some of this into action. So I'm going to finish this lesson here and then in the next lesson which is a demo, we're going to continue with the practical part of implementing SCPs.

So go ahead and complete this video and when you're ready, I'll look forward to you joining me in the next.

## iam-demo-using-service-control-policies

Welcome back and in this demo lesson I want to give you some experience of working with service control policies or SCPs. At this point you've created the AWS account structure which you'll be using for the remainder of the course. You've made an AWS organization and the general account which created that AWS organization became the management account of the organization.

and in addition to that you invited the production AWS account into the organization and created the development account within the organization. Now in this demo lesson I want to show you how you can use service control policies to restrict what identities within an AWS account can do and this is a feature which comes part of AWS organizations. Now before we do that I want to tidy up the AWS organization So make sure that you're logged into the general account, so the management account of the organization, and then just move to the organization's console.

You can either type that in the 'Find Services' box, or it should be available in 'Recently Used Services'. Now, as I talked about in the previous lessons, AWS Organizations includes the ability to organize accounts with a hierarchical structure, and currently there's only the root container of the organization. Now to create a hierarchical structure we need to create some organizational units and we're going to create a development organizational unit and a production organizational unit.

So to do that select the root container at the top of the organizational structure then click actions and create new. And we're going to call the organizational unit for production 'prod' so type prod into name of organizational unit Scroll down and click on 'Create Organizational Unit' and then do the same for 'Development' so make sure 'Route' is still selected click on 'Actions' and then 'Create New' Under 'Name' just type 'dev' and then scroll down and click on 'Create Organizational Unit' Now we're going to move our AWS accounts into these relevant organizational units so currently the 'Development', 'Production' and 'General' accounts are all contained in this 'Route' container So this is the topmost point of our hierarchical structure inside our organisation. So to move accounts we need to select them and then move them into each of the relevant organisational units.

So go ahead and select the Production AWS account, then click on Actions and then Move. Once you're at this dialogue just select the Production Organisational Unit and click on Move. And this account will be moved inside this organisational unit.

And we'll do the same for the development account. So select the development AWS account and again click on actions and then move. Select the dev OU and click on move.

And now we've got these two AWS accounts inside the relevant organizational units. And if we select each of the organizational units in turn, so prod, and we can see that it's got one account inside the production OU. And then if we select "Dev", we can see that it's got the development AWS account inside of this organizational unit.

So that's a simple hierarchical structure that we've created inside this organization. And the general account, so the management account of the organization, is currently within the root container of the organizational structure. So now that we've done that, to prepare for the demo part of this lesson where we're looking at service control policies, I want you to move back to the AWS console.

So just click on AWS, and then click on the account dropdown, and we're going to switch roles into the production AWS account. So select 'Prod' from 'Role History'. Now once we're here, we're going to create an S3 bucket.

So type S3 into the 'Find Services' box, or alternatively, it might be within the recently used services. But either way, move to the S3 console. So once you're at the S3 console, go ahead and click on 'Create Bucket' and for bucket name, I just want you to call it 'CatPics' so C-A-T-P-I-C-S and then pick a random number at the end remember, S3 bucket names need to be globally unique so you'll need to pick a random set of numbers different than what I use and every other student uses so I'm going to pick 1, and then lots of 3s, and then 7 and make sure that you pick the US East 1 region for this bucket Once you've set all those options, just scroll all the way down to the bottom and then select "Create Bucket".

Now once you've created the bucket, just go inside the bucket and we're going to upload some files into this bucket. So follow the same process that we've used before, click on "Add Files" and then attached to this lesson is a link to a cat picture that you'll need to download to your local machine and then upload that cat picture to this S3 bucket. So go ahead and download the image, locate it, go ahead and select that and click on open.

And then click on upload to upload that picture into this S3 bucket. Wait for that to finish and click on close. Now this is a picture of Samson so if you click on this and then click on open, you'll see there Samson looks pretty sleepy.

He does tend to sleep a lot but he's a pretty amazing cat. But what you're illustrating is that you can currently access the Samson.jpg object. and you're currently operating within the production AWS account.

Now crucially the way that you're doing that is you've assumed an IAM role. By switching role into the production account what you've actually done is you've assumed the role which is called organization account access role. And if we open this role up and look at the permissions it currently has the administrator access managed policy attached to this role.

So you're operating inside the production account with the permissions that you've gained by assuming this role and their administrator permissions. So there should be no confusion why you can create an S3 bucket, upload an object and access that object because you have full administrator access which has been granted by attaching this managed policy to the I am role which you're currently assuming as part of switching role into the production account. What we're going to demonstrate is how this can be restricted by using service control policies So at this point move back to the main AWS console Click on the account drop-down and then click switch back to move back to the general AWS account Once we're back inside this account at the main AWS console either type AWS Organizations or select it from the recently visited services now once you're here click on policies And you'll see that currently that most of these options are currently disabled.

So service control policies, tag policies, AI services, opt-out policies and backup policies. They're all disabled. Now I'll be talking about what all of these mean as you move throughout the course, but at this point I want you to click on service control policies and then click on enable service control policies and this will enable the functionality within the AWS Organization now what it's actually done as part of this is to add this full AWS access policy onto the entire Organization so if we click on full AWS access and then scroll down This is the policy which is currently associated with everything within the organization So this has the effect of adding no restrictions on to what any of the accounts within the organization can do So in effect by enabling service control policies the first policy which is applied does nothing it simply Maintains the existing functionality so all AWS accounts within the organization maintain full access to all the services provided by AWS so click on service control policies at the top to move back to the overview of all of the various SCPs that we have available within the organization What we're going to do is create our own service control policy.

Now linked to this lesson is a file called DenyS3.json and this is an example of a new service control policy that we're going to apply. So go ahead and download that file and open it up in a code editor. Now this is a service control policy with two statements.

The first statement is an allow statement. So the effect is allow, action is star which is a wild card and resource is also the star wildcard. Now this replicates the full AWS access service control policy that is applied by default so this allows access to all products and services within an AWS account.

But this one also has a second statement which is a deny statement so this denies any S3 colon star actions on on any AWS resource. So the effect of this is to deny access to S3. Now service control policies follow the same deny, allow, deny logic as identity policies within AWS and so this explicit deny overrules this explicit allow but only for S3 colon star.

So the effect of this is that if this service control policy is applied, then we'll maintain access to all AWS except S3. So we're going to apply this to the production AWS account and observe the results. So to do that, we need to copy all of this into our clipboard and then move back to the AWS console.

Once you're there, make sure you're in the policy section of the console and then service control policies and then go ahead and create a policy. Scroll down and then select all of the existing JSON that's inside this policy box and then just delete it and then paste in what you've just copied into your clipboard. So just as a reminder this denies access to any S3 actions on all resources and then allows access to all of the AWS account.

And then using the deny allow deny rule which by now you should be at least familiar with This means that S3 will be denied and access to all other AWS services will be available. And then scroll up to the top and for policy name we're going to call this "Allow all except S3". Once you've put that in the policy name box then just scroll all the way down to the bottom and create the policy.

So now you have two service control policies, full AWS access, which allows access to every operation and then allow all except S3, which is the new service control policy we've just created. So now go ahead and click on AWS accounts on the menu on the left, and then click on the prod OU because we're going to apply this new service control policy to the production OU. And then click on the policies tab.

And then we're going to do two things. First, we're going to attach the new policy that we've created. So go ahead and click on attach in the applied policies box and then select allow all except S3 and then attach that policy.

And so now we have that policy that's attached to the production OEU. So go ahead and click on the policies tab again, and you can see that we have the allow all except S3 policy attached directly, the full AWS access policy that's attached directly and also the full AWS access policy that's inherited from the root container. So now what we may as well do to keep things tidy is detach the full AWS access policy that's attached directly.

So check the box next to full AWS access, click on detach and then confirm by clicking detach policy. So now the only service control policy that's directly attached to the production is the one that we just created. And just as a reminder, this is the one that allows access to all AWS products and services via this explicit allow but also has this explicit deny just for S3.

So now, if I go back to the main AWS console, and if I go into the S3 console, remember this is the general of the management AWS account, notice how I can see and interact with S3 within this account. If I go back to the main AWS console and click on the account drop-down and then switch roles into the production AWS account, remember this is the one that has this new service control policy attached to it, for the production AWS account now if I go into the S3 console and just wait for it to load, now we receive a permissions error. You don't have access to list buckets.

Now this is because even though this role that we're using does have permissions to access S3, it's operating inside the production AWS account. Because this production AWS account has this SCP attached which explicitly denies access to S3, well we have no access to S3. Access to all of the other services are unaffected because we have administrator access we could go for example to the EC2 console and then go to instances and then go to launch an instance and we won't be doing this but if you just step through you'll see that there are no permissions errors at any point in this process so we could launch an EC2 instance.

The only thing which is impacted by the service control policy is S3 and so that's the only thing that is explicitly denied because it's denied inside the service control policy. If we go back to the general account, so click on the account dropdown and then switch back. Then we go to AWS organizations, go to AWS accounts, then click on the production OU and then click on policies.

If we again attach the full AWS access and then detach the allow all except S3. Now if we follow the same process and we switch role into the production AWS account because this service control policy has no explicit denies this time if we go to the S3 console we can again access this S3 bucket so we can go inside the catpix bucket and then open the object which is Samsung.jpg and there we go we can see Samsung nice and relaxed. So this just illustrates exactly how service control policies or SCPs can be used to restrict access for identities who operate inside an AWS account.

In this case, the production AWS account. So we've removed this custom service control policy that we've created. Now let's just clean up by removing this bucket.

So select the cat picks bucket and then whatever randomness you added onto the end and click empty. Copy and paste or type permanently delete and then select empty. Once that's completed, you can click on exit and then you should be able to delete the bucket.

So select it and then click on delete. You'll need to confirm that by copying and pasting or typing the name of the bucket and then clicking delete bucket. And there you go.

You've got full control over S3 as evidenced by the fact that you can delete that bucket. So now let's go back to the general account and that's the end of this demo lesson. What you've done is create a service control policy, one which allows access to the entire account but denies S3, and you've attached this policy onto the production AWS account and removed the default full AWS access policy.

And you've observed how that has the effect of restricting the permissions that a full admin role has over the production account. At this point, that's everything I wanted to illustrate. I'll be talking more about boundaries and restrictions as they apply to AWS accounts and identities as you move through the course.

But for now, that's everything that you need to do. So go ahead and complete this video. And when you're ready, I'll look forward to you joining me in the next.

## iam-cloudwatch-logs

Welcome to this lesson where I'm going to introduce the theory and architecture of CloudWatch logs. I've already covered the metrics side of CloudWatch earlier in the course, and I'm covering the logs part now because you'll be using it when we cover CloudTrail. So in the CloudTrail demo, we'll be setting up CloudTrail and using CloudWatch logs as a destination for those logs.

So you'll need to understand it and so we'll be covering the architecture in this lesson. So let's jump in and get started. CloudWatch logs is a public service.

The endpoint which applications connect to is hosted in the AWS public zone which means you can use the product within AWS VPCs or from on-premises environments and even other cloud platforms assuming that you have network connectivity as well as AWS permissions. The CloudWatch logs product allows you to store, monitor and access logging data. Logging data at a very basic level is a piece of information data, and a timestamp.

So the timestamp is generally year, month, day, hour, minute, second, and timezone. Now there can be more fields but at a minimum it's generally a timestamp and some data. Now CloudWatch logs has some built in integrations with many AWS services.

These include EC2, VPC Flow logs, Lambda, CloudTrail, R53, and many more. Any services which integrate with CloudWatch logs can store data directly inside the product. And the security for this is generally provided by using IAM roles or service roles.

For anything outside AWS or for logging custom application or OS logs on EC2 for example, you can use the unified CloudWatch agent. Now I've mentioned this before, and I'll be demoing it later in the EC2 section of the course, but this is how anything outside of AWS products and services can log data into CloudWatch logs. So it's either AWS services which can log into CloudWatch directly or you use the unified CloudWatch agent.

And that's how you integrate. There is a third way in which you can use the development kits for AWS and implement logging into CloudWatch logs directly into your application, but that tends to be something that we'll cover in the developer and the Devops AWS courses. For now, just remember either AWS service integrations or the unified CloudWatch agent.

Now CloudWatch logs are also capable of taking logging data and generating a metric from it and this is known as a metric filter. Imagine a situation where you have a Linux instance and one of the operating system log files logs any failed connection attempts via SSH. If this logging information was injected into CloudWatch logs then a metric filter can scan those logs constantly.

And anytime it sees a mention of the failed SSH connection, it can increment a metric within CloudWatch. And on that you can have alarms which can do things based on that metric and I'll be demoing that very thing later in the course. Now let's look at the architecture visually because I'll be showing you how this works in practice in the CloudTrail demo which will be coming up later in the section.

Architecturally, CloudWatch logs looks like this. First, it's a regional service. So let's assume for this example, we talking about us-east-1.

Now the starting point are our logging sources which can include AWS products and services, mobile or server-based applications, external compute services, so virtual or physical servers, databases, or even external API's. And these sources inject data into CloudWatch logs as log events. Now log events look like this.

They have a timestamp and a message block. CloudWatch logs treats this message as a raw block of data. So it can be anything you want, but there are ways that the data can be interpreted and fields and columns defined.

Log events are stored inside log streams and log streams are essentially a sequence of log events from the same source. So let's say that you had a one log file that was stored on multiple EC2 instances that you wanted to inject into CloudWatch logs. So for example, VAR log messages which stores system diagnostics under Linux.

Well each log stream would represent VAR log messages for one instance. So you'd have one log stream for instance one for VAR log messages and one log stream for instance two, for VAR log messages. So each log stream is an ordered set of log events for a specific source for a specific thing.

Now we also have log groups and log groups are containers for multiple log streams for the same type of logging. So continuing the VAR log messages example we would have one log group containing everything for VAR log messages. So we'd set this for VAR log messages and then inside this log group would be lots of different log streams and each log stream would represent one source.

So one EC2 instance where we were receiving data for VAR log messages. Each log stream would then be a collection of log events. So every time an item was added to VAR log messages on a single EC2 instance, there would be one log event inside one log stream for that EC2 instance.

Now a log group is also the place that stores configuration settings. So it's on the log group where we define things like retention settings and permissions. And when we define these settings on a log group, they obviously apply to all log streams inside that log group.

It's also on log groups where metric filters are defined. So these metric filters are constantly reviewing any log events for any log streams in that log group looking for certain patterns, maybe an application error code, or a failed SSH login. When detected, these metric filters increment a metric and metrics can have associated alarms.

And these alarms can be used either to notify administrators or to integrate with AWS or external systems to take action. So CloudWatch logs is a really powerful product. This is the high level architecture, but don't worry you'll get plenty of exposure to it all the way through this course because lots of AWS products integrate with CloudWatch logs and use it to store their logging data.

So we'll be coming back to this product time and time again as we go through the course. CloudTrail uses CloudWatch logs, Lambda uses CloudWatch logs, VPC flow logs use CloudWatch logs. There's lots of examples of AWS products where we'll be integrating them with CloudWatch logs.

So I just wanted to introduce it at this early stage of the course. But that's everything I wanted to cover in this theory lesson. So thanks for watching.

Go ahead, complete this video and when you're ready, join me in the next.

## iam-cloudtrail

Welcome to this lesson, where I'm going to be introducing CloudTrail. CloudTrail is a product which logs API actions which affect AWS accounts. If you stop an instance, that's logged.

If you change a security group, that's logged too. If you create or delete an S3 bucket, that's logged by CloudTrail. Almost everything which can be done to an AWS account is logged by this product.

Now, I want to quickly start with the CloudTrail basics. The product logs API calls or account activities. And every one of those logged activities is called a CloudTrail event.

A CloudTrail event is a record of an activity in an a AWS account. This activity can be an action taken by a user, a role, or a service. Now, CloudTrail by default stores the last 90 days of CloudTrail events in the CloudTrail event history.

This is an area of CloudTrail which is enabled by default in AWS accounts and it's available at no cost and provides 90 days of history on an AWS account. Now, if you want to customize CloudTrail in any way beyond this 90-day event history, you need to create a trail, and we'll be looking at the architecture of a trail in a few moments' time. Now, CloudTrail events can be one of three different types.

We have management events, data events, and insight events. Now, if applicable to the course that you are studying, I'll be talking about insight events in a separate video. For now, we're going to focus on management events and data events.

Management events provide information about management operations that are performed on resources in your AWS account. These are also known as control plane operations. Think of things like creating an EC2 instance, terminating an EC2 instance, creating a VPC.

These are all control plane operations. Now, data events contain information about resource operations performed on or in a resource. So examples of this might be objects being uploaded to S3 or objects being accessed from S3, or when a Lambda function is being invoked.

By default, CloudTrail only logs management events because data events are often much higher volume. Imagine if every access to an S3 object was logged, it could add up pretty quickly. Now, a CloudTrail trail is the unit of configuration within the CloudTrail product.

It's a way you provide configuration to CloudTrail on how to operate. A trail logs events for the AWS region that it's created in. That's critical to understand.

CloudTrail is a regional service. But when you create a trail, it can be configured to operate in one of two ways. You can create a trail which is a one-region trail, or a trail can be set to all regions.

Now, a single-region trail is only ever in the region that it's created in, and it only logs events for that region. An all-region trail, you can think of as a collection of trails in every AWS region, but it's managed as one logical trail, and it's got an additional benefit that if AWS adds any new regions, then an all-region trail is automatically updated. Now this is specific configuration item on a trail which determines if it only logs events for the region that it's in, or if it also logs global services events.

Now, most services log events in the region where the event occurred. So if you create an EC2 instance in AP Southeast 2, then it's logged to that region, and a trail would either need to be a one-region trail in that region, or it would need to be an all-regions trail to pick up that event. A very small number of services log events globally to one region.

So global services such as IAM, or STS, or CloudFront, these services are very globally-focused services, and they always log their events to US East 1, which is Northern Virginia. Now, these type of events are called global service events and a trail needs to have this enabled in order to log these events. This feature is normally enabled by default, if you create a trail inside the user interface.

So this is really critical to understand. AWS services are largely split up into regional services and global services. So when these different types of services log to CloudTrail, they either log in the region that the event is generated in or they log to US East 1, if they're global services.

So when you're diagnosing problems, when you're architecting solutions, if whatever logs you are trying to reach are generated by services which are global, so IAM, STS, and CloudFront, then these are going to be classified as global service events and that will need to be enabled on a trail. Otherwise, a trail will only log events for that isolated region that it's created in. And when you create a trail, it's one of two types, one region, so it is always isolated to that one region, and you would need to create one-region trails in every region, if you wanted to do it manually.

Alternatively, you could create an all-regions trail. And that encompasses all of the regions in AWS, and it's automatically updated as AWS add new regions. Now, once you've got a trail created, management events and data events are all captured by the trail.

And this is based on whether it's isolated to a region or set to all regions. But if we keep focused on an all region trail for now, then this trail is now capturing management events, and if we enable it, data events. So data events is not something that's generally enabled by default.

It's something you have to explicitly set when you create a trail. So this trail is now listening to everything that's occurring in the account. If it's an all-region trail and it's got global services event logging turned on as well, it's listening to everything that's happening in the account.

Now, remember that the CloudTrail event history is limited to 90 days. But when you create a trail, you could be much more flexible. A trail by default can store the events in a definable S3 bucket, and the logs which are generated and stored in an S3 bucket can be stored there indefinitely.

You're only charged for the storage that's used in S3. Now, these logs are stored as a set of compressed JSON log files. And so they consume hardly any space, but they have the benefit, because they're JSON formatted, of being able to be passed by any tooling capable of reading these standard format files.

So that's a really great feature of CloudTrail, that it stores this information in a fairly standard format. Now, another option is that CloudTrail can be integrated with CloudWatch logs and the data can be stored into that product. So CloudTrail can take all of the logging data that it generates, and in addition to putting it into S3, it can put it into CloudWatch logs.

And once it's in CloudWatch logs, you can use that product to search through it, or using a metric filter to take advantage of the data that's put into CloudWatch logs. It makes it much more powerful and you get access to a lot more features, if you use CloudWatch logs versus S3. Now, one of the more recent additions to the CloudTrail product is that you can now create an organizational trail.

And this means if you create this trail from the management account of an organization, it can store all of the information for all of the accounts inside that organization. So it's a single management point for all API and account events across every account in the organization. So that's super powerful and it makes managing multi-account environments much easier.

So we need to talk through some important elements of CloudTrail point by point. So CloudTrail is enabled by default on AWS accounts, but it's only the 90-day event history that's enabled by default. So you don't get any storage in S3 unless you configure a trail.

Trails are how you can take the data that CloudTrail's got access to, and store it in better places, such as S3 and CloudWatch logs. Now, the default for trails is to store management events only. So this only includes management plane events, creating an instance, stopping an instance, terminating an instance, creating or deleting S3 buckets, logins to the console.

Anything that's interacting with AWS products and services from a management perspective is logged by default in CloudTrail. Data events need to be specifically enabled and they come at an extra cost. I'll talk about that in a little bit more detail in the demo lesson, because you need to be aware of the pricing of CloudTrail.

Much of the service is free, but there are certain elements that do carry a cost that you do need to be aware of. Especially, if you use this in production. Now, most AWS services log data to the same region that that service is in.

There are a few specific services, IAM, STS and CloudFront, which are classified as true global services, and they log their data as global service events, which gets logged to US East 1, and a trail will need to be enabled to capture that data. So that's critical. You might find that come up as an exam question.

What you will also definitely find coming up as an exam style question is where they can use CloudTrail for real-time logging. Well, this is one of the limitations of the product. It is not real time.

CloudTrail typically delivers log files within 15 minutes of the account activity occurring. And it generally publishes log files multiple times per hour. What this means is it's not real time.

You can't trust that logging into CloudTrail will give you a complete exhaustive list of events that have happened up to the very point that you're looking. Sometimes it does take a few minutes for that data to arrive in S3 or for that data to arrive in CloudWatch logs. So keep that in mind, if you face any exam questions which talk about real-time logging, CloudTrail is not the product.

Okay, so that's the end of the theory in this lesson. It's time for a demo. In the next lesson, we're going to be setting up an organizational trail within our AWS account structure.

We're going to be setting it up so it's capturing all of the data for all of our member accounts and our management account. And it's going to be storing this data in an S3 bucket and CloudWatch logs within the management account. Now, I can't wait to get started.

It's a fun one and it's something which will prove very useful for the exam as well as real world usage. So go ahead, complete this video, and when you're ready, you can join me in the demo lesson.

## iam-demo-implementing-organizational-trail

Welcome back and welcome to this CloudTrail demo where we're going to set up an organizational trail and configure it to log data for all accounts in our organization to S3 and CloudWatch logs. The first step is that you'll need to be logged into the iM admin user of the management account of the organization. So as a reminder this is the general account.

To set up an organizational trail you always need to be logged into the management account. To set up individual trails you can do that locally inside each of your accounts but it's always more efficient to use an organizational trail. Now before we start the demonstration I want to talk briefly about CloudTrail pricing.

I'll make sure this link is in the lesson description but essentially there is a fairly simple pricing structure to CloudTrail that you need to be aware of. Now the 90 days history that's enabled by default in every AWS account, that's free. You don't get charged for that.

It comes free by default with every AWS account. Now next you have the ability to get one copy of management events free in every region in each AWS account. So that means creating one trail that's configured for management events in each region in each AWS account and that comes for free.

If you create any additional trails so you get any additional copies of management events then they're charged at two dollars per 100,000 events. That won't apply to us in this demonstration but you need to be aware of that if you're using this in production. Now logging data events comes at a charge regardless of the number so we're not going to enable data events for this demo lesson but if you do enable it then that comes at a charge of 10 cents per 100,000 events and that's irrespective of how many trails you have that's from the first time you're logging any data events this charge applies.

Now what we'll be doing in this demo lesson is setting up an organizational trail which will create a trail in every region in every account inside the organization. But because we get one for free in every region in every account, we won't incur any charges for the CloudTrail side of things. We will be charged for any S3 storage that we use.

But S3 also comes with a free tier allocation for storage, which I don't expect us to breach. With that being said, let's get started and implement this solution. So to do that, we need to be logged in to the console UI again in the management account of the organization.

And then we need to move to the CloudTrail console. Now if you've been here recently, it will be in the Recently Visited Services. If not, just type CloudTrail in the Find Services box.

And then open the CloudTrail console. Once you're at the console, you might see a screen like this. If you do then you can just click on the hamburger menu on the left and then go ahead and click on trails.

Now depending on when you're doing this demo if you do see any warnings about a new or old console version then just make sure that you select the new version so your console looks like what's on screen now. Now once you're here we need to create a trail so go ahead and click on create trail. To create a trail you're going to be asked for a few important pieces of information the first of which is the trail name.

Now for trail name we're going to use animals4life.org so just go ahead and enter that. Now by default with this new UI version when you create a trail it's going to create it in all AWS regions in your account. If you're logged into the management account of the organization as we are you also have the ability to enable it for all regions in all accounts of your organization.

So we're going to do that because this allows us to have one single logging location for all CloudTrail logs in all regions in all of our accounts so go ahead and check this box. Now by default CloudTrail stores all of its logs in an S3 bucket and when you're creating a trail you have the ability to either create a new S3 bucket to use or you can use an existing bucket. Now we're going to go ahead and create a brand new bucket for this trail.

Bucket names within S3 need to be globally unique so it needs to be unique name across all regions across all AWS accounts so we're going to call this bucket we're going to start with CloudTrail so type CloudTrail and then a hyphen and then animals for life and then another hyphen and then you'll need to put a random number you'll need to pick something different from me and different from every other student doing this demo so if you get an error about the bucket name being in use you just need to change this random number. Now you're also able to specify if you want the log files stored in the S3 bucket to be encrypted. Now the way that this is done is using SSE-KMS encryption.

This is something that we'll be covering elsewhere in the course and for production usage this is something that you would definitely want to use. For this demonstration to keep things simple we're not going to be encrypting the log files files and so I want you to go ahead and untick this box. Now under additional options you're able to select log file validation so this adds an extra layer of security which means that if any of the log files are tampered with you have the ability to determine that so this is a really useful feature if you're performing any account level audits.

In most production situations I do enable this, but you can also elect to have an SNS notification delivery. So every time log files are delivered into this S3 bucket, you can have a notification again for production usage, or if you need to integrate this with any non AWS systems, and this is often quite useful, but for this demonstration, we'll leave this one unchecked. Now you also have the ability as well as storing these log files into S3 to store them in CloudWatch logs and this gives you extra functionality because this allows you to perform searches, look at the logs from a historical context inside the CloudWatch logs user interface as well as define event driven processes so you can configure CloudWatch logs to scan these CloudTrail logs and in the event that any particular piece of text occurs in the logs, any API call, any actions by a user, you can generate an event which can invoke for example a Lambda function or spawn some other event driven processing.

And don't worry if you don't understand exactly what this means at this point I'll be talking about all of this functionality in detail elsewhere in the course. Now for this demonstration we are going to enable CloudTrail to put these logs into CloudWatch logs as well so check this box. You can choose a log group name within CloudWatch logs for these CloudTrail logs.

If you want to customize this you can but we're going to leave it as the default. Now as with everything inside AWS if a service is acting on our behalf we need to give it the permissions to interact with other AWS services and CloudTrail is no exception. We need to give CloudTrail the ability to interact with CloudWatch logs and we do that using an IAM role and don't worry we'll be talking about IAM roles in detail elsewhere in the course.

For this demonstration just go ahead and select new because we're going to create a new IAM role, a new IAM role that will give CloudTrail the ability to enter data into CloudWatch logs. Now what we need to do is provide a role name so go ahead and enter CloudTrail role for CloudWatch logs and then an underscore and then animals for life. The name doesn't really matter but in production settings you'll want to make sure that you're able to determine what these roles are for and so we'll use a standard naming format.

Now if you expand policy document you'll be able to see the exact policy document or IAM policy document that will be used to give this role the permissions to interact with CloudWatch logs. Now don't worry at this point if you don't fully understand policy documents we'll be using them throughout the course and over time you'll become much more comfortable with exactly how they're used but at a high level this policy document will be attached to this role and this is what will give CloudTrail the ability to interact with CloudWatch logs. At this point just scroll down that's everything that we need to do go ahead and click on next.

Now at this point you'll need to select what type of events you want this trail to log. You've got three different choices. The default is to log only management events so this logs any events against the account or AWS resources so things like starting or stopping an EC2 instance, creating or deleting an EBS volume those type of things will be logged using management events.

You've also got data events and data events give you the ability to log any actions against things inside resources so currently CloudTrail does support a wide range of services for data event logging so you can click on this drop down and see all of the services that it supports. Now for this demonstration we won't be setting this up with data events initially because I'll be covering this elsewhere in the course so go back to the top and uncheck data events. You also have the ability to log insight events and these can identify any unusual activity errors or user behavior on your account so this is especially useful from a security perspective.

Now again for this demonstration we won't be logging any insight events we're just going to log management events. For management events you can further filter down to read or write or both and optionally exclude KMS or RDS data API events and I'll be talking about KMS elsewhere in the course. For this demo lesson we're just going to go ahead and leave it as default so make sure that read and write are checked.

Once you've done that go ahead and click on next on this screen you just need to review everything that all looks good so go ahead and click on create trail now at this point if you do get an error saying the s3 bucket already exists you'll just need to choose a new bucket name so click on edit at the top change the bucket name to something that's globally unique and then just follow that process through again and create the trail after a few moments that trail will be created it It should say US East Northern Virginia as the home region. Even though you didn't get the option to select it because it's selected by default, it is a multi-region trail. And then finally, it is an organizational trail, which means that this trail is now logging any cloud trail events from all regions in all accounts in this AWS organization.

Now this isn't real time, and when you first enable it, it can take some time for anything to start to appear in either S3 or in CloudWatch logs. Now at this stage, what I recommend is that you pause the video and wait for 10 to 15 minutes before continuing, because the initial delivery of that first set of log files through to S3 can take some time. So pause the video, wait 10 to 15 minutes, and then you can resume.

Then right click this link under S3 bucket and open that in a new tab. Then go to that tab and you should start to see a folder structure being created inside the S3 bucket. So let's move down through this folder structure, starting with CloudTrail.

Let's go to US East 1 and just keep going down through this folder structure. And in my case, I have quite a few of these log files which have been delivered already. So I'm going to pick one of them, the most recent, and just click on Open.

Depending on the browser that you're using, you might have to download and then uncompress this file. Because I'm using Firefox, it can natively open the GZ compressed file and then automatically open the JSON log file inside it. So this is an example of a CloudTrail event.

We're able to see the user identity that actually generates this event. In this case, it's me, I am admin. We're able to see the account ID that this event is for.

We can see the event source, the event name, the region, the source IP address, the user agent, in this case the console, all of the relevant information for this particular interaction with the AWS APIs are logged inside this CloudTrail event. Now don't worry if this doesn't make a lot of sense at this point. You're going to get a lot of opportunity to interact with this type of logging event as you do all the various theory and practical lessons within the course.

For now, I just want to highlight exactly what to expect with CloudTrail logs. Now because we've enabled all of this logging information to also go into CloudWatch logs, we can take a look at that as well. So back at the CloudTrail console, if we just click on services, and then type CloudWatch, wait for it to pop up, locate logs underneath CloudWatch, and then open that in a new tab.

Inside CloudWatch, on the left-hand menu, look for logs, and then log groups, and open that. You might need to give this a short while to populate, but once it does, you should see a log group for the cloud trail that you've just created. Go ahead and open that log group.

Inside it, you'll see a number of log streams. Now these log streams will start with your unique organizational code, so this will be different for you. Then there will be the account number of the account that it represents.

Again, these will be different for you. And then there'll be the region name. Because I'm only interacting with the Northern Virginia region, Currently, the only ones that I see are for US East 1.

Now this particular account that I'm in, the general account of the organization, if I look at the ARN at the top or Amazon resource name, if I look at the thing after US East 1 here, this number is my account number. So this is the account number of my general account. So if I look at the log streams, in my case you'll be able to see that this account, So the general account matches this particular log stream.

You'll be able to do the same thing in your account. If you look for this account ID and then match it with one of the log streams, you'll be able to pull the logs for the general AWS account. So if I go inside this particular log stream, then as CloudTrail logs any activity in this account, all of that information will be populated into CloudWatch logs.

And that's what I can see here. And if I expand one of these log entries, we'll see the same formatted CloudTrail event that I just showed you in my text editor. So the only difference when using CloudWatch logs is that the CloudTrail events also get entered into a log stream in a log group within CloudWatch logs.

And as you can see here, the format looks very similar. Now if we just return to the CloudTrail console, one last thing that I wanted to highlight, if you just expand the menu on the left, Whether you enable a particular trail or not, you've always got access to the event history. And the event history stores a log of all CloudTrail events for the last 90 days for this particular account, even if you don't have a specific trail enabled.

So this is standard functionality. What a trail allows you to do is customize exactly what happens to that data. So this area of the console, the event history, always useful if you just want to go in and search for a particular event, maybe check who's logged onto the account recently or look at exactly what the IAM admin user has been doing within this particular AWS account.

The reason why we created a trail is to persistently store that data in S3 as well as put it into CloudWatch logs which gives us that extra functionality. Now with that being said that is everything that I wanted to cover in this demo lesson. One thing that you do need to be aware of is that S3 as a service provides a certain amount of resource under the free tier that's available in every new AWS account so you can store a certain amount of data in S3 free of charge.

The problem with CloudTrail and especially organizational trails is they do generate quite a large number of requests and there is also in addition to space there is a number of requests per month that are part of the free tier. Now if you leave this cloud trail enabled for the duration of your studies for the entire month then it is possible that this will go slightly over the free tier allocation for requests within the S3 service. So you might see warnings that you're approaching a billable threshold and you might even get a couple of cents of bill per month if you leave this enabled all the time.

To avoid that if you just go to trails, open up the trail that you've created and then just go ahead and click on stop logging. You'll need to confirm that by clicking on stop logging and at that point no logging will occur into the S3 bucket or into CloudWatch logs and you won't experience those charges. Now for any production usage the low cost of this service means that you would normally leave it enabled in all situations but to keep costs within the free tier for this course you can if required just go ahead and stop the logging if you don't mind a few cents per month of s3 charges for cloud trail then by all means go ahead and leave it enabled with that being said though that's everything I wanted to cover in this demo lesson so go ahead complete the lesson and then when you're ready I look forward to you joining me in the next

## iam-aws-control-tower-101

Welcome back, and in this video, I want to talk about AWS Control Tower. This is a product which is becoming required knowledge if you need to use AWS in the real world. And because of this, it's starting to feature more and more in all of the AWS exams.

I want this to be a lesson applicable to all of the AWS study paths, so think of this as a foundational lesson. And if required, for the course that you're studying, I might be going into additional detail. We do have a lot to cover, so let's jump in and get started.

At a high level, Control Tower has a simple but wide ranging job, and that's to allow the quick and easy setup of multi-account environments. You might be asking, "Doesn't AWS Organizations already do that?" Well, kind of, Control Tower actually orchestrates other AWS services to provide the functionality that it does, and one of those services is AWS Organizations. But it goes beyond that.

Control Tower uses Organizations, IAM Identity Center, which is the product formerly known as AWS SSO, it also uses CloudFormation, AWS Config, and much more. You can think of Control Tower as another evolution of AWS Organizations adding significantly more features, intelligence, and automation. There are a few different parts of Control Tower which you need to understand, and it's worth really focusing on understanding the distinction now because we're going to be building on this later.

First, we've got the Landing Zone, and simply put, this is the multi-account environment part of Control Tower. This is what most people will be interacting with when they think of Control Tower. Think of this like AWS Organizations only with super powers.

It provides via other AWS services single sign-on and ID Federation so you can use a single login across all of your AWS accounts, and even share this with your existing corporate identity store. And this is provided using the IAM Identity Center, again, the service formerly known as AWS SSO. It also provides centralized logging and auditing, and this uses a combination of CloudWatch, CloudTrail, AWS Config, and SNS.

Everything else in the Control Tower product surrounds this Landing Zone, and I'll show you how this looks later in this lesson. Control Tower also provides guardrails, again, more detail on this is coming up soon. But these are designed to either detect or mandate rules and standards across all AWS accounts within the Landing Zone.

You also have the Account Factory which provides really cool automation for account creation, and adds features to standardize the creation of those accounts. This goes well beyond what AWS Organizations can do on its own, and I'll show you how this works over the rest of this lesson. And if applicable, for the path that you're studying, there will be a demo coming up elsewhere in the course.

Finally, there's a dashboard which offers a single-page oversight of the entire organization. At a high level, that's what you get with Control Tower. Now, things always make more sense visually, so let's step through this high-level architecture visually, and I hope this will add a little bit more context.

We start with Control Tower itself, which like AWS Organizations, is something you create from within an AWS account. And this account becomes the management account at the Landing Zone. At this top, most level within the management account, we have Control Tower itself, which orchestrates everything.

We have AWS Organizations, and as you've already experienced, this provides the multi-account structure, so organizational units and service control policies. And then, we have single sign-on provided by the IAM Identity Center, which historically was known as AWS SSO. This allows for, as the name suggests, single sign-on, which means we can use the same set of internal or federated identities to access everything in the Landing Zone that we have permissions to.

This works in much the same way as AWS SSO worked, but it's all set up and orchestrated by Control Tower. When Control Tower is first set up, it generally creates two organizational units. The foundational organizational units, which by default is called Security, and a custom organizational unit, which by default is named Sandbox.

Inside the foundational or security organizational unit, Control Tower creates two AWS accounts, the Audit account and the Log Archive account. The Log Archive account is for users that need access to all logging information for all of your enrolled accounts within the Landing Zone. Examples of things used within this account are AWS Config and CloudTrail logs, so they're stored within this account so that they're isolated.

You have to explicitly grant access to this account, and it offers a secure, read-only Archive account for logging. The Audit account is for your users which need access to the audit information made available by Control Tower. You can also use this account as a location for any third-party tools to perform auditing of your environment.

It's in this account that you might use SNS for notifications of changes to governance and security policies, and CloudWatch for monitoring Landing Zone wide metrics. It's at this point where Control Tower becomes really awesome because we have the concept of an Account Factory. Think of this as a team of robots who are creating, modifying, or deleting AWS accounts as your business needs them.

And this can be interacted with both from the Control Tower console or via the Service Catalog. Within the custom organizational unit, Account Factory will create AWS accounts in a fully automated way as many of them as you need. The configuration of these accounts is handled by Account Factory.

So, from an account and networking perspective, you have a baseline or cookie-cutter configurations applied, and this ensures a consistent configuration across all AWS accounts within your Landing Zone. Control Tower utilizes CloudFormation under the covers to implement much of this automation, so expect to see stacks created by the product within your environment. And Control Tower uses both, AWS Config and Service Control Policies, to implement account guardrails.

And these detect drifts away from governance standards, or prevent those drifts occurring in the first place. At a high level, this is how Control Tower looks, now the product can scale from simple to super complex. This is a product which you need to use in order to really understand.

And depending on the course that you're studying, you might have the opportunity to get some hands-on later in the course. If not, don't worry, that means that you only need this high-level understanding for the exam. Let's move on and look at the various parts of Control Tower in a little bit more detail.

Let's quickly step through the main points at the Landing Zone. It's a feature designed to allow anyone to implement a well-architected, multi-account environment, and it has the concept of a home region, which is the region that you initially deploy the product into, for example, us-east-1. You can explicitly allow or deny the usage of other AWS regions, but the home region, the one that you deploy into, is always available.

The Landing Zone is built using AWS Organizations, AWS Config, CloudFormation, and much more. Essentially, Control Tower is a product which brings the features of lots of different AWS products together and orchestrates them. I've mentioned that there's a concept of the foundational OU, by default called the Security OU, and within this, Log Archive and Audit AWS accounts.

And these are used mainly for security and auditing purposes. You've also got the Sandbox OU which is generally used for testing and less rigid security situations. You can create other organizational units and accounts, and for a real-world deployment of Control Tower, you're generally going to have lots of different organizational units.

Potentially, even nested ones to implement a structure which works for your organization. Landing Zone utilizes the IAM Identity Center, again, formerly known as AWS SSO, to provide SSO or single sign-on services across multiple AWS accounts within the Landing Zone, and it's also capable of ID Federation. And ID Federation simply means that you can use your existing identity stores to access all of these different AWS accounts.

The Landing Zone provides monitoring and notifications using CloudWatch and SNS, and you can also allow end users to provision new AWS accounts within the Landing Zone using Service Catalog. This is the Landing Zone at a high level, let's next talk about guardrails. Guardrails are essentially rules for multi-account governance.

Guardrails come in three different types, mandatory, strongly recommended, or elective. Mandatory ones are always applied. Strongly recommended are obviously strongly recommended by AWS.

And elective ones can be used to implement fairly niche requirements, and these are completely optional. Guardrails themselves function in two different ways. We have preventative and these stop you doing things within your AWS accounts in your Landing Zone, and these are implemented using Service Control policies, which are part at the AWS Organizations product.

These guardrails are either enforced or not enabled, so you can either enforce them or not. And if they're enforced, it's simply means that any actions defined by that guardrail are prevented from occurring within any of your AWS accounts. An example of this might be to allow or deny usage of AWS regions, or to disallow bucket policy changes within accounts inside your Landing Zone.

The second functional type of guardrail is detective, and you can think of this as a compliance check. This uses AWS Config rules and allows you to check that the configuration of a given thing within an AWS account matches what you define as best practice. These type of guardrails are either clear, in violation, or not enabled.

And an example of this would be a detective guardrail to check whether CloudTrail is enabled within a AWS account, or whether any EC2 instances have public IPv4 addresses associated with those instances. The important distinction to understand here is that preventative guardrails will stop things occurring, and detective guardrails will only identify those things. So, guardrails are a really important security and governance construct within the Control Tower product.

Lastly, I want to talk about the Account Factory itself, this is essentially a feature which allows automated account provisioning, and this can be done by either cloud administrators or end users with appropriate permissions. And this automated provisioning includes the application of guardrails, so any guardrails which defined can be automatically applied to these automatically provisioned AWS accounts. Because these accounts can be provisioned by end users, think of these as members of your organization, then either these members of your organization or anyone that you define can be given admin permissions on an AWS account which is automatically provisioned.

This allows you to have a truly, self-service, automatic process for provisioning AWS accounts so you can allow any member of your organization within tightly controlled parameters to be able to provision accounts for any purpose which you define as okay. And that person will be given admin rights over that AWS account. These can be long-running accounts or short-term accounts, these accounts are also configured with standard account and network configuration.

If you have any organizational policies for how networking or any account settings are configured, these automatically provisioned accounts will come with this configuration. And this includes things like the IP addressing used by VPCs within the accounts which could be automatically configured to avoid things like addressing overlap. And this is really important when you're provisioning accounts at scale.

The Account Factory allows accounts to be closed or repurposed, and this whole process can be tightly integrated with a businesses SDLC or software development life cycle. So, as well as doing this from the console UI, the Control Tower product and Account Factory can be integrated using APIs into any SDLC processes that you have within your organization. If you need accounts to be provisioned as part of a certain stage of application development, or you want accounts to be provisioned as part of maybe client demos or software testing, then you can do this using the Account Factory feature.

At this point, that is everything I wanted to cover at this high level about the Control Tower. If you need practical experience of Control Tower for the course that you are studying, there will be a demo lesson coming up elsewhere in the course, which gives you that practical experience. Don't be concerned if this is the only lesson that there is, or if there's this lesson plus additional deep-dive theory.

I'll make sure, for whatever course you're studying, you have enough exposure to Control Tower. With that being said, though, that is the end of this high-level video. So go ahead and complete the video, and when you're ready, I'll look forward to you joining me in the next.

