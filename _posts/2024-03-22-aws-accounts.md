---
title: "AWS SAA-C03 part 1: Account Basics"
categories:
  - exams
tags:
  - aws-saa-c03
---

I'm officially a [Django contributor](https://github.com/django/django/pull/17916), yay. 

Next milestone: clearing the SAA-C03 in May. 

I'm doing the Cantrill course along with TutorialsDojo. The below is me revising the video content with the help of some simple scripts, I work a lot better with text and async work rather than video content. (Seriously, why is everything videos?) 

## aws-accounts-aws-accounts-the-basics.txt

Welcome back, and in this lesson, I want to introduce AWS Accounts. Really understanding what an AWS Account is and what benefits it provides is one of the most important things within AWS. Many students, especially at the start, confuse AWS Accounts with users inside of those accounts and I want you to be 100% clear on the difference.

If you've used AWS before, you might already have an idea of what AWS Accounts are and how they work, but understanding accounts at a really instinctive level is essential for a solutions architect, developer or engineer. Simple systems which you design might operate from within a single AWS Account, but more complex systems or environments operated by large enterprises might use tens, or in some cases, hundreds of AWS Accounts, and for that reason, it's important that you really understand the features and benefits provided by AWS Accounts. This might seem pretty basic, but it's really powerful when you do fully understand it and really dangerous to operate at production scale if you don't.

Let's jump in and get started. This is an AWS Account. When you're just starting with AWS, you might only create one of these.

You might even already have one. Bigger, more complex projects or businesses will generally use many AWS Accounts, and in this course, you're going to use multiple AWS Accounts for the demo lessons, and this will help you understand how businesses actually use AWS in the real world. At a high level, an AWS Account is a container for identities and AWS resources.

Identities is just the technically correct way of referring to things like users, so the things which you use to log in to systems such as AWS. An AWS Account contains users, which you log in with, and resources, which you provision, inside of that account. Keep this idea of an AWS Account being a container in your mind constantly as you move through the course, but this is especially important in this stage of the course where you're going to be creating the AWS Accounts that you'll use constantly as you move through the content.

When you create an AWS Account, you give the account a name, you need to provide a unique email address, and you also need to provide a payment method, which is generally a credit card. If we're creating a production account, we might name the account PROD for production, we would use a unique email address which is unique for this specific AWS Account, and provide a credit card for this production account. Just to reiterate, the credit card can be used for multiple AWS Accounts, but the email address can't.

It has to be unique. You need one unique email address for every AWS Account. The email address that you provide when creating the account is used to create a special type of identity within the AWS Account, which is known as the account root user.

Every AWS Account has an account root user, so the root user of that AWS Account. In this example, if you create a production AWS Account, then the account root user of that account can only log in to that one production AWS Account. If you make another AWS Account, let's say a developer account, then that account will have its own unique account root user with its own unique email address.

Those account root users are different. The production account root user can only access the production account and the developer account root user can only access the developer account. Initially, the account root user is the only identity, the only user created with an AWS Account.

Initially, you have the blank account, the container, and inside that is the account root user of that account. The account root user has full control over that one specific AWS Account and any resources which are created inside it. The account root user can't be restricted.

It will always have full access to everything within that one AWS Account which it belongs to. This is the reason why we need to be really careful with the account root user, because if the user name and password ever become known, the results can be disastrous because the details can be used to delete everything within the AWS Account. The credit card that you provide when you create the AWS Account, that's set as the account payment method, so you can create resources within an AWS Account, and I'll be covering these throughout the course, and if those resources have any billable usage, then that usage is billed to the account payment method, in this case, a credit card.

I'll talk about this later in the course, but on the whole, AWS is what's known as a pay-as-you-consume or pay-as-you-go platform. If you use a service within an AWS Account for two minutes, then you pay for two minutes of that service. Certain services include a certain allocation of free usage per month, and this is known as the free tier, and this is what we're going to take advantage of in this course to keep costs at an absolute minimum.

Now that I've covered the account root user and billing within an account, now I want to touch on the security as it relates to AWS Accounts. You know that the account root user has full control over this one specific AWS Account and this can't be restricted. You can create additional identities inside the AWS Account which can be restricted.

I'll talk about this more soon, but this uses a service called Identity and Access Management, known as IAM, and with IAM, you can create other identities inside the account. These can be different types of identities. We've got IAM users, IAM groups and IAM roles, and I'll cover these in detail in the relevant section of the course, but at this point, it's important to understand that all of these IAM identities start off with no access to the AWS Account, but they can all be given full or limited access rights over this one specific AWS Account.

Just like the account root user, the IAM service is also dedicated to your account. Unless you specify otherwise, any IAM identities created in my account won't be able to access your account. Only identities which you create inside your account and then grant access will be able to access resources within your AWS Account.

Later in the course, I'll talk about how you can do cross-account permissions, but for this point in the course, just think of AWS Accounts as containers. Only things within the account can access anything else within that same account, and another key thing to remember is that with the exception of the account root user, any IAM identity starts off with no permissions. You have to explicitly grant permissions to any identities managed by the IAM service.

Another concept which I want you to be really familiar with is the boundary of the account. On screen now, the orange line around the account, think of this as a wall. It can keep things inside the account from getting out and also keep things outside the account from getting in.

AWS Accounts are really good at containing any damage caused within those accounts, so things such as an inexperienced system administrator doing something silly or a bad actor attempting to intentionally harm your account. If the credentials for the account root user are leaked, then these could be used to delete everything inside that one specific AWS Account, and if your entire business runs from that one single account, then this can be really, really bad. However, if you create separate AWS Accounts for different uses, maybe a development account, a test account and a production account, then you can limit the damage.

If you have any credential leakage or if you have any system admins doing any silly mistakes causing resources to be deleted, then generally these will be isolated to that one specific AWS Account. You can also create AWS Accounts for different teams within your business or even different products that your business sells. AWS Accounts are great for keeping bad things inside one specific part of your AWS environment.

They're also really good for keeping things outside of that boundary. By default, all access to an AWS Account is denied, so unless you configure otherwise, no external identity is allowed access to an AWS Account. The exception to this, of course, is the account root user of that account, who always has full control.

This means that any external identities, for example, external users, are denied by default if they attempt to access your AWS Account. External identities can be granted access, such as Julie in the middle, if you explicitly want to allow this access, but the default security stance is that unless you explicitly allow something, then no access is allowed to your AWS Account. That's AWS Accounts.

They're a crucial part of the AWS product set and understanding them at a really instinctive level is important. Whether you're a solutions architect, a developer, a sysadmin or a DevOps engineer, you need to be comfortable with how to use AWS Accounts effectively. In the following lessons, you're going to create the AWS Accounts which you'll be using for the duration of this course.

I'm strongly recommending that you create brand-new AWS Accounts. Don't make the mistake of trying to use your existing AWS Account or accounts because they're likely to be in a pretty bad state. The longer an AWS Account exists, the more potential there is for misconfiguration, and so it's much better to use brand-new accounts for this course.

I want you to learn how to configure all of this in a correct way using best practices, so please go ahead and create brand-new AWS Accounts for this course. I'll even show you a trick so that you can use one email account to create all of the unique email addresses needed for these multiple accounts, so it shouldn't take that much in the way of effort. With that being said, go ahead and complete this lesson, and then when you're ready, I look forward to you joining me in the next lesson where we're going to get started on creating the AWS Accounts for this course.

## aws-accounts-demo-creating-aws-account.txt

Welcome back and in this demo lesson I'm going to step you through how to create an AWS account. This might seem simple but it's important that we start off with the same best practice foundation. In the real world most businesses and projects will use more than one AWS account.

So rather than teaching you using sandbox accounts or using a single AWS account you're going to create a few accounts that you'll use as you move through the course. Now later in the course you're going to link these together using AWS organizations as you start to learn about multi-account management. For now though we're going to start with a single account and before we get started with this I want to show you visually what you're going to be creating over the first part of the course.

Now the first account that you'll be creating is the account that you're going to be logging into and we're going to start by referring to this as the general AWS account. Later in the course when you start using AWS organizations and learn about multi-account management You're going to hear me refer to this as the management AWS account just know that the management account and the general account are the same thing We're referring to this first AWS account that you're going to create So this will be the first account that you'll create and as you know by now when you create an AWS account an account "Account Root User" is created along with it. And it's this "Account Root User" that you'll initially log in to this general AWS account with.

Remember, the "Account Root User" is specific to this one particular account, so this "Account Root User" has full control of the general AWS account. Once you've created this AWS account, you're going to secure it. And this is done by adding multi-factor authentication, also known as MFA, onto the account root user.

Now historically this was a physical device which generated a code which changed periodically. But you can also use an application on your phone or tablet. The idea is that a physical or virtual MFA is associated with the account root user.

Then instead of just needing a username or password to log in, which can be leaked, now Now you also need a one-time code which is generated by the MFA device or application, and this means it's much more secure. You're also going to be configuring a budget, because while the course is going to be as much within the free tier as possible, if you do leave anything running, this might have a cost and will want you to be notified as soon as possible, so a budget helps protect against any unintended costs. Now we also want to avoid using the account root user as much as possible because you can't restrict it and because there's only one of them per AWS account.

Now because of this it's best practice to create IAM identities within your AWS accounts and so you're going to create an IAM identity, an IAM user within the general AWS account called IAM admin. Now this is just a normal IAM user which you're going to give administrator permissions over the general AWS account and this is the identity that you're going to be using for the remainder of the course when you're interacting with the general AWS account. Once you've fully created and configured the general account you're going to repeat that process to create a second one which we're going to refer to as the production AWS account.

So this is a brand new AWS account with a brand new account root user and a brand new IAM identity within that account also called IAM admin. Now this will be the starting structure that you're going to be using throughout the course. Before we get started though I promise you a trick to make creating multiple AWS accounts easier and that's what I want to talk about next.

Now this is a feature that I know a hundred percent works with Gmail It may work with other email providers, but I can only guarantee Gmail at this point. When you're creating AWS accounts, you should view them as disposable, and you should create as many of them as you need. You already know why, because they're containers and they isolate things inside the AWS account.

It's actually better to create a new AWS account structure for every course that you do, because it keeps things isolated and safe and secure. Now because AWS accounts require unique email addresses this can make it a fairly painful process to create them. Historically 10 AWS accounts have required 10 unique email addresses but that's not true if you use a feature available within Gmail and some other email providers.

Let's say that you have a Gmail address in this case it's It's catguy@gmail.com. So this email address is constructed of two parts. The username on the left, so catguy, and then an @ symbol, and then the domain, so gmail.com.

Now normally this would allow you to create one AWS account using the catguy@gmail.com email address. But what you can do is you can use the plus sign in the email address to create an infinite supply unique addresses all of which go back to this main account. For example you could take your username so cat guy and then add a plus and then put AWS account 1 so the whole email address would be cat guy plus AWS account 1 at gmail.com you could also create a second this time using AWS account 2 and then even a third using AWS account 3.

Now these are all unique email addresses but they've required no configuration. You just have the one single Gmail account which comes with the one default email address so catguy@gmail.com and all you do is use the plus symbol and then include any text and that creates a brand new unique email address from the perspective of AWS but you haven't had to configure anything on Gmail. You just take your normal email address, you add some text after the plus sign and that creates what's called a dynamic alias.

It's a brand new email which always points at your main Gmail account. So you can use anything after the plus symbol and it creates what looks like a unique email address and you can use this address to sign up for an AWS account. So this essentially gives you an infinite number of unique email addresses using one single Gmail.

So at this point you don't have any reason not to create a brand new set of AWS accounts for every single training course that you do. Now let's switch over to the console and get started creating the first AWS account, so the general AWS account. Okay so now I've moved across to my web browser and to create an AWS account you're going to need a few things.

You'll need an email address for the account root user of that account and remember what I've just talked about on the previous screen how you can create an infinite number of unique emails to use. You'll also need to choose an AWS account name and this is important because it will help you identify the account. You'll need to set a unique password for this account root user.

You'll need billing information to add to the account. Now the account does come with a free tier allocation so you won't be billed against this billing method unless you actually incur charges and I'll be teaching you throughout this course how you can keep track of any charges on your AWS account and the course itself where possible will be within the free tier. In addition to this you'll need to verify your identity and you'll also need to choose a support plan even if that plan is the free one.

So to get started we need to go ahead and enter the email address for this AWS account. Now remember this is the general AWS account. You'll need to pick something that makes sense to you and is unique to you because this email address needs to be unique and you do need to be able to receive emails to this address.

Now depending on the version of the user interface that you do have and this can change very often you might get this box pre-populated so this AWS account name. For me this is the structure I'll be using so AC my initials - training - AWS and then hyphen general. This is for the general AWS account and I'll be changing this general to production when I create the production account.

Now at this stage you'll need to verify the email address so once you've entered all of that information go ahead and click verify email address. You'll receive a verification email containing a code to this address. It could take up to five minutes to arrive and do make sure that you check your spam folder.

Once you do have that code, enter it into this box and then click on verify. Hopefully you'll see that the email address has been verified and then we're good to continue and it's at this point that you'll need to pick a suitably strong password for the account root user of this account. Now I recommend using a password manager to generate a strong password so go ahead and do that enter that same password into both boxes and then click on continue.

Next you'll be asked for some account information, generally this will be a personal AWS account for your own projects, so pick the appropriate box, enter the appropriate information here, check this box and click on continue and I'm going to be hiding this information for privacy reasons. Next you'll need to enter some billing information and this payment method won't be charged unless you incur charges against the AWS account. I'm going to keep this course as much within the free tier as possible so this generally shouldn't happen.

Now it's It's worth noting that you might notice a pending payment on this credit or debit card which AWS used to verify your identity. This pending charge will generally disappear within a few days. It's only used to verify that it's a valid billing method.

So go ahead and enter all of this information and then continue and once again I'm going to keep this information redacted for privacy reasons. This next step is a simple identity verification step. You'll need to pick the method of identity verification, either SMS or voice call.

I'm going to pick SMS because generally that's quicker. You might only see one or the other of these options or you might see both. Just pick the one that's appropriate.

For SMS you'll need to enter a valid phone number to receive text messages to, so I'm going to enter my details. You might need to complete this security check by entering these characters, so I'm going to go ahead and do that. Then I'll move on.

I'll wait for the verification code to arrive, enter it into that box, and then move on to the next step. At this point you'll need to pick the support plan to use. For training accounts we default to using the basic support plan which is free.

And this will provide just enough support for any account or billing issues. If we need anything more, if this is a production AWS account, then we need to pick Developer or Business support. Now I'll be covering the details of these other support plans, if appropriate, elsewhere in the course.

For now though, go ahead and pick 'Basic Support' and then click the button to continue. Now at this point you should see a 'Congratulations' screen which tells you that AWS are activating your account. Now this activation can sometimes be instant or it can take anywhere up to an hour.

In my case I've already received the email, so normally it is relatively quick. Once you do receive the email, you can click to start logging in to the management console. And again, you'll need to use the email address associated with the account root user.

You might have to complete a security check, but then you will have to enter the password for the account root user. And once you've logged in, you'll be at the main AWS console. And now we're logged into the main AWS console.

Now don't worry if you do see some error or warning notifications when you first sign into the console. these widgets take time to populate. There are a few final steps that I want you to do before we finish up creating this AWS account.

To do that click on the account drop down at the top right and then move to account. Now again I've blanked out all of my personal information. What I want you to do though is to scroll down on this screen then optionally under alternate contacts you can click on edit and enter your details for all three of these contacts.

If you creating an AWS account for business reasons then often you might have different billing operation and security contacts. Now you don't have to do this step but if you are creating this account for real-world usage you might want to enter these details. What I do want you to do though is to continue scrolling down and under IAM user and role access to billing information click on edit check this activate IAM access box and then click on update.

This is going to make sure that if you're logged in as an IAM identity then you have full access to the billing console provided you have permissions. If this box wasn't checked then even if we gave an IAM identity full admin permissions it wouldn't be able to access the billing console so it's important that we allow access to this console. Now at this point that's everything that you need to do in this creating an AWS account video so move back to the console and one last thing I want to mention is throughout this course whenever you're interacting with AWS generally I want you to be in the Northern Virginia region.

Now what region is selected by default depends on where you're logging into AWS from and this region selection does have the tendency to change so generally as you're working through any of my courses continually verify that if the region is selected it does say US East 1. If it says anything like global that's okay but if it displays a region make sure that it's US East 1 and if it's not go ahead and change it back to Northern Virginia. At this point though that's everything I wanted to cover.

You've completed the account setup of the general AWS account so go ahead and complete this video and when you're ready I look forward to you joining me in the next.

## aws-accounts-multifactor-authentication.txt

00:00:00.300 --> 00:00:01.170 Welcome back, 00:00:01.170 --> 00:00:03.150 and in this fundamentals lesson, 00:00:03.150 --> 00:00:05.040 I want to quickly cover a topic 00:00:05.040 --> 00:00:07.440 which you'll use constantly within the course 00:00:07.440 --> 00:00:08.730 and in the real world, 00:00:08.730 --> 00:00:13.110 and that's multifactor authentication, known as MFA. 00:00:13.110 --> 00:00:15.240 Now, we have a fair amount of theory to cover. 00:00:15.240 --> 00:00:17.700 So let's just jump in and get started.

00:00:17.700 --> 00:00:19.290 Now, before I talk about the way 00:00:19.290 --> 00:00:23.760 that multifactor authentication is implemented within AWS, 00:00:23.760 --> 00:00:25.620 let's just refresh our knowledge 00:00:25.620 --> 00:00:28.620 on exactly why MFA is needed. 00:00:28.620 --> 00:00:30.210 So consider for a moment the way 00:00:30.210 --> 00:00:34.080 that you usually log in to any web-based applications. 00:00:34.080 --> 00:00:37.350 Generally, you use usernames and passwords.

00:00:37.350 --> 00:00:40.320 And if both of these are leaked, then anyone can be you. 00:00:40.320 --> 00:00:43.050 Anyone can take your username and password 00:00:43.050 --> 00:00:45.420 and use them to log in to an application 00:00:45.420 --> 00:00:48.300 and impersonate you as an identity. 00:00:48.300 --> 00:00:50.940 So what we need is a way to improve this.

00:00:50.940 --> 00:00:53.250 So there's another term which I want to introduce 00:00:53.250 --> 00:00:56.790 and that term is known as a factor or factors. 00:00:56.790 --> 00:01:00.840 So factors are pieces of evidence which prove identity 00:01:00.840 --> 00:01:03.120 and there are different types of factors. 00:01:03.120 --> 00:01:06.630 So when you hear the term single-factor authentication, 00:01:06.630 --> 00:01:09.510 this means to use just one of these types 00:01:09.510 --> 00:01:11.940 or one of these types of factors.

00:01:11.940 --> 00:01:16.320 Multifactor authentication is when you use multiple factors 00:01:16.320 --> 00:01:18.210 or multiple types of factors 00:01:18.210 --> 00:01:20.280 to log in to an application. 00:01:20.280 --> 00:01:22.650 Now, there are four common factors that you'll use 00:01:22.650 --> 00:01:25.590 to log in to any web application. 00:01:25.590 --> 00:01:27.300 First is knowledge, 00:01:27.300 --> 00:01:29.280 and this is something that you know.

00:01:29.280 --> 00:01:33.420 So the knowledge factor includes usernames and passwords. 00:01:33.420 --> 00:01:35.880 The second type of factor is possession 00:01:35.880 --> 00:01:37.500 and this is something that you have, 00:01:37.500 --> 00:01:42.210 so a bank card or an MFA device or an MFA application. 00:01:42.210 --> 00:01:46.920 So consider what you do when you use a bank card at an ATM.

00:01:46.920 --> 00:01:48.510 You have to have the bank card, 00:01:48.510 --> 00:01:50.250 you put it inside the ATM, 00:01:50.250 --> 00:01:52.500 and then you need to enter a pin. 00:01:52.500 --> 00:01:55.610 So this is an example of multifactor authentication. 00:01:55.610 --> 00:01:58.050 In this case, you're using two factors: 00:01:58.050 --> 00:02:00.180 something that you have, the bank card, 00:02:00.180 --> 00:02:02.430 and something that you know, your pin.

00:02:02.430 --> 00:02:04.320 The next factor is inherent. 00:02:04.320 --> 00:02:05.940 So this is something that you are, 00:02:05.940 --> 00:02:10.110 so a fingerprint, a face scan, voice identification, 00:02:10.110 --> 00:02:11.340 or an iris scan. 00:02:11.340 --> 00:02:14.310 These are all examples of the inherent factor.

00:02:14.310 --> 00:02:16.560 And then lastly, we have location. 00:02:16.560 --> 00:02:19.290 So this can be either a physical location, 00:02:19.290 --> 00:02:22.740 so a particular set of coordinates anywhere in the world, 00:02:22.740 --> 00:02:25.050 or it can be the type of network 00:02:25.050 --> 00:02:28.230 that you're currently logged in to to access a system. 00:02:28.230 --> 00:02:30.450 So whether you're logged in to the corporate network 00:02:30.450 --> 00:02:33.000 or using your home wifi network.

00:02:33.000 --> 00:02:35.070 Various different security procedures 00:02:35.070 --> 00:02:38.070 might require a certain location, 00:02:38.070 --> 00:02:39.690 which is a factor to use 00:02:39.690 --> 00:02:42.120 as part of an authentication process. 00:02:42.120 --> 00:02:42.953 So in general, 00:02:42.953 --> 00:02:46.020 the more factors that your authentication process uses, 00:02:46.020 --> 00:02:47.910 this means more security 00:02:47.910 --> 00:02:51.390 and it also means that it's harder to fake your identity. 00:02:51.390 --> 00:02:53.670 So imagine if you could only log in to a system 00:02:53.670 --> 00:02:55.380 using something that you know, 00:02:55.380 --> 00:02:56.940 so username and password, 00:02:56.940 --> 00:02:58.110 something that you have, 00:02:58.110 --> 00:03:02.160 so a security card or an MFA device or application, 00:03:02.160 --> 00:03:05.970 imagine if you also needed a fingerprint or a facial scan 00:03:05.970 --> 00:03:07.710 and you could only log in 00:03:07.710 --> 00:03:10.620 within the confines of your corporate network.

00:03:10.620 --> 00:03:13.320 That would mean a really secure login process, 00:03:13.320 --> 00:03:16.110 but it would mean it's not very convenient. 00:03:16.110 --> 00:03:18.480 So generally, we're trying to achieve a balance 00:03:18.480 --> 00:03:21.060 between convenience and security. 00:03:21.060 --> 00:03:23.700 Now, at this point, I want to show you the specific process 00:03:23.700 --> 00:03:28.230 of how multifactor authentication is implemented within AWS.

00:03:28.230 --> 00:03:29.850 So we're going to step through the process 00:03:29.850 --> 00:03:34.770 of exactly how AWS handles the addition of a second factor. 00:03:34.770 --> 00:03:38.460 So this is an MFA device or an MFA application. 00:03:38.460 --> 00:03:40.770 So we start with an AWS account.

00:03:40.770 --> 00:03:42.900 And by default, you log in to this 00:03:42.900 --> 00:03:45.090 with a username and password. 00:03:45.090 --> 00:03:47.340 These are both things that you know. 00:03:47.340 --> 00:03:48.210 So this is known 00:03:48.210 --> 00:03:52.140 as single-factor or one-factor authentication.

00:03:52.140 --> 00:03:54.900 Now, the issue, as I touched upon previously, 00:03:54.900 --> 00:03:56.670 is that if both of these leak, 00:03:56.670 --> 00:03:58.980 either because of an error on your part 00:03:58.980 --> 00:04:00.960 or because of malware on the machine 00:04:00.960 --> 00:04:02.550 that you are using to log in, 00:04:02.550 --> 00:04:05.310 then a bad actor can fake your identity 00:04:05.310 --> 00:04:06.900 and log in as you. 00:04:06.900 --> 00:04:09.390 Now, we improve this by using MFA. 00:04:09.390 --> 00:04:13.530 As a reminder, this stands for multifactor authentication.

00:04:13.530 --> 00:04:17.790 And MFA can be activated using a physical MFA device, 00:04:17.790 --> 00:04:20.010 which is a key fob style device 00:04:20.010 --> 00:04:22.740 which generates ever-changing codes, 00:04:22.740 --> 00:04:25.590 or you can use a virtual MFA device, 00:04:25.590 --> 00:04:28.020 which is added to an MFA application 00:04:28.020 --> 00:04:30.240 such as Google Authenticator, 00:04:30.240 --> 00:04:33.420 and these applications run on a phone or other device 00:04:33.420 --> 00:04:36.240 and can store lots of virtual MFAs. 00:04:36.240 --> 00:04:37.860 And this means that they can be used 00:04:37.860 --> 00:04:39.690 for lots of different services 00:04:39.690 --> 00:04:41.280 and lots of different accounts 00:04:41.280 --> 00:04:42.750 within those services. 00:04:42.750 --> 00:04:46.950 Now, to configure MFA within AWS for a specific identity, 00:04:46.950 --> 00:04:49.080 let's say the account root user, 00:04:49.080 --> 00:04:52.170 you activate MFA for that user.

00:04:52.170 --> 00:04:56.070 And when you do so, AWS generates a secret key, 00:04:56.070 --> 00:04:58.440 which is a randomly generated key, 00:04:58.440 --> 00:05:01.590 and it also generates other associated information 00:05:01.590 --> 00:05:04.020 such as the username it links to 00:05:04.020 --> 00:05:06.360 and the name of the service. 00:05:06.360 --> 00:05:09.420 This information needs to be eventually entered 00:05:09.420 --> 00:05:11.220 into an MFA application, 00:05:11.220 --> 00:05:13.230 such as Google Authenticator, 00:05:13.230 --> 00:05:14.662 and to make this easier, 00:05:14.662 --> 00:05:17.580 AWS use all of this information together, 00:05:17.580 --> 00:05:20.850 so the secret key and the additional information, 00:05:20.850 --> 00:05:22.830 to generate a QR code 00:05:22.830 --> 00:05:26.850 and this QR code encodes all of this information 00:05:26.850 --> 00:05:28.560 in a visual pattern. 00:05:28.560 --> 00:05:30.480 So once you've got this QR code, 00:05:30.480 --> 00:05:33.540 using the MFA application on your phone, 00:05:33.540 --> 00:05:34.920 you scan this code, 00:05:34.920 --> 00:05:37.230 which transfers the information 00:05:37.230 --> 00:05:39.720 into the MFA application.

00:05:39.720 --> 00:05:43.470 And this means there's now an entry in the application 00:05:43.470 --> 00:05:46.800 with a code which regenerates periodically. 00:05:46.800 --> 00:05:48.000 It's never the same. 00:05:48.000 --> 00:05:49.740 A new code is generated 00:05:49.740 --> 00:05:52.890 every single time the code refreshes.

00:05:52.890 --> 00:05:55.350 Now, the way to think about the application 00:05:55.350 --> 00:05:59.370 is that it holds one or more virtual MFAs 00:05:59.370 --> 00:06:02.940 and each virtual MFA, as the name suggests, 00:06:02.940 --> 00:06:06.570 is an MFA device, only virtual. 00:06:06.570 --> 00:06:09.600 So if you have two users within AWS, 00:06:09.600 --> 00:06:13.410 then you would generally have two virtual MFAs 00:06:13.410 --> 00:06:16.200 and you can have, within sensible limits, 00:06:16.200 --> 00:06:20.460 as many of these as you want within your MFA application 00:06:20.460 --> 00:06:23.880 all representing identities in various services 00:06:23.880 --> 00:06:27.840 such as AWS, Google Mail, Azure, GCP, 00:06:27.840 --> 00:06:31.950 or any other cloud environments or web applications. 00:06:31.950 --> 00:06:33.780 Now, once you have the MFA configured, 00:06:33.780 --> 00:06:36.450 the next time you log in to AWS, 00:06:36.450 --> 00:06:39.690 as well as being required to enter the username and password 00:06:39.690 --> 00:06:42.360 for the specific user that you're using, 00:06:42.360 --> 00:06:46.230 you'll also be prompted to enter the MFA code showing 00:06:46.230 --> 00:06:49.170 for that one specific virtual MFA 00:06:49.170 --> 00:06:51.570 within your authenticator application.

00:06:51.570 --> 00:06:55.920 It needs to be the current code for the correct virtual MFA 00:06:55.920 --> 00:06:59.160 on your specific authenticator application 00:06:59.160 --> 00:07:02.160 on your phone or other device. 00:07:02.160 --> 00:07:04.770 This means in addition to the username and password, 00:07:04.770 --> 00:07:06.510 which are both things that you know, 00:07:06.510 --> 00:07:09.570 so this means single-factor authentication, 00:07:09.570 --> 00:07:12.360 you now need to provide something that you have 00:07:12.360 --> 00:07:16.350 and this means your identity inside AWS is secured 00:07:16.350 --> 00:07:19.440 using multifactor authentication. 00:07:19.440 --> 00:07:21.930 Even if your username or password were leaked, 00:07:21.930 --> 00:07:23.940 in order to log in to AWS, 00:07:23.940 --> 00:07:28.320 that's only possible if you provide the MFA code as well.

00:07:28.320 --> 00:07:30.750 If you lose your MFA device, 00:07:30.750 --> 00:07:33.690 even though a bad actor has that device 00:07:33.690 --> 00:07:35.580 and has that MFA code, 00:07:35.580 --> 00:07:37.320 login would only be possible 00:07:37.320 --> 00:07:40.260 if they also know your username and password. 00:07:40.260 --> 00:07:41.760 You need all three. 00:07:41.760 --> 00:07:44.550 And in general, on most modern phones, 00:07:44.550 --> 00:07:48.480 the MFA application itself will also be protected 00:07:48.480 --> 00:07:50.970 with multifactor authentication.

00:07:50.970 --> 00:07:53.160 So generally, you'd need to have first logged in 00:07:53.160 --> 00:07:55.320 to the device using a pin code 00:07:55.320 --> 00:07:57.900 and then potentially needing a fingerprint scan 00:07:57.900 --> 00:07:59.370 or a facial scan 00:07:59.370 --> 00:08:03.150 in order to gain access to your MFA application. 00:08:03.150 --> 00:08:04.800 So this is a really effective way 00:08:04.800 --> 00:08:06.480 of adding additional security 00:08:06.480 --> 00:08:10.980 to any of your web applications, including AWS. 00:08:10.980 --> 00:08:13.380 Now, this is everything I wanted to cover in this lesson.

00:08:13.380 --> 00:08:15.990 This is a feature that you're going to be using constantly 00:08:15.990 --> 00:08:17.520 in any of my courses 00:08:17.520 --> 00:08:20.130 and if you use AWS in the real world. 00:08:20.130 --> 00:08:22.470 But with that being said, go ahead and complete this video, 00:08:22.470 --> 00:08:23.340 and when you're ready, 00:08:23.340 --> 00:08:25.803 I'll look forward to you joining me in the next.

## aws-accounts-securing-aws-account.txt

Welcome back and in this demo lesson I'm going to show you how to initially secure an AWS account. What you're going to do is attach a virtual MFA device to the account root user of the general account which adds an additional layer of security. Now before we begin let's explore what this means.

We're going to be working on the general AWS account with the account root user and let's pretend for a second it already has some resources which have been created within it, though for now our accounts are completely clean. Now with this example if you're trying to log into this general AWS account then so far you will have used the account root user and you will have provided the account root user email address and the associated password and this is known as single factor or one factor authentication because it's using one type of secret, in this case the password, something which Julie in this example knows. Now there's a problem with this method though if in some way the account root user credentials were leaked maybe via espionage or social engineering then a bad actor could use them and easily log into the account in Julie's place and potentially delete all of the resources in the account so all of the cat pictures which you've been storing inside AWS or create new resources to farm Bitcoin so something which will cost you money and make the clown lots of money in the process.

Now we can prevent this by using multi-factor authentication and this means adding a second factor something other than the secret which Julie knows. Now in addition to this we're using something that Julie has. A physical MFA device or virtual MFA device which is running within an application on her mobile phone.

Now it means that in order to log in an MFA code is needed. Something which is valid for a single use and changes every 30 seconds or so. Now this means that if our evil clown only has the username and password or if he has an older invalid code then he will be denied entry into the general account using the account root user.

In this case we're using two factors something that Julie knows so her password and something that Julie has. Now we could depending on the system add even more factors. Certain systems allow you to use biometrics such as a fingerprint or retinal scan which in this This example is something that Julie is, and that makes it even harder for anyone but Julie to access a sensitive system.

With AWS we can use an MFA token system, and that's what we're going to be configuring next, so let's move over to the console and get started attaching a virtual MFA device to the account root user of the general AWS account. So to configure that what we need to do is to click on this dropdown and then select security credentials. You're taken to a different area of the console and don't worry that it says identity and access management.

This is simply the console where you configure your security credentials but because we're using this drop down and because we're logged in as the account root user of the general AWS account then we're configuring the security credentials for the account root user. So scroll down to multi-factor authentication and then click assign MFA device. Now we need to give this MFA device a name so you can put anything here I'm going to pick something that makes sense to me but you can put something which makes sense to you for this specific authenticator and then you're allowed to choose an MFA device type.

Now the options that we currently have available we've got authenticator app, security key or hardware TOTP token. Now for this demo we're going to pick authenticator app so go ahead and select that option and then click on next. In order to set up this virtual MFA you need to click on show QR code and then scan the QR code with your virtual MFA application.

Now examples of these include the Google authenticator, 1Password, Authy or many more. I've included some examples attached to this lesson, but you do need to download an authenticator application for your mobile phone or desktop. Once you've done that, what you'll need to do is to click on 'show QR code', scan the code and it will create an entry within that virtual MFA application.

Now you will have entry for each identity in each account so at this point we're going to create a virtual MFA for the account root user of the general AWS account. Later in the course when you create the production account you'll be creating another entry within your MFA application for the account root user of the production AWS account and then later still you'll be creating another MFA for the IAM admin identity in both of those accounts so by the end of this part of the course you'll have four entries within your MFA application. One for the account root user of the general account, one for the account root user of the production account and then one for the IAM admin user in each of the general and production accounts for a total of four.

But now let's worry about setting this up for the account root user of the general account so click on show QR code scan that code and you'll be presented with an MFA code which constantly changes. Once you've done that you need to save that in your MFA application and then enter two consecutive codes in these boxes. So you'll see that once you scan this QR code and save it, it will generate a code which changes periodically and you need to enter two of those codes.

Now I'm going to keep all of this secret for security reasons but you need to follow this process. So click on show QR code, scan the code with your authenticator application, enter the first code into box number one and then the second code into box number two. Now this might take you a couple of seconds so pause the video, you'll need to wait for your authenticator application to generate two different codes and once it has, go ahead and click to move on to the next screen.

That process has been completed successfully and you should see this positive dialogue saying you have successfully assigned a virtual MFA. And then click on this drop down and we're going to test that the process has been completed successfully. So go ahead and click on sign out and then click to log back in to the console.

You'll need to make sure that root user is selected and then enter your account root user email address for the general AWS account. Go ahead and click to move on. You might be again prompted for another security check.

Just enter those characters and if you can't see them clearly click on refresh or click on the speaker symbol to do this with audio. Click to move on. You'll need to enter your chosen password and then click.

This time you'll need to enter your MFA code and this will be contained within your authenticator application. So locate that code and enter it and this This code changes periodically and it's only valid for a one time use. So it means that even if your account email address and password were leaked, nobody can log into this account root user without a valid MFA code.

Go ahead and click to log into the console and you'll be successfully logged back into the AWS console. Only now to do this from this point onwards, you'll need something that you know, which as the account root user email and password as well as something that you have which is the one time password. Now again for production usage you should probably use a hardware token but for setting up training accounts using a virtual MFA device is absolutely fine and again I've attached some good quality software applications to this lesson which you can use for this training or for any other MFA style applications.

Now at this point we've finished everything that we needed to do in this demo lesson. Remember when you're setting up any other AWS accounts and any other identities within those accounts you need to add another entry within your MFA application. Don't reuse the one-time password that you've just added for the account root user of the general account you need to add additional entries into your authenticator application for any other identities in any other AWS accounts.

and by the end of this section of the course you should have a total of four one each for the account root user of the general and production accounts so two for the account root users of those accounts and then one each for the IAM admin user of the general and production accounts so two, one each for each of those for a total of four so by the end of this section you should have four virtual MFAs configured and that's a good thing to check once you've completed this section of the course. But at this point that's everything I want you to do in this demo lesson so go ahead and complete this video and when you're ready I look forward to you joining me in the next.

## aws-accounts-creating-a-budget.txt

Welcome back and in this demo lesson we're going to step through how you can handle basic cost management of an AWS account. I'm going to explain what the AWS free tier is and we're going to set up a budget within our AWS account so we can closely monitor any spend as we move through the course. Now it's my intention this course will stay as much as possible within the AWS free tier but you do need to know how to effectively monitor usage within the platform.

Now attached to this lesson is a link which details all of the offers which are available within the AWS Free Tier. Now products within AWS either provide free trials which give you short term free trial offers, some services provide access for 12 months for free, some services are always free or a certain allocation. Now this page, the AWS Free Tier Overview, gives you an overview of all of the different free elements of all of the AWS products.

So you can see, for example, that for the first 12 months you're provided with 750 hours per month of access to certain EC2 instances. instances. You can see that you receive five gigabytes of standard storage on Amazon S3 and you're given 750 hours of certain types of Amazon RDS instance.

Now many products within the platform give you access to a certain allocation and this page details all of those allocations so it's definitely something that you should take a look at. Now inside AWS accounts you have access to a number of tools which provide really granular access to what services are consuming things within your AWS account. You're able to see services which transfer data, you're able to see if you're consuming space within S3 buckets and what region, you get access to very granular tooling within AWS.

Now to do this just make sure that you are logged in as the account root user of the general AWS account and then click on this drop-down and go ahead and click on billing dashboard. This is going to take us to the billing console which is the central point that you need to use to interact with any of the AWS billing services. What you're able to do is to click on bills and you can click on the date drop down and see an overview of any usage for both the current un-billed month as well as any previous bills.

You're also able to see any payments, any any credits. Further down the line, you can see cost and usage reports. You're able to go into the cost explorer product and get really granular views over any spends within your account.

And this page will provide a really good overview of the spend last month, the month to date, as well as a forecast spend for the current month. It's a really good way to see how much your estimated bill is likely to be. So as we move through the course, This is something that I want you to come back to and evaluate your usage on a constant basis.

What I also recommend to all of my students is to click on billing preferences and then check all of these boxes. So check that you want to receive a PDF invoice by email. By default, you will receive an email every month to let you know that your bill is ready.

But if you don't check this box, then you have to log into the AWS account to see that bill. If you check this box, it will be delivered along with the email. So that's really useful.

You should also check receive free tier usage alerts, because this will notify you if you're approaching any of the usage thresholds for the AWS free tier. And you should go ahead and put your email address in this box to receive those alerts. And then finally, you should probably go ahead and check this final box to receive billing alerts.

Now, what I want to do at this point is to create a cost budget. So on the menu on the left, go ahead and click on budgets. Budgets are a really effective way which allow you to monitor your spend and configure alerts as you approach certain percentages of that desired spend.

So it's a really good way to manage the costs of your AWS account. So let's go ahead and click on create a budget. Now under budget setup, make sure that you select to use a template.

You can click on Customize Advanced, but for this course we're going to use a template. Now below there are a number of different templates that you can choose to use. Now what you pick depends on what budget you have available for your training.

The one that's selected right now is the Zero Spend budget. And this will inform you if you have any costs on your AWS account. Now this is useful if you want to ensure that you stay entirely within the free tier.

You'll be notified if you have any spend on the AWS account. The other option is to pick a monthly cost budget where you can specify an amount of money per month that you're willing to spend. And you'll be notified if you exceed that amount.

So at this point you have two choices. You can either specify a zero spend budget or a monthly cost budget. So go ahead and pick whichever one of these that you want to use.

I'm going to choose a monthly cost budget, but if you aren't able to spend an amount of money reliably, then go ahead and pick the zero spend budget. Once you do that, you'll need to name your budget. If you are choosing the cost budget, then directly under that you'll need to specify the amount of money that you want to spend.

In my case, I'm going to pick 10. So if I spend more than 10 USD, I'm going to be notified. And then in either case whether you're using the zero spend or the monthly cost budget you'll need to enter email recipients.

So go ahead and enter your email in this box. This is the email address that will receive any notifications if you exceed this budget. And then once you've entered all that, scroll down and click on 'Create Budget'.

Now at this point the budget's created, everything should look good and it will take up to 24 hours to populate all of your spend data. That's all good, all I want to make sure is that you know how to create a budget. As I mentioned before for this course we're going to keep it as much in the free tier as possible but if you are creating production accounts which have real business usage then you do need to get into the habit of creating budgets.

Now at this point that's everything that you'll need to do for this demo. Go ahead and complete the video and when you're ready I'll look forward to you joining me. in the next.

## aws-accounts-creating-the-production-account.txt

Welcome back. And at this point you've successfully created and configured the general AWS account which you'll be using throughout this course. Now I mentioned earlier in the course that to make this realistic, to give you the experience of working with a multi account environment, we're going to be using different AWS accounts and connecting them together using an AWS organization.

Now I'll be covering what AWS organizations is later in the course, but next I'll want you to go ahead and create a brand new Production AWS Account. So this is a completely separate account than the general account that you've created up until this point of the course. As you move through the course, certain demos will require multiple AWS accounts in order to demonstrate certain technologies.

For example, cross account storage using the simple storage service. Whenever we're using demos, which only require one account, we'll be using the general account. Any demos which require multiple accounts will also be using the production account.

So at this point, I want this to be a do it to yourself lesson. I want you to go ahead and create the production AWS account with exactly the same configuration as you have done for the general account. Now creating and figuring the production account will involve a number of steps.

First, you'll need to decide on an email address to use for the production AWS account. Now because this is a brand new account, a completely separate AWS account from the general AWS account, you'll need to use a unique email address. Now don't forget the Gmail '+' trick that are detailed earlier in this section of the course.

This will allow you to use the '+' sign in an email address. And this will mean that you can generate an infinite number of unique email addresses which all go back to the same Gmail account. So you'll need to configure an email address that's different from the one that you used for the general account and you'll need to use this for the production account.

Once you've got that email address configured, then you'll need to go ahead and follow the exact same signup process to create the production AWS account. Now you can use most of the same value, so the same, the same address, you'll need to choose a different account name, I recommend using -production instead of -general like you used when you are creating the general account, but you can use on the whole the same details. You'll be able to use the same credit card.

You should pick the same support plan, but at the end of that process, you'll be logged in to the AWS console of the production AWS account, a brand new account. You'll also need to follow the same steps to secure the production AWS account which means adding multifactor authentication to the account root user of that production account and you'll need to log out and log back in to test it. Now make sure when you're adding MFA to the account root user, you are adding the MFA as a separate code or separate profile within your multifactor authentication application.

So whether you are using Google authenticator, or One Password, or Authy or any of those other tools, make sure that you're adding the MFA for the account root user of the production AWS account as a separate MFA within that application. Don't try to use the same MFA setup that you used for the general AWS account. Once you've added MFA, you'll need to go to the billing console, go to billing preferences and check the same three check boxes that you did for the general account, also adding your email address for any alerts.

Then you'll need to go to budgets and create a budget also the same way that you did for the general AWS account. If you've forgotten any of those steps, feel free to re-watch the previous lessons and just adjust the configuration for the production AWS account. You also need to remember to go into the account settings of the production AWS account and enable IAM User and Role Access to billing.

And then optionally, if you did this in the general account, you can also add those three different account contacts to that same account screen. But remember, this is optional. Now I want you to follow all this process yourself without any guidance from me because I want you to be comfortable setting up a brand new AWS account.

I'm super confident that you can do this. You rock, you followed every step of the process from beginning to end for the general account. So you can just do the same thing for the production account.

So at this point, go ahead and complete this video and then create and configure the production account. And I look forward to seeing you when you've completed that in the next lesson of the course.

## aws-accounts-iam-basics.txt

Welcome back and in this lesson, I want to introduce a really important AWS service and that's Identity and Access Management known as IAM, or IAM. Now I have a whole section of the course dedicated to this service later on, but for now I just want to introduce it. Now, I want to make this lesson as brief as possible, so let's just jump in and get started.

To understand why IAM exists, we need to understand the current identity situation of the AWS accounts that you've created for the course so far. The accounts that you've created have an associated Account Root User, and the account trusts this user fully. This is why the Account Root User has full unrestricted access to the account.

Now the AWS account and the Account Root User can really be thought of as the same thing. The Account Root User gets created with the account, and it can't be restricted in any way. In most real world situations, you want to be able to grant other people in your organization access to your AWS account.

This might be users, groups, or even applications which they create or manage and you generally want to restrict the access that these people, groups or applications have. It's always best practice to only give the permissions required to do a job, or perform a task and this is called least privileged access. Only having a single identity in the account is also problematic.

If the credentials are ever leaked for the Account Root User, then the damage could be account wide. Remember, it's not possible to restrict the permissions or the access rights that the Account Root User has, and so if the credentials are leaked, then potentially all regions and all services in those regions are at risk. What we need is a way to allow more control over what access is given to our AWS accounts, and that is where IAM comes in handy.

Every AWS account comes with its own running copy of IAM, its own database. Now IAM is a globally resilient service, so any data is always secure across all AWS regions. Remember that one because it'll probably feature on the exam, but also understand that the IAM that you see in each of your accounts is your own dedicated instance of IAM separate from other accounts and from anyone else's accounts.

Your AWS account trusts your instance of IAM. IAM like the Account Root User can do anything in the account. Now there are some restrictions, but this is generally around billing control and account closure.

Operationally, the IAM of your account is trusted fully by the account and so IAM as a service can do as much as the Account Root User. Inside IAM, you can create other identities. So there are different types of identities and you can create many of these, so you're not limited to the single Account Root User anymore, you can create multiple identities.

And IAM can allow these identities to do certain things. Now because a single AWS account trusts IAM, if IAM allows one of the identities that it manages to do something, the account automatically trusts that identity in the same way that it trusts IAM and I'll show you how this works when I talk in more detail about access rights and permissions as we go through the course. Let's quickly look at some of the different things that IAM lets us create.

IAM lets you create three different types of identity objects, we've got IAM User, IAM Groups, and IAM Roles. They each have their own specific users and by the end of this course, I'll make sure that you really understand when to use each, but at this stage, I just want to quickly introduce them. Now users represent humans or applications that need access to your AWS account.

If Bob from accounting needs access to AWS billing, or Jane from infrastructure needs access to create and terminate EC2 virtual machines known as instance, then generally Bob and Jane will have an IAM User created inside the IAM service. But IAM user can also be used for applications. If you have a backup application, it might also use an IAM User to log into your account and do those backups.

Next we've got groups and groups are just collections of related users. If you want to manage all development team users, you might create a development team group and add the IAM User to that group, same for finance or HR. Then we've got IAM Roles and IAM Roles are fairly tough to understand at first, but they can be used by AWS services or if you want to grant external access to your account.

Now you'll see later in the course how you can use IAM Roles to give an EC2 instance itself access to AWS services. Roles are generally used when you want to grant access to services in your account to an uncertain number of entities. So for example, if you want all EC2 instance in your account to be able to access the simple storage service which I'll be covering soon, then you can create a role which grants access to the simple storage service and then allow instance to use that role.

So generally you pick IAM Users when you can identify the individual thing that will log in to that user. So if it's an individual person or an individual application, then generally you'll use users. Roles tend to get used when the number of things is uncertain.

So if you want to grant users of external accounts access to say a simple storage service bucket, or if you want to grant an uncertain number of EC2 instance access to certain services in your account, or if you want to allow AWS services themselves to interact on your behalf, then you'll generally use a role. Now it is really difficult to explain what a role does and when you'll use it by just covering the theory. So later in the course, I'm gonna give you plenty of examples of the types of situations when you would and wouldn't use roles.

Now there's one more concept that I want you to be super clear on, and that is an IAM policy or a policy document. IAM lets you create these policies which are essentially objects or documents which can be used to allow or deny access to AWS services when and only when they're attached to IAM Users, groups, or roles. So policies on their own, do nothing, they simply define, allow or deny rights to certain services only when you attach the policies to other identities, so users, groups, and roles do they have any effect Now at a high level, IAM has three main jobs.

Firstly, it's an Identity Provider or an IDP. It lets you create, modify and delete identities such as users and roles and it also authenticates those identities. So when anyone attempts to make a request to AWS, they're known as a security principle and what they need to do is to prove their identity.

I might claim to be an IAM User called Adrian in my account, but I need to be able to prove this. And so IAM authenticates me and generally this is using a username or password, but as you'll see later in the course there are other methods of authentication. Now, assuming I prove my identity, IAM then authorizes me, or not to access AWS resources, so I'm either allowed or denied access to certain things.

And this is based on policies associated with the identity that I authenticate with. Really try and remember these terms. So you've got an ID provider which is a service that allows you to create and manage identities.

You've got the authentication process which is where you are challenged to prove that you are the identity that you are claiming to be. And then once you're authenticated, you become an authenticated identity and then you're authorized or not to access AWS services. Now we're almost done, I just have a few points I want you to remember And then it's demo time.

IAM is provided for free there are no costs associated with creating users, groups, or roles. There are limits on how many of each you can have, and some of these limits actually matter for real world usage and for the exam, so I'm gonna go into more details on these later. IAM is a global service, it's got one global database for your account and it's globally resilient.

So it can cope with the failure of large sections of the AWS infrastructure. Now IAM only controls what its identities can do. So IAM User or roles which you create in IAM, it allows or denies those identities to do things via policies.

It doesn't allow direct control over external accounts, or users, so you can't use IAM to control what an external user in an external account can do. IAM only controls local identities in your account. Lastly, IAM lets you make use of identity federation and multifactor authentication.

Now don't be scared of these terms for now, identity federation lets you take identities that you already have. For example, your business's active directory, or WEB identities such as Facebook, Twitter, Google, and more and then use these indirectly to access AWS resources. Don't worry about understanding it now, I just wanted to introduce the term and I'll be covering it extensively later in the course, including some demos to let you experience it yourself.

I've already showed you multifactor authentication, we've added it to the Account Root User of the accounts have created. So when the Account Root User needs to log into that AWS account, they need to input the one time password that's generated by the MFA application on our phones. And what you can see on the bottom right of your screen now is just an example of a physical MFA device.

So this is a physical device that you'd carry with you along with your wallet and keys that would generate these one time passwords that you'd need to use when you log in. Okay, so that's all of the IAM basic theory that I wanted to cover, it's demo time. Over the next few lessons, I'm going to show you how you can further secure your AWS accounts that you'll use for this course.

I'm going to demo setting up IAM and creating an IAM admin user. Now, the reason we're gonna do this is to create a second user that will have full permissions on the AWS account. So the IAM admin user in many ways is gonna function just like the Account Root User, but it will use IAM.

Now the reason we are doing this is so that we can stop using the Account Root User. Remember, we only have one Account Root User and it's not possible to restrict the permissions of this user. And so best practice is that it's only used to perform the initial account set up.

Afterwards, we need to utilize IAM User, rather than the Account Root User, so that's what I'm gonna demonstrate. Now at this point once we've got this IAM admin user throughout the course as we need additional identities, we'll use this IAM admin user to create those additional identities which will be giving less permissions. So remember it's always best practice to only get the permissions required to do a specific task.

And so if I'm demonstrating a certain product or technology, generally we're gonna be using an IAM User that has just enough access rights to perform that task. So just like we did with the Account Root User, we're gonna create an IAM admin user in each of the course AWS accounts, so that's what's coming up next. So at this point feel free to complete this video and when you're ready, join me in the next for the demo.

## aws-accounts-adding-iamadmin-to-general-account.txt

Welcome back and in this demo lesson we're going to further secure our general AWS account and we're going to do that by creating an IAM identity which you're going to use for the remainder of the course. In general we don't want to use the account root user for anything for production usage or even while using this account for training. It's not possible to restrict the account root user, you can't delete it or recreate it and so we should almost never use it.

Normal process when you finished creating an AWS account should be to create a normal admin user, which will be given full control over the account and it will replace your usage day to day of the account root user. So we now have this general AWS account. We have an account root user for this AWS account and we've secured it with one time password capability.

But now what we're going to do is set up an IAM identity with admin permissions that we'll be using from this point onward in the course. So to do that, click in the services search box at the top and type IAM and then click IAM to move to the IAM console. If you're going to sign on with any IAM identities, then you need to use a sign in URL for IAM users.

And right now you'll see that it's in this format. It's HTTPS and then your account ID, which is unique to you, and then .signin.aws.amazon.com/console. Now you can set an account alias.

By default, this is set to your account ID, but we can make this sign in URL a little bit more friendly by setting an alias. And I like to keep this theme of general and production so that we can see which account it is that we're logging into. So we're going to set an account alias.

Now this account alias needs to be globally unique. So you need to set it to something which makes sense and has the word general in, but also is specific to you. So to create this alias, go ahead and click on create.

And then you need to enter your preferred alias in this box. and assuming that nobody else has used this alias, I can go ahead and click to save those changes. There we go, I'm able to create the alias that I want, so that's great.

You need to follow the same process, but pick a unique alias for you. Just make sure that it has the word "General" within it, so it's nice and easy to identify which AWS account you're logging into. Next we're going to go ahead and create the IAM identity, which we're going to be using from this point onward in the course.

and again, each IAM identity that we create is specific to the AWS account that it's created within so we're going to create an IAM identity called IAM admin but we'll be creating one in this lesson for the general AWS account and then later in this section you'll also be creating a similar identity for the production AWS account and these, just like the account root users, are completely separate identities. So go ahead and click on users, and then click on add users. Now for the username we're going to choose IAMADMIN.

This doesn't have to be unique globally, only within this account. So you won't currently have an identity called IAMADMIN, so you can also call your user IAMADMIN. Now we are going to be granting this user access to the AWS Management Console, so check this box.

And then because AWS are slowly introducing the Identity Center as their recommended place to create identities within AWS, you're offered the choice between creating a user in the Identity Center or creating an IAM user. Now so that you have experience of both, at this point we're going to create an IAM user later in the course you'll get some experience with the identity center but for now go ahead and click I want to create an IAM user and then we need to set a console password for the IAM admin user of the general AWS account. Now again you can use a password manager to auto generate this on your behalf but you do need to make sure that you note it down.

So click on custom password and then enter your chosen password within this box. I'm going to choose to generate a password using my password manager and then I'm going to uncheck users must create a new password at next sign in because I don't want to have to change the password when I first log in to the account and I suggest you do the same. So uncheck this box and then click to move on.

Now we need to give this identity some permissions. Initially it won't have any permissions except those to change the password and basic interaction permissions for the AWS console. So we need to give it admin permissions so go ahead and click attach existing policies directly.

You could add this user to a group which might have existing permissions or you could copy the permissions from an existing user. In our case though because we don't have either of these already configured we're going to attach an existing policy directly. I'll be talking about all this functionality elsewhere in the course.

For now though, locate administrator access which is a policy which grants full admin control over this AWS account, check the box and this will mean that this managed policy is going to be associated or attached to this IAM user and then click to move on and then you can go ahead and click to create the IAM admin user. You should see that this has been created successfully and you're even able to click to send an email with login instructions to this user but we're not going to do that we're just going to go ahead and click return to users list and then close down any extra dialogue. Now at this point go ahead and click on dashboard.

What we need to do now is to test that we can successfully login as this IAM identity. Remember we want to use this for the remainder of the course rather than use the account root user of the general AWS account. So what I want you to do is to copy the sign in URL for IAM users into your clipboard and you should probably note this down somewhere safe because this is going to be the URL that you'll use whenever you want to log in to the general AWS account using this IAM user from now on.

So make sure that that's copied into your clipboard and then just go to that URL so paste that into your address bar and then open it. Now this is going to log you out of the account root user and present you with a slightly different login screen, in this case sign in as an IAM user. You'll see that this box has been pre-populated and it will either have the account ID or the account alias.

Because I created an alias you'll see that it's using my alias, in your case it should be different. Go ahead and enter IAM admin in the IAM username box then you'll need to enter the password that you picked in the previous step for the IAM admin user of the general AWS account. Once you've entered all of that information go ahead and click on sign in and now you're logged into the management console but this time instead of using the account root user of the general AWS account this time you're using an IAM user.

If you click on this drop-down you'll be able to see that you're using IAM user IAM admin and it lists your account number next to my account but it's easy to know that we're logged in as an IAM identity because it says it at the top of this drop-down. Now this IAM identity has administrator access and so it does have full control over this account the same level of access as the account root user of this AWS account but from this point forward we're going to be using this account rather than the account root user. Now because this is an admin account we do need to fully secure it.

So we need to set up one-time passwords in the same way that we did for the account root user. So to do that click on this drop down and go to my security credentials and we need to follow the same process that we did for the account root user. So scroll down and now we need to click assign MFA device under multi-factor authentication.

Remember because this is done per identity within each AWS account, we don't currently have one assigned because previously we set the one up for the account root user. We need to set this up again with a new one-time password profile in your software application for this specific identity. So we're not reusing the one that we previously set up for the account root user.

Now we need to give this MFA device a name. So you can put anything here. I'm going to pick something that makes sense to me.

Just make sure that it has I am admin somewhere in that name to help you distinguish from the account root user MFA device name. And then you're allowed to choose an MFA device type. Now the options that we currently have available, we've got Authenticator App, Security Key or Hardware TOTP Token.

Now for this demo we're going to pick Authenticator App. So go ahead and select that option and then click on Next. And you need to follow the same process.

You'll need to click Show QR Code and then scan that QR Code as a new entry within your Authenticator application. Don't reuse the one that you already have. Once you've scanned that QR code and created the new entry in your authenticator application, the new entry for the IAM admin user of the general AWS account, then you'll need to enter two consecutive MFA codes that are generated by this new entry.

And again this may take a few moments to do because you need to enter two consecutive codes and once you've done that you can click on add MFA and then we need to log out and log back in again to test this one-time password. So click on this drop down and click on sign out. You'll need to once again use the URL that you noted down in the previous step which is the sign in URL for IAM identities of the general AWS account.

You should see the account ID or account alias pre-populated once again. Make sure that it is your alias for your general AWS account. Enter IAM admin for the IAM username.

Once again you'll need to enter the password that you chose. Click on sign in. This time you'll be prompted for a one-time password because that's what we've just set up.

So enter that in this box and then click to login to the AWS console. And there we go we now require a one-time password as well as the username and normal password to log in to this IAM admin user. Now just to reiterate what we've done we've created a separate identity so IAM admin within the general AWS account so this is a separate identity from the account root user of the general AWS account.

From this point forward we won't be using the account root user of the general account we'll be using the IAM admin identity of the general account. Now because this is an administrator user just like we did for the account root user of the general account we've configured multi-factor authentication for this IAM admin identity. It's a separate entry in your authenticator application so now you should have two.

One for the account root user of the general account and one for the IAM admin user of the general account. And this means now that in order to log into this IAM admin identity of this general AWS account you need the sign in URL, the username, the password and the one-time code. Now at this point that's everything that you need to do within this demo lesson.

Go ahead and complete this video and when you're ready I'll look forward to you joining me in the next.

## aws-accounts-adding-iamadmin-to-production-account.txt

Welcome back and in this demo lesson we're going to be following on from the previous demo lesson only this time we're going to be creating the IAM admin identity inside the production AWS account. So what I'll need you to do is make sure that you're logged into the production AWS account using the account root user. It should say production on this drop down at the top.

While you're doing that, also get into the habit of making sure that you have the US-East-1 region selected in this dropdown at the top right of the screen. We're going to be following exactly the same process to create the IAM admin user. So move across to the IAM console.

The quickest way is to click in the search box at the top and type "IAM" and then click to move across to the IAM console. And we need to go ahead and create an account alias for the production AWS account So go ahead and look on the right hand side of the screen and click on create Now you want to make sure that this production account alias is in a similar format to the one you created for the general AWS account And instead of general I'll be using production Again this needs to be globally unique, it should mention production and you should use the same structure as you used when creating your general account alias. So go ahead and enter the alias and click on save changes.

Once you've done that go ahead and note this down somewhere safe because you'll need it whenever you want to log in to the production AWS account using an IAM identity. Now that we've set that we can click on users and go ahead and create the IAM admin user for the production AWS account. Now for the username we're going to choose IAM admin.

This doesn't have to be unique globally only within this account so you won't currently have an identity called IAM admin so you can also call your user IAM admin. Now we are going to be granting this user access to the AWS management console So check this box. And then because AWS is slowly introducing the identity center as their recommended place to create identities within AWS, you're offered the choice between creating a user in the identity center or creating an IAM user now, so that you have experience of both at this point, we're going to create an IAM user later in the course, you'll get some experience with the identity center, but for now, go ahead and click I want to create an IAM user and then we need to set a console password for the IAM admin user of the production AWS account.

Now again you can use a password manager to auto generate this on your behalf but you do need to make sure that you note it down. So click on custom password and then enter your chosen password within this box. I'm I'm going to choose to generate a password using my password manager and then I'm going to uncheck "Users must create a new password at next sign in" because I don't want to have to change the password when I first log in to the account and I suggest you do the same.

So uncheck this box and then click to move on. Now we need to give this identity some permissions. Initially it won't have any permissions except those to change the password and basic interaction permissions for the AWS console.

So we need to give it admin permissions. So go ahead and click attach existing policies directly. You could add this user to a group which might have existing permissions or you could copy the permissions from an existing user.

In our case though, because we don't have either of these already configured, we're going to attach an existing policy directly. I'll be talking about all of this functionality elsewhere in the course. For now though, locate administrator access which is a policy which grants full admin control over this AWS account, check the box, and this will mean that this managed policy is going to be associated or attached to this IAM user, and then click to move on.

And then you can go ahead and click to create the IAM admin user. You should see that this has been created successfully, and you're even able to click to send an email with login instructions to this user, but we're not going to do that. We're just going to go ahead and click return to users list and then close down any extra dialogue.

Now at this point, go ahead and click on dashboard. What we need to do now is to test that we can successfully log in as this IAM identity. Remember, we want to use this for the remainder of the course, rather than use the account root user of the production AWS account.

So what I want you to do is to copy the sign in URL for IAM users into your clipboard. And you should probably note this down somewhere safe and then just go to that URL. So paste that into your address bar and then open it.

Now this is going to log you out of the account root user and present you with a slightly different login screen. In this case, sign in as an IAM user. You'll see that this box has been pre-populated and it will either have the account ID or the account alias.

Because I created an alias, you'll see that it's using my alias. In your case, it should be different. Go ahead and enter "iamadmin" in the IAM username box.

Then you'll need to enter the password that you picked in the previous step for the IAM admin user of the production AWS account. Once you've entered all of that information, go ahead and click on Sign In. And now you're logged in to the management console, but this time instead of using the account root user of the production AWS account, now you're logged in to an IAM user of that same AWS account.

If you click on this dropdown, you'll be able to see that you're using IAM user IAM admin, and it lists your account number next to my account. But it's easy to know that we're logged in as an IAM identity because it says it at the top of this dropdown. Now this IAM identity has administrator access and so it does have full control over this account the same level of access as the account root user of this AWS account but from this point forward we're going to be using this account rather than the account root user Now because this is an admin account we do need to fully secure it so we need to set up one-time passwords in the same way that we did for the account root user So to do that click on this drop down and go to my security credentials and we need to follow the same process that we did for the account root user.

So scroll down and now we need to click assign MFA device under multi-factor authentication. Remember because this is done per identity within each AWS account we don't currently have one assigned because previously we set the one up for the account root user. We need to set this up again with a new one-time password profile in your software application for this specific identity so we're not reusing the one that we previously set up for the account root user.

Now we need to give this MFA device a name so you can put anything here I'm going to pick something that makes sense to me just make sure that it has I am admin somewhere in that name to help you distinguish from the account root user MFA device name and then you're allowed to choose an MFA device type. Now the options that we currently have available we've got authenticator app, security key or hardware TOTP token. Now for this demo we're going to pick authenticator app so go ahead and select that option and then click on next and you need to follow the same process.

You'll need to click show QR code and then scan that QR code as a new entry within your authenticator application. Don't reuse the one that you already have. Once you've scanned that QR code and created the new entry in your authenticator application then you'll need to enter two consecutive MFA codes that are generated by this new entry and again And this may take a few moments to do because you need to enter two consecutive codes and once you've done that you can click on Add MFA.

And then we need to log out and log back in again to test this one time password. So click on this drop down and click on Sign Out. You'll need to once again use the URL that you noted down in the previous step which is the sign in URL for IAM identities of the production AWS account.

You should see the account ID or account alias pre-populated once again. Enter IAMADMIN for the IAM username. Once again you'll need to enter the password that you chose.

Click on sign in. This time you'll be prompted for a one-time password because that's what we've just set up. So enter that in this box and then click to log in to the AWS console.

And there we go, we now require a one-time password as well as the username and normal password to log in to this IAM admin user and now you've finished the account setup and account securing process. You have two AWS accounts, the general account and the production account. Both of those AWS accounts have their own individual account root user.

Both of them have an IAM identity, it's an IAM user called IAM admin and for IAM admin in both of those accounts you've configured MFA so we have four different identities split across two different accounts and all four identities are fully secured so you need a username a password and a one-time password. Now that's everything that you'll need to do in this demo lesson go ahead and complete the video and when you're ready I look forward to you joining me in the next.

## aws-accounts-iam-access-keys.txt

Welcome back, and by this point, you've got a set of working AWS accounts. You've configured the account security, added billing alarms, set up IAM and created an IAM admin user, and then completed all of that with multifactor authentication. So far, the AWS access that we've experimented with has been using the console UI in a web browser.

It is possible to access AWS using the command line, or even within other applications using APIs, or application programming interfaces. Authentication via the command line is not done via username, password, and MFA. It's done using IAM Access Keys, and that's the subject of this lesson.

So let's jump in and get started. Access keys are long-term credentials available within AWS. They're not the only type of long-term credential that you need to be aware of.

And all long-term credentials are used with IAM users. If you're authenticating to AWS, and you're doing so using an IAM user identity, then generally you'll either use a username and password when you're using the console UI, or access keys when you're using the command line interface. Now, they're called long-term credentials, because they don't change regularly or rotate.

You as the owner of the credentials have to explicitly change them. For example, updating your password. Access keys, in many ways, are similar to the username and password that you've used to this point, but there are a number of crucial differences.

An IAM user has one username and one password. It can't have anymore. Now, you can actually create IAM users which are only used for command line or API access.

And for those, you don't need to assign a password. So a password on an IAM user is actually optional. The important thing, though, is an IAM user can't have more than one username or one password.

Now, you can change the password, but it only ever has a maximum of one at a time. Now, if I ever refer to credentials throughout this course, and a username and password is an example of a set of credentials, there is normally a public part and a private part to those credentials. With usernames and passwords, the username is the public part of those credentials, and the password is private.

You don't need to worry too much if somebody knows your username, but if they know your username and password in conjunction, then that's known as a credential leak, and you're in trouble. An MFA is just another private part to your credentials. It makes it harder to leak the full credential set.

The first difference with access keys is an IAM user can have two sets, two access keys. It can have zero, one or two, but never more. Access keys can be created, deleted, made inactive, or made active.

And logically they default when they're created to be the active state. Now, like username and password credential sets, access keys are actually formed from two parts. The first part is the access key ID, and the second part is the secret access key.

The access key ID looks something like this, and the secret access key, that's longer and more complex. When you create access keys, and I use that term to refer to both parts of the credentials, AWS provides both of these to you, so you're given both the access key ID and the secret access key when you create that set of credentials. Now, once you're initially provided with both the access key ID and the secret access key, from that point onward, there's no ability to get access again to the secret access key.

AWS don't allow any future downloads of the secret access key part of a set of access keys. You can only ever see the access key ID, so it's especially important that that initial time, when you're provided with both, you note down the secret access key and store it safely and securely. When you make a request to AWS using the command line interface, you use both of these parts, so the public part and the private part.

Now, the access key ID, in many ways, is like an IAM username. And the secret access key is like a password. If you let anyone have access to the secret access key, then it can be used to act as that IAM user, so you need to be really sure that whenever you store the access key ID and the secret access key, you keep the secret access key safe and secure.

Now, if you do misplace the secret access key, or you concerned that your credentials have been leaked, then you can't change the secret access key. You need to delete the entire access key, so that's both parts, the access key ID and the secret access key, and then recreate it. And that will give you a brand new set of credentials, so a brand new access key ID and a brand new secret access key.

Now, if you have any command line interfaces or applications, which are configured to use access keys, and you make that set of credentials inactive or delete them, then the command line interface or application will stop working until you either make it active again or generate a new set, and then update those command line interfaces or applications with the new details. If you ever hear the term "Rotating access keys," it simply means to create a brand new set and remove the old one. It's no more complex than that.

That's why an IAM user can have two sets. Generally, if utilizing the first set, then to rotate them you'll create a second set, update all of your applications and command line utilities to that new set, and then delete the old one. Now, with the exception of the account root user, which can also have access keys, although that's not recommended, IAM users are the only identity which uses access keys, so the only identity that uses long-term credentials.

IAM roles don't use access keys. And I'll talk more about those in the IAM section of the course later on. For now, I just wanted to introduce the basics.

It's security related, and I want you to understand how it works from the offset. Now that you've learned the theory of access keys, it's time to experiment. Now, we're gonna have a demo, and in that demo, we're gonna create access keys in both the general AWS account and the production AWS account.

Once you've created those access keys, I'll be showing you how to download and configure the AWS command line tools. And as part of that process, you'll be using these access keys and configuring the command line tools to be able to connect to both the general and the production AWS account. So at this point, that's everything you need to do.

Go ahead, complete this lesson, and when you're ready, I'll see you in the next.

## aws-accounts-creating-access-keys-and-aws-cli-v2-tools.txt

Welcome back, and in this lesson, you're going to create access keys for both the iamadmin user in the general AWS account as well as the iamadmin user in the production AWS account, and then I'm going to step you through how to install the AWS command-line tools and configure those tools to access the AWS products and services using the access keys that you create. So this is going to put you in a position where you're able to use the AWS command-line utilities to interact with both the general AWS account and the production AWS account. Now we're going to start off in the general AWS account, so you'll need to be logged in as the iamadmin user of the general AWS account.

Assuming that you are, click on the account drop-down and then select Security credentials because this is where you configure access keys. So as I mentioned in the previous theory lesson, access keys can be created for IAM users, and this is what we're going to do here. So to create a set of access keys, it's as simple as scrolling down slightly and then clicking Create access key.

Now, when you create an access key, you'll need to specify what its intended use is. In this particular case, we're using it with the Command Line Interface, so we're going to go ahead and check this top box, then scroll down to the bottom and check the understanding confirmation box and click on Next. You'll need to give the access key a description, so I'm gonna go ahead and put LOCAL CLI IAMADMIN-GENERAL in this box.

If this were production, you might put the intended purpose or you might put who the access keys are assigned to. In any case, I'm not going to be using these access keys because I'm going to recreate them in a few moments. So I'm gonna go ahead and click on Create access key.

Now, when you create access keys, you're presented with two main pieces of information, the access key, which is this text on the left, and this is non-sensitive information. You can think of this much like a username. On the right though, we have the secret access key, and this is the secret part, the sensitive part.

Anyone with both of these pieces of information can access your AWS account, and so we need to be extremely careful with showing anyone the secret access key. So for security reasons, I'm not going to show this on screen. I'm gonna go ahead and click on Done, and we can see that now we have one access key created.

Now, when you've got a set of access keys, you can click on Actions and go to Deactivate and then confirm to deactivate that access key, and the reverse of this is you can click on Actions and then Activate to reactivate those access keys, and that's useful if you want to suspend access for any reason. Now, an individual identity can have two sets of access keys. So I could go ahead and click on Create access key again, check this box at the top, scroll down, check this understanding box, click on Next, and enter something into this box and click Create access key, and then I'll click on Done and Continue, and you can see that we have two different access keys created, but we can't create a third.

You can only have two access keys, either active or inactive, per identity within AWS. So I can't create another set of access keys. Now, the ability to have two is useful if you want to rotate access keys.

At this point though, I'm gonna go ahead and delete both of these because we're not going to use them. So click on Actions and then Delete. You'll see that you need to deactivate an access key before you can delete it, so I'll click on Deactivate, and then I'll need to paste in the access key ID into the box and click Delete, and I'll follow the same process for the other access key, and that puts us in the position where we have no access keys for this identity.

So now we're going to create the access keys properly that we're going to use with the Command Line Interface. So go ahead and click on Create access key again. Check the Command Line Interface box.

Scroll down to the bottom. Check this box and click on Next, and then enter a description. I'm going to use LOCAL CLI IAMADMIN-GENERAL, and then click on Create access key.

Now you're not able to get access to the secret access key from this point forward if you don't either show it or save it. So if you ever lose access to the secret access key, you'll need to regenerate the access keys. Now, what I suggest we do is click on Download .csv file, and this is going to save these access keys to a file called iamadmin_accesskeys.

Because these are the access keys for the general AWS account, I want you to go ahead and rename this file to iamadmin_accesskeys_general. Once you've done that, you can go ahead and click on Done, and now we're going to do the same for the production AWS account. Now, I have both of these accounts open in separate browser session tabs.

If you don't have this capability, if you don't use Firefox and don't have this add-on, then you'll need to log out of the general AWS account and then re-log in as the iamadmin user for the production AWS account. Once you've done that, click on the account drop-down at the top right and move to Security credentials. Once you're there, scroll down.

Click Create access key again. Check the box for Command Line Interface. Check the acknowledge box and then click on Next, and then in the description box, go ahead and use the same format, so LOCAL CLI IAMADMIN-PRODUCTION, and click Create access key.

Then once again, click on Download .csv file and rename this file to iamadmin_accesskeys_production, and once you've done that, you can go ahead and click on Done, and now we've created the two sets of access keys that we'll use with the Command Line Interface. Next, you'll need to install version 2 of the AWS Command Line Interface. Now, I've included a link attached to this lesson which details how to download and install the AWS command line for Windows, Linux and macOS.

The installation process isn't all that complex. The important part is the configuration, and the configuration is the same on all of the supported operating systems. So if you open up the URL that's attached to this lesson, it will open a page which should look something like this.

You'll see that there are instructions for Linux, macOS and Windows. So select the correct operating system, so the operating system that you're using on your local machine. If you scroll down, you'll see instructions on how to install it on your particular operating system and you'll find a link to an installation package.

So go ahead and click that link and that will open the installation. We'll be accepting all of the defaults no matter what the operating system. So just perform a default installation.

The installation will take a few minutes to complete. Once it's completed, click on Finish or close down the installation application. Again, this is slightly different depending on which operating system you're using.

Then we need to move across to our command prompt or terminal, depending on which operating system you're using. If I just run an aws and press Enter, if I see usage instructions which look like this, then it's been completed successfully. If you see an error indicating that the application or the command is not found, then you might need to restart your operating system, but in this case, it's completed successfully.

You can verify it properly by running aws space -- and then version and press Enter, and if it's working correctly, you should see aws-cli and then a version 2.something.something. The important part is version 2 because this brings significant enhancements over version 1 that we will be using in this course. What we're going to do now is configure the Command Line Interface.

Now, the way that the command line is integrated with our AWS accounts, or more specifically, our identities or users in those accounts, is we need to configure a set of credentials which the Command Line Interface will use to communicate with AWS. Now, the way that we configure these credentials is to run an aws and then space and then the word configure. Now, if we just use aws configure, then this configures the default configuration profile for the Command Line Interface, and this default configuration profile is what's used if we don't specify what's known as a named profile.

So the Command Line Interface allows us to specify named profiles and it's these that we can use to configure multiple AWS accounts. So we can have a named profile for the iamadmin user in the general AWS account, and we can have another named profile for the iamadmin user in the production AWS account, and that's what we're going to do. So to configure a named profile, all we do is add a space on the end and then --profile and then a space and then the name of this profile.

Now, what I suggest you use is iamadmin- and then general. So this is the name of the profile that will connect to the iamadmin user in the general AWS account. Logically, for the named profile for the production account, we'll be using iamadmin-production.

So first, let's configure the profile for the iamadmin user in the general account. So it should say aws space configure space --profile space iamadmin-general. Go ahead and enter that and press Enter.

Now at this point, it's going to ask for a number of pieces of information. It's going to ask for the access key ID. It's going to ask for the secret access key.

It will ask for a default region and then a default output format. So first, we'll need these credentials. Now, these are contained in these files that you saved earlier.

So first, you'll need to open up the document which contains the word general. So these are the credentials for the iamadmin user inside the general AWS account. So open up this document.

Now, this document will contain an access key ID and then a comma and then it will contain the secret access key. So you need to copy down the access key ID, so the part before the comma. Don't include the comma.

Copy that into your clipboard, and then paste this in where it says Access Key ID, and it should look something like this. Make sure you get all of the characters and then press Enter. Then it will ask for the secret access key, which is the part after the comma within the credentials document.

So copy that into your clipboard and then paste that in, and then press Enter. Next, it will ask for a default region, and we're always going to use Northern Virginia, which is us-east-1. So go ahead and enter that and then press Enter, and then for the default output format, you can just go ahead and press Enter and we'll use the default of None.

Now at this point, the Command Line Interface has been configured to integrate with the iamadmin user of the the general AWS account, and to test that, we can use aws space s3 space ls and then a space. Now this will run a listing of any S3 buckets in this account, and if we don't have any buckets, it will simply return an empty string, and that's fine, but if it returns an error, then we know we have a problem. Now, if we just ran this command on its own, we would get an error because we haven't configured any credentials as part of the default profile.

So it will tell us, "Unable to locate credentials." Because we've configured these credentials inside a named profile, we need to specify that named profile on the command line. So I'm just gonna type that command in again and then follow it with --profile and then a space and then I'm going to use the named profile that I've configured previously, so iamadmin-general. This time, if I press Enter, now that I run the command with the named profile, we won't get the error.

This time it will return an empty string, and that's fine because we don't have any S3 buckets within this account. It's a brand-new account. If you've already created any S3 buckets or if you already have any resources in this account, which you shouldn't do because it's a brand-new account, you might see a list of buckets, but if you're following the instructions as I'm giving them, you should have an empty list here, and that's fine.

The only thing you need to worry about is if you receive an error message. If you receive an error message, it probably means that you haven't copied down either the access key ID or the secret access key in their entirety, and to fix that, you can just go ahead and rerun the aws configure command with this named profile on the end. If we just rerun this, it will offer us the ability to just re-enter those values, but in this case, because we didn't get an error, we don't need to do this.

The next thing we need to do is to follow the same process but this time for the iamadmin user inside the production AWS account. So to do that, aws space configure space --profile space iamadmin-production, and then press Enter and you'll be prompted for those same four pieces of information. So now we need to open the iamadmin credentials for the production AWS account.

You'll see the format is the same. We'll need to copy down the access key ID, which is everything before the comma. Copy that into your clipboard.

Paste that in and press Enter. Then the secret access key, everything after the comma, copy that into your clipboard. Paste that in and press Enter.

Again, the region will be us-east-1, so enter that and press Enter, and then press Enter again so that we don't set a default output format, and now we should be able to run aws space s3 space ls space --profile space iamadmin-production, and again, press Enter, and again, if we don't receive an error, if either we receive this empty string or a list of buckets, that means everything's working as expected. Now, just before I finish up with this lesson, I've been fairly open with showing you these credentials on screen. Now, this is a huge security risk.

If you have these credentials right now, then you could log in to my AWS account. Now, when I'm recording this lesson, what I'm going to do is replace these credentials. So although I've configured my Command Line Interface using these credentials, the minute I stop recording, I'm gonna go back to the AWS console, delete these access keys, and then reconfigure my command line with brand new credentials.

The outcome will be the same, but it simply means that I'm invalidating the credentials that you've seen on this video. For day-to-day usage and for your purposes, you should never show these credentials to anyone who you don't want having access to your AWS account. So whenever you generate credentials, it's important to understand that for anybody who has the access key ID and the secret access key, they can utilize the IAM identity that you've configured together with any permissions that that identity has over this AWS account.

So if you leak your iamadmin credentials, then anyone who has those credentials can interact with either your general or production AWS accounts as the iamadmin user. Because that user has full administration permissions on the account, the results of that can be disastrous. So you need to get into the habit of being extremely careful where you store these credential files and to whom you grant access.

So it's really important to start off being really paranoid and really careful about these credentials, and going a step further, at this point, you should probably delete both of these credential files, so the one for the general AWS account and the one for the production AWS account, and that just means that all of these credentials are safely configured within the Command Line Interface, are not stored anywhere where they can be accessed by anyone but you. Now at this point, you've configured everything that you need to as part of this lesson. So you've set up the AWS Command Line Interface and you've configured two named profiles, iamadmin-general and iamadmin-production, and these are what we're going to use throughout the rest of this course whenever we need to do any work using the command line.

At this point, you've done everything that you need to, so go ahead and complete this video, and when you're ready, I look forward to you joining me in the next lesson.

## aws-accounts.md

## aws-accounts-aws-accounts-the-basics.txt Welcome back, and in this lesson, I want to introduce AWS Accounts. Really understanding what an AWS Account is and what benefits it provides is one of the most important things within AWS. Many students, especially at the start, confuse AWS Accounts with users inside of those accounts and I want you to be 100% clear on the difference.

If you've used AWS before, you might already have an idea of what AWS Accounts are and how they work, but understanding accounts at a really instinctive level is essential for a solutions architect, developer or engineer. Simple systems which you design might operate from within a single AWS Account, but more complex systems or environments operated by large enterprises might use tens, or in some cases, hundreds of AWS Accounts, and for that reason, it's important that you really understand the features and benefits provided by AWS Accounts. This might seem pretty basic, but it's really powerful when you do fully understand it and really dangerous to operate at production scale if you don't.

Let's jump in and get started. This is an AWS Account. When you're just starting with AWS, you might only create one of these.

You might even already have one. Bigger, more complex projects or businesses will generally use many AWS Accounts, and in this course, you're going to use multiple AWS Accounts for the demo lessons, and this will help you understand how businesses actually use AWS in the real world. At a high level, an AWS Account is a container for identities and AWS resources.

Identities is just the technically correct way of referring to things like users, so the things which you use to log in to systems such as AWS. An AWS Account contains users, which you log in with, and resources, which you provision, inside of that account. Keep this idea of an AWS Account being a container in your mind constantly as you move through the course, but this is especially important in this stage of the course where you're going to be creating the AWS Accounts that you'll use constantly as you move through the content.

When you create an AWS Account, you give the account a name, you need to provide a unique email address, and you also need to provide a payment method, which is generally a credit card. If we're creating a production account, we might name the account PROD for production, we would use a unique email address which is unique for this specific AWS Account, and provide a credit card for this production account. Just to reiterate, the credit card can be used for multiple AWS Accounts, but the email address can't.

It has to be unique. You need one unique email address for every AWS Account. The email address that you provide when creating the account is used to create a special type of identity within the AWS Account, which is known as the account root user.

Every AWS Account has an account root user, so the root user of that AWS Account. In this example, if you create a production AWS Account, then the account root user of that account can only log in to that one production AWS Account. If you make another AWS Account, let's say a developer account, then that account will have its own unique account root user with its own unique email address.

Those account root users are different. The production account root user can only access the production account and the developer account root user can only access the developer account. Initially, the account root user is the only identity, the only user created with an AWS Account.

Initially, you have the blank account, the container, and inside that is the account root user of that account. The account root user has full control over that one specific AWS Account and any resources which are created inside it. The account root user can't be restricted.

It will always have full access to everything within that one AWS Account which it belongs to. This is the reason why we need to be really careful with the account root user, because if the user name and password ever become known, the results can be disastrous because the details can be used to delete everything within the AWS Account. The credit card that you provide when you create the AWS Account, that's set as the account payment method, so you can create resources within an AWS Account, and I'll be covering these throughout the course, and if those resources have any billable usage, then that usage is billed to the account payment method, in this case, a credit card.

I'll talk about this later in the course, but on the whole, AWS is what's known as a pay-as-you-consume or pay-as-you-go platform. If you use a service within an AWS Account for two minutes, then you pay for two minutes of that service. Certain services include a certain allocation of free usage per month, and this is known as the free tier, and this is what we're going to take advantage of in this course to keep costs at an absolute minimum.

Now that I've covered the account root user and billing within an account, now I want to touch on the security as it relates to AWS Accounts. You know that the account root user has full control over this one specific AWS Account and this can't be restricted. You can create additional identities inside the AWS Account which can be restricted.

I'll talk about this more soon, but this uses a service called Identity and Access Management, known as IAM, and with IAM, you can create other identities inside the account. These can be different types of identities. We've got IAM users, IAM groups and IAM roles, and I'll cover these in detail in the relevant section of the course, but at this point, it's important to understand that all of these IAM identities start off with no access to the AWS Account, but they can all be given full or limited access rights over this one specific AWS Account.

Just like the account root user, the IAM service is also dedicated to your account. Unless you specify otherwise, any IAM identities created in my account won't be able to access your account. Only identities which you create inside your account and then grant access will be able to access resources within your AWS Account.

Later in the course, I'll talk about how you can do cross-account permissions, but for this point in the course, just think of AWS Accounts as containers. Only things within the account can access anything else within that same account, and another key thing to remember is that with the exception of the account root user, any IAM identity starts off with no permissions. You have to explicitly grant permissions to any identities managed by the IAM service.

Another concept which I want you to be really familiar with is the boundary of the account. On screen now, the orange line around the account, think of this as a wall. It can keep things inside the account from getting out and also keep things outside the account from getting in.

AWS Accounts are really good at containing any damage caused within those accounts, so things such as an inexperienced system administrator doing something silly or a bad actor attempting to intentionally harm your account. If the credentials for the account root user are leaked, then these could be used to delete everything inside that one specific AWS Account, and if your entire business runs from that one single account, then this can be really, really bad. However, if you create separate AWS Accounts for different uses, maybe a development account, a test account and a production account, then you can limit the damage.

If you have any credential leakage or if you have any system admins doing any silly mistakes causing resources to be deleted, then generally these will be isolated to that one specific AWS Account. You can also create AWS Accounts for different teams within your business or even different products that your business sells. AWS Accounts are great for keeping bad things inside one specific part of your AWS environment.

They're also really good for keeping things outside of that boundary. By default, all access to an AWS Account is denied, so unless you configure otherwise, no external identity is allowed access to an AWS Account. The exception to this, of course, is the account root user of that account, who always has full control.

This means that any external identities, for example, external users, are denied by default if they attempt to access your AWS Account. External identities can be granted access, such as Julie in the middle, if you explicitly want to allow this access, but the default security stance is that unless you explicitly allow something, then no access is allowed to your AWS Account. That's AWS Accounts.

They're a crucial part of the AWS product set and understanding them at a really instinctive level is important. Whether you're a solutions architect, a developer, a sysadmin or a DevOps engineer, you need to be comfortable with how to use AWS Accounts effectively. In the following lessons, you're going to create the AWS Accounts which you'll be using for the duration of this course.

I'm strongly recommending that you create brand-new AWS Accounts. Don't make the mistake of trying to use your existing AWS Account or accounts because they're likely to be in a pretty bad state. The longer an AWS Account exists, the more potential there is for misconfiguration, and so it's much better to use brand-new accounts for this course.

I want you to learn how to configure all of this in a correct way using best practices, so please go ahead and create brand-new AWS Accounts for this course. I'll even show you a trick so that you can use one email account to create all of the unique email addresses needed for these multiple accounts, so it shouldn't take that much in the way of effort. With that being said, go ahead and complete this lesson, and then when you're ready, I look forward to you joining me in the next lesson where we're going to get started on creating the AWS Accounts for this course.

## aws-accounts-demo-creating-aws-account.txt Welcome back and in this demo lesson I'm going to step you through how to create an AWS account. This might seem simple but it's important that we start off with the same best practice foundation. In the real world most businesses and projects will use more than one AWS account.

So rather than teaching you using sandbox accounts or using a single AWS account you're going to create a few accounts that you'll use as you move through the course. Now later in the course you're going to link these together using AWS organizations as you start to learn about multi-account management. For now though we're going to start with a single account and before we get started with this I want to show you visually what you're going to be creating over the first part of the course.

Now the first account that you'll be creating is the account that you're going to be logging into and we're going to start by referring to this as the general AWS account. Later in the course when you start using AWS organizations and learn about multi-account management You're going to hear me refer to this as the management AWS account just know that the management account and the general account are the same thing We're referring to this first AWS account that you're going to create So this will be the first account that you'll create and as you know by now when you create an AWS account an account "Account Root User" is created along with it. And it's this "Account Root User" that you'll initially log in to this general AWS account with.

Remember, the "Account Root User" is specific to this one particular account, so this "Account Root User" has full control of the general AWS account. Once you've created this AWS account, you're going to secure it. And this is done by adding multi-factor authentication, also known as MFA, onto the account root user.

Now historically this was a physical device which generated a code which changed periodically. But you can also use an application on your phone or tablet. The idea is that a physical or virtual MFA is associated with the account root user.

Then instead of just needing a username or password to log in, which can be leaked, now Now you also need a one-time code which is generated by the MFA device or application, and this means it's much more secure. You're also going to be configuring a budget, because while the course is going to be as much within the free tier as possible, if you do leave anything running, this might have a cost and will want you to be notified as soon as possible, so a budget helps protect against any unintended costs. Now we also want to avoid using the account root user as much as possible because you can't restrict it and because there's only one of them per AWS account.

Now because of this it's best practice to create IAM identities within your AWS accounts and so you're going to create an IAM identity, an IAM user within the general AWS account called IAM admin. Now this is just a normal IAM user which you're going to give administrator permissions over the general AWS account and this is the identity that you're going to be using for the remainder of the course when you're interacting with the general AWS account. Once you've fully created and configured the general account you're going to repeat that process to create a second one which we're going to refer to as the production AWS account.

So this is a brand new AWS account with a brand new account root user and a brand new IAM identity within that account also called IAM admin. Now this will be the starting structure that you're going to be using throughout the course. Before we get started though I promise you a trick to make creating multiple AWS accounts easier and that's what I want to talk about next.

Now this is a feature that I know a hundred percent works with Gmail It may work with other email providers, but I can only guarantee Gmail at this point. When you're creating AWS accounts, you should view them as disposable, and you should create as many of them as you need. You already know why, because they're containers and they isolate things inside the AWS account.

It's actually better to create a new AWS account structure for every course that you do, because it keeps things isolated and safe and secure. Now because AWS accounts require unique email addresses this can make it a fairly painful process to create them. Historically 10 AWS accounts have required 10 unique email addresses but that's not true if you use a feature available within Gmail and some other email providers.

Let's say that you have a Gmail address in this case it's It's catguy@gmail.com. So this email address is constructed of two parts. The username on the left, so catguy, and then an @ symbol, and then the domain, so gmail.com.

Now normally this would allow you to create one AWS account using the catguy@gmail.com email address. But what you can do is you can use the plus sign in the email address to create an infinite supply unique addresses all of which go back to this main account. For example you could take your username so cat guy and then add a plus and then put AWS account 1 so the whole email address would be cat guy plus AWS account 1 at gmail.com you could also create a second this time using AWS account 2 and then even a third using AWS account 3.

Now these are all unique email addresses but they've required no configuration. You just have the one single Gmail account which comes with the one default email address so catguy@gmail.com and all you do is use the plus symbol and then include any text and that creates a brand new unique email address from the perspective of AWS but you haven't had to configure anything on Gmail. You just take your normal email address, you add some text after the plus sign and that creates what's called a dynamic alias.

It's a brand new email which always points at your main Gmail account. So you can use anything after the plus symbol and it creates what looks like a unique email address and you can use this address to sign up for an AWS account. So this essentially gives you an infinite number of unique email addresses using one single Gmail.

So at this point you don't have any reason not to create a brand new set of AWS accounts for every single training course that you do. Now let's switch over to the console and get started creating the first AWS account, so the general AWS account. Okay so now I've moved across to my web browser and to create an AWS account you're going to need a few things.

You'll need an email address for the account root user of that account and remember what I've just talked about on the previous screen how you can create an infinite number of unique emails to use. You'll also need to choose an AWS account name and this is important because it will help you identify the account. You'll need to set a unique password for this account root user.

You'll need billing information to add to the account. Now the account does come with a free tier allocation so you won't be billed against this billing method unless you actually incur charges and I'll be teaching you throughout this course how you can keep track of any charges on your AWS account and the course itself where possible will be within the free tier. In addition to this you'll need to verify your identity and you'll also need to choose a support plan even if that plan is the free one.

So to get started we need to go ahead and enter the email address for this AWS account. Now remember this is the general AWS account. You'll need to pick something that makes sense to you and is unique to you because this email address needs to be unique and you do need to be able to receive emails to this address.

Now depending on the version of the user interface that you do have and this can change very often you might get this box pre-populated so this AWS account name. For me this is the structure I'll be using so AC my initials - training - AWS and then hyphen general. This is for the general AWS account and I'll be changing this general to production when I create the production account.

Now at this stage you'll need to verify the email address so once you've entered all of that information go ahead and click verify email address. You'll receive a verification email containing a code to this address. It could take up to five minutes to arrive and do make sure that you check your spam folder.

Once you do have that code, enter it into this box and then click on verify. Hopefully you'll see that the email address has been verified and then we're good to continue and it's at this point that you'll need to pick a suitably strong password for the account root user of this account. Now I recommend using a password manager to generate a strong password so go ahead and do that enter that same password into both boxes and then click on continue.

Next you'll be asked for some account information, generally this will be a personal AWS account for your own projects, so pick the appropriate box, enter the appropriate information here, check this box and click on continue and I'm going to be hiding this information for privacy reasons. Next you'll need to enter some billing information and this payment method won't be charged unless you incur charges against the AWS account. I'm going to keep this course as much within the free tier as possible so this generally shouldn't happen.

Now it's It's worth noting that you might notice a pending payment on this credit or debit card which AWS used to verify your identity. This pending charge will generally disappear within a few days. It's only used to verify that it's a valid billing method.

So go ahead and enter all of this information and then continue and once again I'm going to keep this information redacted for privacy reasons. This next step is a simple identity verification step. You'll need to pick the method of identity verification, either SMS or voice call.

I'm going to pick SMS because generally that's quicker. You might only see one or the other of these options or you might see both. Just pick the one that's appropriate.

For SMS you'll need to enter a valid phone number to receive text messages to, so I'm going to enter my details. You might need to complete this security check by entering these characters, so I'm going to go ahead and do that. Then I'll move on.

I'll wait for the verification code to arrive, enter it into that box, and then move on to the next step. At this point you'll need to pick the support plan to use. For training accounts we default to using the basic support plan which is free.

And this will provide just enough support for any account or billing issues. If we need anything more, if this is a production AWS account, then we need to pick Developer or Business support. Now I'll be covering the details of these other support plans, if appropriate, elsewhere in the course.

For now though, go ahead and pick 'Basic Support' and then click the button to continue. Now at this point you should see a 'Congratulations' screen which tells you that AWS are activating your account. Now this activation can sometimes be instant or it can take anywhere up to an hour.

In my case I've already received the email, so normally it is relatively quick. Once you do receive the email, you can click to start logging in to the management console. And again, you'll need to use the email address associated with the account root user.

You might have to complete a security check, but then you will have to enter the password for the account root user. And once you've logged in, you'll be at the main AWS console. And now we're logged into the main AWS console.

Now don't worry if you do see some error or warning notifications when you first sign into the console. these widgets take time to populate. There are a few final steps that I want you to do before we finish up creating this AWS account.

To do that click on the account drop down at the top right and then move to account. Now again I've blanked out all of my personal information. What I want you to do though is to scroll down on this screen then optionally under alternate contacts you can click on edit and enter your details for all three of these contacts.

If you creating an AWS account for business reasons then often you might have different billing operation and security contacts. Now you don't have to do this step but if you are creating this account for real-world usage you might want to enter these details. What I do want you to do though is to continue scrolling down and under IAM user and role access to billing information click on edit check this activate IAM access box and then click on update.

This is going to make sure that if you're logged in as an IAM identity then you have full access to the billing console provided you have permissions. If this box wasn't checked then even if we gave an IAM identity full admin permissions it wouldn't be able to access the billing console so it's important that we allow access to this console. Now at this point that's everything that you need to do in this creating an AWS account video so move back to the console and one last thing I want to mention is throughout this course whenever you're interacting with AWS generally I want you to be in the Northern Virginia region.

Now what region is selected by default depends on where you're logging into AWS from and this region selection does have the tendency to change so generally as you're working through any of my courses continually verify that if the region is selected it does say US East 1. If it says anything like global that's okay but if it displays a region make sure that it's US East 1 and if it's not go ahead and change it back to Northern Virginia. At this point though that's everything I wanted to cover.

You've completed the account setup of the general AWS account so go ahead and complete this video and when you're ready I look forward to you joining me in the next. ## aws-accounts-multifactor-authentication.txt 00:00:00.300 --> 00:00:01.170 Welcome back, 00:00:01.170 --> 00:00:03.150 and in this fundamentals lesson, 00:00:03.150 --> 00:00:05.040 I want to quickly cover a topic 00:00:05.040 --> 00:00:07.440 which you'll use constantly within the course 00:00:07.440 --> 00:00:08.730 and in the real world, 00:00:08.730 --> 00:00:13.110 and that's multifactor authentication, known as MFA. 00:00:13.110 --> 00:00:15.240 Now, we have a fair amount of theory to cover.

00:00:15.240 --> 00:00:17.700 So let's just jump in and get started. 00:00:17.700 --> 00:00:19.290 Now, before I talk about the way 00:00:19.290 --> 00:00:23.760 that multifactor authentication is implemented within AWS, 00:00:23.760 --> 00:00:25.620 let's just refresh our knowledge 00:00:25.620 --> 00:00:28.620 on exactly why MFA is needed. 00:00:28.620 --> 00:00:30.210 So consider for a moment the way 00:00:30.210 --> 00:00:34.080 that you usually log in to any web-based applications.

00:00:34.080 --> 00:00:37.350 Generally, you use usernames and passwords. 00:00:37.350 --> 00:00:40.320 And if both of these are leaked, then anyone can be you. 00:00:40.320 --> 00:00:43.050 Anyone can take your username and password 00:00:43.050 --> 00:00:45.420 and use them to log in to an application 00:00:45.420 --> 00:00:48.300 and impersonate you as an identity.

00:00:48.300 --> 00:00:50.940 So what we need is a way to improve this. 00:00:50.940 --> 00:00:53.250 So there's another term which I want to introduce 00:00:53.250 --> 00:00:56.790 and that term is known as a factor or factors. 00:00:56.790 --> 00:01:00.840 So factors are pieces of evidence which prove identity 00:01:00.840 --> 00:01:03.120 and there are different types of factors.

00:01:03.120 --> 00:01:06.630 So when you hear the term single-factor authentication, 00:01:06.630 --> 00:01:09.510 this means to use just one of these types 00:01:09.510 --> 00:01:11.940 or one of these types of factors. 00:01:11.940 --> 00:01:16.320 Multifactor authentication is when you use multiple factors 00:01:16.320 --> 00:01:18.210 or multiple types of factors 00:01:18.210 --> 00:01:20.280 to log in to an application. 00:01:20.280 --> 00:01:22.650 Now, there are four common factors that you'll use 00:01:22.650 --> 00:01:25.590 to log in to any web application.

00:01:25.590 --> 00:01:27.300 First is knowledge, 00:01:27.300 --> 00:01:29.280 and this is something that you know. 00:01:29.280 --> 00:01:33.420 So the knowledge factor includes usernames and passwords. 00:01:33.420 --> 00:01:35.880 The second type of factor is possession 00:01:35.880 --> 00:01:37.500 and this is something that you have, 00:01:37.500 --> 00:01:42.210 so a bank card or an MFA device or an MFA application.

00:01:42.210 --> 00:01:46.920 So consider what you do when you use a bank card at an ATM. 00:01:46.920 --> 00:01:48.510 You have to have the bank card, 00:01:48.510 --> 00:01:50.250 you put it inside the ATM, 00:01:50.250 --> 00:01:52.500 and then you need to enter a pin. 00:01:52.500 --> 00:01:55.610 So this is an example of multifactor authentication.

00:01:55.610 --> 00:01:58.050 In this case, you're using two factors: 00:01:58.050 --> 00:02:00.180 something that you have, the bank card, 00:02:00.180 --> 00:02:02.430 and something that you know, your pin. 00:02:02.430 --> 00:02:04.320 The next factor is inherent. 00:02:04.320 --> 00:02:05.940 So this is something that you are, 00:02:05.940 --> 00:02:10.110 so a fingerprint, a face scan, voice identification, 00:02:10.110 --> 00:02:11.340 or an iris scan.

00:02:11.340 --> 00:02:14.310 These are all examples of the inherent factor. 00:02:14.310 --> 00:02:16.560 And then lastly, we have location. 00:02:16.560 --> 00:02:19.290 So this can be either a physical location, 00:02:19.290 --> 00:02:22.740 so a particular set of coordinates anywhere in the world, 00:02:22.740 --> 00:02:25.050 or it can be the type of network 00:02:25.050 --> 00:02:28.230 that you're currently logged in to to access a system.

00:02:28.230 --> 00:02:30.450 So whether you're logged in to the corporate network 00:02:30.450 --> 00:02:33.000 or using your home wifi network. 00:02:33.000 --> 00:02:35.070 Various different security procedures 00:02:35.070 --> 00:02:38.070 might require a certain location, 00:02:38.070 --> 00:02:39.690 which is a factor to use 00:02:39.690 --> 00:02:42.120 as part of an authentication process. 00:02:42.120 --> 00:02:42.953 So in general, 00:02:42.953 --> 00:02:46.020 the more factors that your authentication process uses, 00:02:46.020 --> 00:02:47.910 this means more security 00:02:47.910 --> 00:02:51.390 and it also means that it's harder to fake your identity.

00:02:51.390 --> 00:02:53.670 So imagine if you could only log in to a system 00:02:53.670 --> 00:02:55.380 using something that you know, 00:02:55.380 --> 00:02:56.940 so username and password, 00:02:56.940 --> 00:02:58.110 something that you have, 00:02:58.110 --> 00:03:02.160 so a security card or an MFA device or application, 00:03:02.160 --> 00:03:05.970 imagine if you also needed a fingerprint or a facial scan 00:03:05.970 --> 00:03:07.710 and you could only log in 00:03:07.710 --> 00:03:10.620 within the confines of your corporate network. 00:03:10.620 --> 00:03:13.320 That would mean a really secure login process, 00:03:13.320 --> 00:03:16.110 but it would mean it's not very convenient. 00:03:16.110 --> 00:03:18.480 So generally, we're trying to achieve a balance 00:03:18.480 --> 00:03:21.060 between convenience and security.

00:03:21.060 --> 00:03:23.700 Now, at this point, I want to show you the specific process 00:03:23.700 --> 00:03:28.230 of how multifactor authentication is implemented within AWS. 00:03:28.230 --> 00:03:29.850 So we're going to step through the process 00:03:29.850 --> 00:03:34.770 of exactly how AWS handles the addition of a second factor. 00:03:34.770 --> 00:03:38.460 So this is an MFA device or an MFA application.

00:03:38.460 --> 00:03:40.770 So we start with an AWS account. 00:03:40.770 --> 00:03:42.900 And by default, you log in to this 00:03:42.900 --> 00:03:45.090 with a username and password. 00:03:45.090 --> 00:03:47.340 These are both things that you know.

00:03:47.340 --> 00:03:48.210 So this is known 00:03:48.210 --> 00:03:52.140 as single-factor or one-factor authentication. 00:03:52.140 --> 00:03:54.900 Now, the issue, as I touched upon previously, 00:03:54.900 --> 00:03:56.670 is that if both of these leak, 00:03:56.670 --> 00:03:58.980 either because of an error on your part 00:03:58.980 --> 00:04:00.960 or because of malware on the machine 00:04:00.960 --> 00:04:02.550 that you are using to log in, 00:04:02.550 --> 00:04:05.310 then a bad actor can fake your identity 00:04:05.310 --> 00:04:06.900 and log in as you. 00:04:06.900 --> 00:04:09.390 Now, we improve this by using MFA.

00:04:09.390 --> 00:04:13.530 As a reminder, this stands for multifactor authentication. 00:04:13.530 --> 00:04:17.790 And MFA can be activated using a physical MFA device, 00:04:17.790 --> 00:04:20.010 which is a key fob style device 00:04:20.010 --> 00:04:22.740 which generates ever-changing codes, 00:04:22.740 --> 00:04:25.590 or you can use a virtual MFA device, 00:04:25.590 --> 00:04:28.020 which is added to an MFA application 00:04:28.020 --> 00:04:30.240 such as Google Authenticator, 00:04:30.240 --> 00:04:33.420 and these applications run on a phone or other device 00:04:33.420 --> 00:04:36.240 and can store lots of virtual MFAs. 00:04:36.240 --> 00:04:37.860 And this means that they can be used 00:04:37.860 --> 00:04:39.690 for lots of different services 00:04:39.690 --> 00:04:41.280 and lots of different accounts 00:04:41.280 --> 00:04:42.750 within those services.

00:04:42.750 --> 00:04:46.950 Now, to configure MFA within AWS for a specific identity, 00:04:46.950 --> 00:04:49.080 let's say the account root user, 00:04:49.080 --> 00:04:52.170 you activate MFA for that user. 00:04:52.170 --> 00:04:56.070 And when you do so, AWS generates a secret key, 00:04:56.070 --> 00:04:58.440 which is a randomly generated key, 00:04:58.440 --> 00:05:01.590 and it also generates other associated information 00:05:01.590 --> 00:05:04.020 such as the username it links to 00:05:04.020 --> 00:05:06.360 and the name of the service. 00:05:06.360 --> 00:05:09.420 This information needs to be eventually entered 00:05:09.420 --> 00:05:11.220 into an MFA application, 00:05:11.220 --> 00:05:13.230 such as Google Authenticator, 00:05:13.230 --> 00:05:14.662 and to make this easier, 00:05:14.662 --> 00:05:17.580 AWS use all of this information together, 00:05:17.580 --> 00:05:20.850 so the secret key and the additional information, 00:05:20.850 --> 00:05:22.830 to generate a QR code 00:05:22.830 --> 00:05:26.850 and this QR code encodes all of this information 00:05:26.850 --> 00:05:28.560 in a visual pattern.

00:05:28.560 --> 00:05:30.480 So once you've got this QR code, 00:05:30.480 --> 00:05:33.540 using the MFA application on your phone, 00:05:33.540 --> 00:05:34.920 you scan this code, 00:05:34.920 --> 00:05:37.230 which transfers the information 00:05:37.230 --> 00:05:39.720 into the MFA application. 00:05:39.720 --> 00:05:43.470 And this means there's now an entry in the application 00:05:43.470 --> 00:05:46.800 with a code which regenerates periodically. 00:05:46.800 --> 00:05:48.000 It's never the same.

00:05:48.000 --> 00:05:49.740 A new code is generated 00:05:49.740 --> 00:05:52.890 every single time the code refreshes. 00:05:52.890 --> 00:05:55.350 Now, the way to think about the application 00:05:55.350 --> 00:05:59.370 is that it holds one or more virtual MFAs 00:05:59.370 --> 00:06:02.940 and each virtual MFA, as the name suggests, 00:06:02.940 --> 00:06:06.570 is an MFA device, only virtual. 00:06:06.570 --> 00:06:09.600 So if you have two users within AWS, 00:06:09.600 --> 00:06:13.410 then you would generally have two virtual MFAs 00:06:13.410 --> 00:06:16.200 and you can have, within sensible limits, 00:06:16.200 --> 00:06:20.460 as many of these as you want within your MFA application 00:06:20.460 --> 00:06:23.880 all representing identities in various services 00:06:23.880 --> 00:06:27.840 such as AWS, Google Mail, Azure, GCP, 00:06:27.840 --> 00:06:31.950 or any other cloud environments or web applications.

00:06:31.950 --> 00:06:33.780 Now, once you have the MFA configured, 00:06:33.780 --> 00:06:36.450 the next time you log in to AWS, 00:06:36.450 --> 00:06:39.690 as well as being required to enter the username and password 00:06:39.690 --> 00:06:42.360 for the specific user that you're using, 00:06:42.360 --> 00:06:46.230 you'll also be prompted to enter the MFA code showing 00:06:46.230 --> 00:06:49.170 for that one specific virtual MFA 00:06:49.170 --> 00:06:51.570 within your authenticator application. 00:06:51.570 --> 00:06:55.920 It needs to be the current code for the correct virtual MFA 00:06:55.920 --> 00:06:59.160 on your specific authenticator application 00:06:59.160 --> 00:07:02.160 on your phone or other device. 00:07:02.160 --> 00:07:04.770 This means in addition to the username and password, 00:07:04.770 --> 00:07:06.510 which are both things that you know, 00:07:06.510 --> 00:07:09.570 so this means single-factor authentication, 00:07:09.570 --> 00:07:12.360 you now need to provide something that you have 00:07:12.360 --> 00:07:16.350 and this means your identity inside AWS is secured 00:07:16.350 --> 00:07:19.440 using multifactor authentication.

00:07:19.440 --> 00:07:21.930 Even if your username or password were leaked, 00:07:21.930 --> 00:07:23.940 in order to log in to AWS, 00:07:23.940 --> 00:07:28.320 that's only possible if you provide the MFA code as well. 00:07:28.320 --> 00:07:30.750 If you lose your MFA device, 00:07:30.750 --> 00:07:33.690 even though a bad actor has that device 00:07:33.690 --> 00:07:35.580 and has that MFA code, 00:07:35.580 --> 00:07:37.320 login would only be possible 00:07:37.320 --> 00:07:40.260 if they also know your username and password. 00:07:40.260 --> 00:07:41.760 You need all three.

00:07:41.760 --> 00:07:44.550 And in general, on most modern phones, 00:07:44.550 --> 00:07:48.480 the MFA application itself will also be protected 00:07:48.480 --> 00:07:50.970 with multifactor authentication. 00:07:50.970 --> 00:07:53.160 So generally, you'd need to have first logged in 00:07:53.160 --> 00:07:55.320 to the device using a pin code 00:07:55.320 --> 00:07:57.900 and then potentially needing a fingerprint scan 00:07:57.900 --> 00:07:59.370 or a facial scan 00:07:59.370 --> 00:08:03.150 in order to gain access to your MFA application. 00:08:03.150 --> 00:08:04.800 So this is a really effective way 00:08:04.800 --> 00:08:06.480 of adding additional security 00:08:06.480 --> 00:08:10.980 to any of your web applications, including AWS.

00:08:10.980 --> 00:08:13.380 Now, this is everything I wanted to cover in this lesson. 00:08:13.380 --> 00:08:15.990 This is a feature that you're going to be using constantly 00:08:15.990 --> 00:08:17.520 in any of my courses 00:08:17.520 --> 00:08:20.130 and if you use AWS in the real world. 00:08:20.130 --> 00:08:22.470 But with that being said, go ahead and complete this video, 00:08:22.470 --> 00:08:23.340 and when you're ready, 00:08:23.340 --> 00:08:25.803 I'll look forward to you joining me in the next.

## aws-accounts-securing-aws-account.txt Welcome back and in this demo lesson I'm going to show you how to initially secure an AWS account. What you're going to do is attach a virtual MFA device to the account root user of the general account which adds an additional layer of security. Now before we begin let's explore what this means.

We're going to be working on the general AWS account with the account root user and let's pretend for a second it already has some resources which have been created within it, though for now our accounts are completely clean. Now with this example if you're trying to log into this general AWS account then so far you will have used the account root user and you will have provided the account root user email address and the associated password and this is known as single factor or one factor authentication because it's using one type of secret, in this case the password, something which Julie in this example knows. Now there's a problem with this method though if in some way the account root user credentials were leaked maybe via espionage or social engineering then a bad actor could use them and easily log into the account in Julie's place and potentially delete all of the resources in the account so all of the cat pictures which you've been storing inside AWS or create new resources to farm Bitcoin so something which will cost you money and make the clown lots of money in the process.

Now we can prevent this by using multi-factor authentication and this means adding a second factor something other than the secret which Julie knows. Now in addition to this we're using something that Julie has. A physical MFA device or virtual MFA device which is running within an application on her mobile phone.

Now it means that in order to log in an MFA code is needed. Something which is valid for a single use and changes every 30 seconds or so. Now this means that if our evil clown only has the username and password or if he has an older invalid code then he will be denied entry into the general account using the account root user.

In this case we're using two factors something that Julie knows so her password and something that Julie has. Now we could depending on the system add even more factors. Certain systems allow you to use biometrics such as a fingerprint or retinal scan which in this This example is something that Julie is, and that makes it even harder for anyone but Julie to access a sensitive system.

With AWS we can use an MFA token system, and that's what we're going to be configuring next, so let's move over to the console and get started attaching a virtual MFA device to the account root user of the general AWS account. So to configure that what we need to do is to click on this dropdown and then select security credentials. You're taken to a different area of the console and don't worry that it says identity and access management.

This is simply the console where you configure your security credentials but because we're using this drop down and because we're logged in as the account root user of the general AWS account then we're configuring the security credentials for the account root user. So scroll down to multi-factor authentication and then click assign MFA device. Now we need to give this MFA device a name so you can put anything here I'm going to pick something that makes sense to me but you can put something which makes sense to you for this specific authenticator and then you're allowed to choose an MFA device type.

Now the options that we currently have available we've got authenticator app, security key or hardware TOTP token. Now for this demo we're going to pick authenticator app so go ahead and select that option and then click on next. In order to set up this virtual MFA you need to click on show QR code and then scan the QR code with your virtual MFA application.

Now examples of these include the Google authenticator, 1Password, Authy or many more. I've included some examples attached to this lesson, but you do need to download an authenticator application for your mobile phone or desktop. Once you've done that, what you'll need to do is to click on 'show QR code', scan the code and it will create an entry within that virtual MFA application.

Now you will have entry for each identity in each account so at this point we're going to create a virtual MFA for the account root user of the general AWS account. Later in the course when you create the production account you'll be creating another entry within your MFA application for the account root user of the production AWS account and then later still you'll be creating another MFA for the IAM admin identity in both of those accounts so by the end of this part of the course you'll have four entries within your MFA application. One for the account root user of the general account, one for the account root user of the production account and then one for the IAM admin user in each of the general and production accounts for a total of four.

But now let's worry about setting this up for the account root user of the general account so click on show QR code scan that code and you'll be presented with an MFA code which constantly changes. Once you've done that you need to save that in your MFA application and then enter two consecutive codes in these boxes. So you'll see that once you scan this QR code and save it, it will generate a code which changes periodically and you need to enter two of those codes.

Now I'm going to keep all of this secret for security reasons but you need to follow this process. So click on show QR code, scan the code with your authenticator application, enter the first code into box number one and then the second code into box number two. Now this might take you a couple of seconds so pause the video, you'll need to wait for your authenticator application to generate two different codes and once it has, go ahead and click to move on to the next screen.

That process has been completed successfully and you should see this positive dialogue saying you have successfully assigned a virtual MFA. And then click on this drop down and we're going to test that the process has been completed successfully. So go ahead and click on sign out and then click to log back in to the console.

You'll need to make sure that root user is selected and then enter your account root user email address for the general AWS account. Go ahead and click to move on. You might be again prompted for another security check.

Just enter those characters and if you can't see them clearly click on refresh or click on the speaker symbol to do this with audio. Click to move on. You'll need to enter your chosen password and then click.

This time you'll need to enter your MFA code and this will be contained within your authenticator application. So locate that code and enter it and this This code changes periodically and it's only valid for a one time use. So it means that even if your account email address and password were leaked, nobody can log into this account root user without a valid MFA code.

Go ahead and click to log into the console and you'll be successfully logged back into the AWS console. Only now to do this from this point onwards, you'll need something that you know, which as the account root user email and password as well as something that you have which is the one time password. Now again for production usage you should probably use a hardware token but for setting up training accounts using a virtual MFA device is absolutely fine and again I've attached some good quality software applications to this lesson which you can use for this training or for any other MFA style applications.

Now at this point we've finished everything that we needed to do in this demo lesson. Remember when you're setting up any other AWS accounts and any other identities within those accounts you need to add another entry within your MFA application. Don't reuse the one-time password that you've just added for the account root user of the general account you need to add additional entries into your authenticator application for any other identities in any other AWS accounts.

and by the end of this section of the course you should have a total of four one each for the account root user of the general and production accounts so two for the account root users of those accounts and then one each for the IAM admin user of the general and production accounts so two, one each for each of those for a total of four so by the end of this section you should have four virtual MFAs configured and that's a good thing to check once you've completed this section of the course. But at this point that's everything I want you to do in this demo lesson so go ahead and complete this video and when you're ready I look forward to you joining me in the next. ## aws-accounts-creating-a-budget.txt Welcome back and in this demo lesson we're going to step through how you can handle basic cost management of an AWS account.

I'm going to explain what the AWS free tier is and we're going to set up a budget within our AWS account so we can closely monitor any spend as we move through the course. Now it's my intention this course will stay as much as possible within the AWS free tier but you do need to know how to effectively monitor usage within the platform. Now attached to this lesson is a link which details all of the offers which are available within the AWS Free Tier.

Now products within AWS either provide free trials which give you short term free trial offers, some services provide access for 12 months for free, some services are always free or a certain allocation. Now this page, the AWS Free Tier Overview, gives you an overview of all of the different free elements of all of the AWS products. So you can see, for example, that for the first 12 months you're provided with 750 hours per month of access to certain EC2 instances.

instances. You can see that you receive five gigabytes of standard storage on Amazon S3 and you're given 750 hours of certain types of Amazon RDS instance. Now many products within the platform give you access to a certain allocation and this page details all of those allocations so it's definitely something that you should take a look at.

Now inside AWS accounts you have access to a number of tools which provide really granular access to what services are consuming things within your AWS account. You're able to see services which transfer data, you're able to see if you're consuming space within S3 buckets and what region, you get access to very granular tooling within AWS. Now to do this just make sure that you are logged in as the account root user of the general AWS account and then click on this drop-down and go ahead and click on billing dashboard.

This is going to take us to the billing console which is the central point that you need to use to interact with any of the AWS billing services. What you're able to do is to click on bills and you can click on the date drop down and see an overview of any usage for both the current un-billed month as well as any previous bills. You're also able to see any payments, any any credits.

Further down the line, you can see cost and usage reports. You're able to go into the cost explorer product and get really granular views over any spends within your account. And this page will provide a really good overview of the spend last month, the month to date, as well as a forecast spend for the current month.

It's a really good way to see how much your estimated bill is likely to be. So as we move through the course, This is something that I want you to come back to and evaluate your usage on a constant basis. What I also recommend to all of my students is to click on billing preferences and then check all of these boxes.

So check that you want to receive a PDF invoice by email. By default, you will receive an email every month to let you know that your bill is ready. But if you don't check this box, then you have to log into the AWS account to see that bill.

If you check this box, it will be delivered along with the email. So that's really useful. You should also check receive free tier usage alerts, because this will notify you if you're approaching any of the usage thresholds for the AWS free tier.

And you should go ahead and put your email address in this box to receive those alerts. And then finally, you should probably go ahead and check this final box to receive billing alerts. Now, what I want to do at this point is to create a cost budget.

So on the menu on the left, go ahead and click on budgets. Budgets are a really effective way which allow you to monitor your spend and configure alerts as you approach certain percentages of that desired spend. So it's a really good way to manage the costs of your AWS account.

So let's go ahead and click on create a budget. Now under budget setup, make sure that you select to use a template. You can click on Customize Advanced, but for this course we're going to use a template.

Now below there are a number of different templates that you can choose to use. Now what you pick depends on what budget you have available for your training. The one that's selected right now is the Zero Spend budget.

And this will inform you if you have any costs on your AWS account. Now this is useful if you want to ensure that you stay entirely within the free tier. You'll be notified if you have any spend on the AWS account.

The other option is to pick a monthly cost budget where you can specify an amount of money per month that you're willing to spend. And you'll be notified if you exceed that amount. So at this point you have two choices.

You can either specify a zero spend budget or a monthly cost budget. So go ahead and pick whichever one of these that you want to use. I'm going to choose a monthly cost budget, but if you aren't able to spend an amount of money reliably, then go ahead and pick the zero spend budget.

Once you do that, you'll need to name your budget. If you are choosing the cost budget, then directly under that you'll need to specify the amount of money that you want to spend. In my case, I'm going to pick 10.

So if I spend more than 10 USD, I'm going to be notified. And then in either case whether you're using the zero spend or the monthly cost budget you'll need to enter email recipients. So go ahead and enter your email in this box.

This is the email address that will receive any notifications if you exceed this budget. And then once you've entered all that, scroll down and click on 'Create Budget'. Now at this point the budget's created, everything should look good and it will take up to 24 hours to populate all of your spend data.

That's all good, all I want to make sure is that you know how to create a budget. As I mentioned before for this course we're going to keep it as much in the free tier as possible but if you are creating production accounts which have real business usage then you do need to get into the habit of creating budgets. Now at this point that's everything that you'll need to do for this demo.

Go ahead and complete the video and when you're ready I'll look forward to you joining me. in the next. ## aws-accounts-creating-the-production-account.txt Welcome back.

And at this point you've successfully created and configured the general AWS account which you'll be using throughout this course. Now I mentioned earlier in the course that to make this realistic, to give you the experience of working with a multi account environment, we're going to be using different AWS accounts and connecting them together using an AWS organization. Now I'll be covering what AWS organizations is later in the course, but next I'll want you to go ahead and create a brand new Production AWS Account.

So this is a completely separate account than the general account that you've created up until this point of the course. As you move through the course, certain demos will require multiple AWS accounts in order to demonstrate certain technologies. For example, cross account storage using the simple storage service.

Whenever we're using demos, which only require one account, we'll be using the general account. Any demos which require multiple accounts will also be using the production account. So at this point, I want this to be a do it to yourself lesson.

I want you to go ahead and create the production AWS account with exactly the same configuration as you have done for the general account. Now creating and figuring the production account will involve a number of steps. First, you'll need to decide on an email address to use for the production AWS account.

Now because this is a brand new account, a completely separate AWS account from the general AWS account, you'll need to use a unique email address. Now don't forget the Gmail '+' trick that are detailed earlier in this section of the course. This will allow you to use the '+' sign in an email address.

And this will mean that you can generate an infinite number of unique email addresses which all go back to the same Gmail account. So you'll need to configure an email address that's different from the one that you used for the general account and you'll need to use this for the production account. Once you've got that email address configured, then you'll need to go ahead and follow the exact same signup process to create the production AWS account.

Now you can use most of the same value, so the same, the same address, you'll need to choose a different account name, I recommend using -production instead of -general like you used when you are creating the general account, but you can use on the whole the same details. You'll be able to use the same credit card. You should pick the same support plan, but at the end of that process, you'll be logged in to the AWS console of the production AWS account, a brand new account.

You'll also need to follow the same steps to secure the production AWS account which means adding multifactor authentication to the account root user of that production account and you'll need to log out and log back in to test it. Now make sure when you're adding MFA to the account root user, you are adding the MFA as a separate code or separate profile within your multifactor authentication application. So whether you are using Google authenticator, or One Password, or Authy or any of those other tools, make sure that you're adding the MFA for the account root user of the production AWS account as a separate MFA within that application.

Don't try to use the same MFA setup that you used for the general AWS account. Once you've added MFA, you'll need to go to the billing console, go to billing preferences and check the same three check boxes that you did for the general account, also adding your email address for any alerts. Then you'll need to go to budgets and create a budget also the same way that you did for the general AWS account.

If you've forgotten any of those steps, feel free to re-watch the previous lessons and just adjust the configuration for the production AWS account. You also need to remember to go into the account settings of the production AWS account and enable IAM User and Role Access to billing. And then optionally, if you did this in the general account, you can also add those three different account contacts to that same account screen.

But remember, this is optional. Now I want you to follow all this process yourself without any guidance from me because I want you to be comfortable setting up a brand new AWS account. I'm super confident that you can do this.

You rock, you followed every step of the process from beginning to end for the general account. So you can just do the same thing for the production account. So at this point, go ahead and complete this video and then create and configure the production account.

And I look forward to seeing you when you've completed that in the next lesson of the course. ## aws-accounts-iam-basics.txt Welcome back and in this lesson, I want to introduce a really important AWS service and that's Identity and Access Management known as IAM, or IAM. Now I have a whole section of the course dedicated to this service later on, but for now I just want to introduce it.

Now, I want to make this lesson as brief as possible, so let's just jump in and get started. To understand why IAM exists, we need to understand the current identity situation of the AWS accounts that you've created for the course so far. The accounts that you've created have an associated Account Root User, and the account trusts this user fully.

This is why the Account Root User has full unrestricted access to the account. Now the AWS account and the Account Root User can really be thought of as the same thing. The Account Root User gets created with the account, and it can't be restricted in any way.

In most real world situations, you want to be able to grant other people in your organization access to your AWS account. This might be users, groups, or even applications which they create or manage and you generally want to restrict the access that these people, groups or applications have. It's always best practice to only give the permissions required to do a job, or perform a task and this is called least privileged access.

Only having a single identity in the account is also problematic. If the credentials are ever leaked for the Account Root User, then the damage could be account wide. Remember, it's not possible to restrict the permissions or the access rights that the Account Root User has, and so if the credentials are leaked, then potentially all regions and all services in those regions are at risk.

What we need is a way to allow more control over what access is given to our AWS accounts, and that is where IAM comes in handy. Every AWS account comes with its own running copy of IAM, its own database. Now IAM is a globally resilient service, so any data is always secure across all AWS regions.

Remember that one because it'll probably feature on the exam, but also understand that the IAM that you see in each of your accounts is your own dedicated instance of IAM separate from other accounts and from anyone else's accounts. Your AWS account trusts your instance of IAM. IAM like the Account Root User can do anything in the account.

Now there are some restrictions, but this is generally around billing control and account closure. Operationally, the IAM of your account is trusted fully by the account and so IAM as a service can do as much as the Account Root User. Inside IAM, you can create other identities.

So there are different types of identities and you can create many of these, so you're not limited to the single Account Root User anymore, you can create multiple identities. And IAM can allow these identities to do certain things. Now because a single AWS account trusts IAM, if IAM allows one of the identities that it manages to do something, the account automatically trusts that identity in the same way that it trusts IAM and I'll show you how this works when I talk in more detail about access rights and permissions as we go through the course.

Let's quickly look at some of the different things that IAM lets us create. IAM lets you create three different types of identity objects, we've got IAM User, IAM Groups, and IAM Roles. They each have their own specific users and by the end of this course, I'll make sure that you really understand when to use each, but at this stage, I just want to quickly introduce them.

Now users represent humans or applications that need access to your AWS account. If Bob from accounting needs access to AWS billing, or Jane from infrastructure needs access to create and terminate EC2 virtual machines known as instance, then generally Bob and Jane will have an IAM User created inside the IAM service. But IAM user can also be used for applications.

If you have a backup application, it might also use an IAM User to log into your account and do those backups. Next we've got groups and groups are just collections of related users. If you want to manage all development team users, you might create a development team group and add the IAM User to that group, same for finance or HR.

Then we've got IAM Roles and IAM Roles are fairly tough to understand at first, but they can be used by AWS services or if you want to grant external access to your account. Now you'll see later in the course how you can use IAM Roles to give an EC2 instance itself access to AWS services. Roles are generally used when you want to grant access to services in your account to an uncertain number of entities.

So for example, if you want all EC2 instance in your account to be able to access the simple storage service which I'll be covering soon, then you can create a role which grants access to the simple storage service and then allow instance to use that role. So generally you pick IAM Users when you can identify the individual thing that will log in to that user. So if it's an individual person or an individual application, then generally you'll use users.

Roles tend to get used when the number of things is uncertain. So if you want to grant users of external accounts access to say a simple storage service bucket, or if you want to grant an uncertain number of EC2 instance access to certain services in your account, or if you want to allow AWS services themselves to interact on your behalf, then you'll generally use a role. Now it is really difficult to explain what a role does and when you'll use it by just covering the theory.

So later in the course, I'm gonna give you plenty of examples of the types of situations when you would and wouldn't use roles. Now there's one more concept that I want you to be super clear on, and that is an IAM policy or a policy document. IAM lets you create these policies which are essentially objects or documents which can be used to allow or deny access to AWS services when and only when they're attached to IAM Users, groups, or roles.

So policies on their own, do nothing, they simply define, allow or deny rights to certain services only when you attach the policies to other identities, so users, groups, and roles do they have any effect Now at a high level, IAM has three main jobs. Firstly, it's an Identity Provider or an IDP. It lets you create, modify and delete identities such as users and roles and it also authenticates those identities.

So when anyone attempts to make a request to AWS, they're known as a security principle and what they need to do is to prove their identity. I might claim to be an IAM User called Adrian in my account, but I need to be able to prove this. And so IAM authenticates me and generally this is using a username or password, but as you'll see later in the course there are other methods of authentication.

Now, assuming I prove my identity, IAM then authorizes me, or not to access AWS resources, so I'm either allowed or denied access to certain things. And this is based on policies associated with the identity that I authenticate with. Really try and remember these terms.

So you've got an ID provider which is a service that allows you to create and manage identities. You've got the authentication process which is where you are challenged to prove that you are the identity that you are claiming to be. And then once you're authenticated, you become an authenticated identity and then you're authorized or not to access AWS services.

Now we're almost done, I just have a few points I want you to remember And then it's demo time. IAM is provided for free there are no costs associated with creating users, groups, or roles. There are limits on how many of each you can have, and some of these limits actually matter for real world usage and for the exam, so I'm gonna go into more details on these later.

IAM is a global service, it's got one global database for your account and it's globally resilient. So it can cope with the failure of large sections of the AWS infrastructure. Now IAM only controls what its identities can do.

So IAM User or roles which you create in IAM, it allows or denies those identities to do things via policies. It doesn't allow direct control over external accounts, or users, so you can't use IAM to control what an external user in an external account can do. IAM only controls local identities in your account.

Lastly, IAM lets you make use of identity federation and multifactor authentication. Now don't be scared of these terms for now, identity federation lets you take identities that you already have. For example, your business's active directory, or WEB identities such as Facebook, Twitter, Google, and more and then use these indirectly to access AWS resources.

Don't worry about understanding it now, I just wanted to introduce the term and I'll be covering it extensively later in the course, including some demos to let you experience it yourself. I've already showed you multifactor authentication, we've added it to the Account Root User of the accounts have created. So when the Account Root User needs to log into that AWS account, they need to input the one time password that's generated by the MFA application on our phones.

And what you can see on the bottom right of your screen now is just an example of a physical MFA device. So this is a physical device that you'd carry with you along with your wallet and keys that would generate these one time passwords that you'd need to use when you log in. Okay, so that's all of the IAM basic theory that I wanted to cover, it's demo time.

Over the next few lessons, I'm going to show you how you can further secure your AWS accounts that you'll use for this course. I'm going to demo setting up IAM and creating an IAM admin user. Now, the reason we're gonna do this is to create a second user that will have full permissions on the AWS account.

So the IAM admin user in many ways is gonna function just like the Account Root User, but it will use IAM. Now the reason we are doing this is so that we can stop using the Account Root User. Remember, we only have one Account Root User and it's not possible to restrict the permissions of this user.

And so best practice is that it's only used to perform the initial account set up. Afterwards, we need to utilize IAM User, rather than the Account Root User, so that's what I'm gonna demonstrate. Now at this point once we've got this IAM admin user throughout the course as we need additional identities, we'll use this IAM admin user to create those additional identities which will be giving less permissions.

So remember it's always best practice to only get the permissions required to do a specific task. And so if I'm demonstrating a certain product or technology, generally we're gonna be using an IAM User that has just enough access rights to perform that task. So just like we did with the Account Root User, we're gonna create an IAM admin user in each of the course AWS accounts, so that's what's coming up next.

So at this point feel free to complete this video and when you're ready, join me in the next for the demo. ## aws-accounts-adding-iamadmin-to-general-account.txt Welcome back and in this demo lesson we're going to further secure our general AWS account and we're going to do that by creating an IAM identity which you're going to use for the remainder of the course. In general we don't want to use the account root user for anything for production usage or even while using this account for training.

It's not possible to restrict the account root user, you can't delete it or recreate it and so we should almost never use it. Normal process when you finished creating an AWS account should be to create a normal admin user, which will be given full control over the account and it will replace your usage day to day of the account root user. So we now have this general AWS account.

We have an account root user for this AWS account and we've secured it with one time password capability. But now what we're going to do is set up an IAM identity with admin permissions that we'll be using from this point onward in the course. So to do that, click in the services search box at the top and type IAM and then click IAM to move to the IAM console.

If you're going to sign on with any IAM identities, then you need to use a sign in URL for IAM users. And right now you'll see that it's in this format. It's HTTPS and then your account ID, which is unique to you, and then .signin.aws.amazon.com/console.

Now you can set an account alias. By default, this is set to your account ID, but we can make this sign in URL a little bit more friendly by setting an alias. And I like to keep this theme of general and production so that we can see which account it is that we're logging into.

So we're going to set an account alias. Now this account alias needs to be globally unique. So you need to set it to something which makes sense and has the word general in, but also is specific to you.

So to create this alias, go ahead and click on create. And then you need to enter your preferred alias in this box. and assuming that nobody else has used this alias, I can go ahead and click to save those changes.

There we go, I'm able to create the alias that I want, so that's great. You need to follow the same process, but pick a unique alias for you. Just make sure that it has the word "General" within it, so it's nice and easy to identify which AWS account you're logging into.

Next we're going to go ahead and create the IAM identity, which we're going to be using from this point onward in the course. and again, each IAM identity that we create is specific to the AWS account that it's created within so we're going to create an IAM identity called IAM admin but we'll be creating one in this lesson for the general AWS account and then later in this section you'll also be creating a similar identity for the production AWS account and these, just like the account root users, are completely separate identities. So go ahead and click on users, and then click on add users.

Now for the username we're going to choose IAMADMIN. This doesn't have to be unique globally, only within this account. So you won't currently have an identity called IAMADMIN, so you can also call your user IAMADMIN.

Now we are going to be granting this user access to the AWS Management Console, so check this box. And then because AWS are slowly introducing the Identity Center as their recommended place to create identities within AWS, you're offered the choice between creating a user in the Identity Center or creating an IAM user. Now so that you have experience of both, at this point we're going to create an IAM user later in the course you'll get some experience with the identity center but for now go ahead and click I want to create an IAM user and then we need to set a console password for the IAM admin user of the general AWS account.

Now again you can use a password manager to auto generate this on your behalf but you do need to make sure that you note it down. So click on custom password and then enter your chosen password within this box. I'm going to choose to generate a password using my password manager and then I'm going to uncheck users must create a new password at next sign in because I don't want to have to change the password when I first log in to the account and I suggest you do the same.

So uncheck this box and then click to move on. Now we need to give this identity some permissions. Initially it won't have any permissions except those to change the password and basic interaction permissions for the AWS console.

So we need to give it admin permissions so go ahead and click attach existing policies directly. You could add this user to a group which might have existing permissions or you could copy the permissions from an existing user. In our case though because we don't have either of these already configured we're going to attach an existing policy directly.

I'll be talking about all this functionality elsewhere in the course. For now though, locate administrator access which is a policy which grants full admin control over this AWS account, check the box and this will mean that this managed policy is going to be associated or attached to this IAM user and then click to move on and then you can go ahead and click to create the IAM admin user. You should see that this has been created successfully and you're even able to click to send an email with login instructions to this user but we're not going to do that we're just going to go ahead and click return to users list and then close down any extra dialogue.

Now at this point go ahead and click on dashboard. What we need to do now is to test that we can successfully login as this IAM identity. Remember we want to use this for the remainder of the course rather than use the account root user of the general AWS account.

So what I want you to do is to copy the sign in URL for IAM users into your clipboard and you should probably note this down somewhere safe because this is going to be the URL that you'll use whenever you want to log in to the general AWS account using this IAM user from now on. So make sure that that's copied into your clipboard and then just go to that URL so paste that into your address bar and then open it. Now this is going to log you out of the account root user and present you with a slightly different login screen, in this case sign in as an IAM user.

You'll see that this box has been pre-populated and it will either have the account ID or the account alias. Because I created an alias you'll see that it's using my alias, in your case it should be different. Go ahead and enter IAM admin in the IAM username box then you'll need to enter the password that you picked in the previous step for the IAM admin user of the general AWS account.

Once you've entered all of that information go ahead and click on sign in and now you're logged into the management console but this time instead of using the account root user of the general AWS account this time you're using an IAM user. If you click on this drop-down you'll be able to see that you're using IAM user IAM admin and it lists your account number next to my account but it's easy to know that we're logged in as an IAM identity because it says it at the top of this drop-down. Now this IAM identity has administrator access and so it does have full control over this account the same level of access as the account root user of this AWS account but from this point forward we're going to be using this account rather than the account root user.

Now because this is an admin account we do need to fully secure it. So we need to set up one-time passwords in the same way that we did for the account root user. So to do that click on this drop down and go to my security credentials and we need to follow the same process that we did for the account root user.

So scroll down and now we need to click assign MFA device under multi-factor authentication. Remember because this is done per identity within each AWS account, we don't currently have one assigned because previously we set the one up for the account root user. We need to set this up again with a new one-time password profile in your software application for this specific identity.

So we're not reusing the one that we previously set up for the account root user. Now we need to give this MFA device a name. So you can put anything here.

I'm going to pick something that makes sense to me. Just make sure that it has I am admin somewhere in that name to help you distinguish from the account root user MFA device name. And then you're allowed to choose an MFA device type.

Now the options that we currently have available, we've got Authenticator App, Security Key or Hardware TOTP Token. Now for this demo we're going to pick Authenticator App. So go ahead and select that option and then click on Next.

And you need to follow the same process. You'll need to click Show QR Code and then scan that QR Code as a new entry within your Authenticator application. Don't reuse the one that you already have.

Once you've scanned that QR code and created the new entry in your authenticator application, the new entry for the IAM admin user of the general AWS account, then you'll need to enter two consecutive MFA codes that are generated by this new entry. And again this may take a few moments to do because you need to enter two consecutive codes and once you've done that you can click on add MFA and then we need to log out and log back in again to test this one-time password. So click on this drop down and click on sign out.

You'll need to once again use the URL that you noted down in the previous step which is the sign in URL for IAM identities of the general AWS account. You should see the account ID or account alias pre-populated once again. Make sure that it is your alias for your general AWS account.

Enter IAM admin for the IAM username. Once again you'll need to enter the password that you chose. Click on sign in.

This time you'll be prompted for a one-time password because that's what we've just set up. So enter that in this box and then click to login to the AWS console. And there we go we now require a one-time password as well as the username and normal password to log in to this IAM admin user.

Now just to reiterate what we've done we've created a separate identity so IAM admin within the general AWS account so this is a separate identity from the account root user of the general AWS account. From this point forward we won't be using the account root user of the general account we'll be using the IAM admin identity of the general account. Now because this is an administrator user just like we did for the account root user of the general account we've configured multi-factor authentication for this IAM admin identity.

It's a separate entry in your authenticator application so now you should have two. One for the account root user of the general account and one for the IAM admin user of the general account. And this means now that in order to log into this IAM admin identity of this general AWS account you need the sign in URL, the username, the password and the one-time code.

Now at this point that's everything that you need to do within this demo lesson. Go ahead and complete this video and when you're ready I'll look forward to you joining me in the next. ## aws-accounts-adding-iamadmin-to-production-account.txt Welcome back and in this demo lesson we're going to be following on from the previous demo lesson only this time we're going to be creating the IAM admin identity inside the production AWS account.

So what I'll need you to do is make sure that you're logged into the production AWS account using the account root user. It should say production on this drop down at the top. While you're doing that, also get into the habit of making sure that you have the US-East-1 region selected in this dropdown at the top right of the screen.

We're going to be following exactly the same process to create the IAM admin user. So move across to the IAM console. The quickest way is to click in the search box at the top and type "IAM" and then click to move across to the IAM console.

And we need to go ahead and create an account alias for the production AWS account So go ahead and look on the right hand side of the screen and click on create Now you want to make sure that this production account alias is in a similar format to the one you created for the general AWS account And instead of general I'll be using production Again this needs to be globally unique, it should mention production and you should use the same structure as you used when creating your general account alias. So go ahead and enter the alias and click on save changes. Once you've done that go ahead and note this down somewhere safe because you'll need it whenever you want to log in to the production AWS account using an IAM identity.

Now that we've set that we can click on users and go ahead and create the IAM admin user for the production AWS account. Now for the username we're going to choose IAM admin. This doesn't have to be unique globally only within this account so you won't currently have an identity called IAM admin so you can also call your user IAM admin.

Now we are going to be granting this user access to the AWS management console So check this box. And then because AWS is slowly introducing the identity center as their recommended place to create identities within AWS, you're offered the choice between creating a user in the identity center or creating an IAM user now, so that you have experience of both at this point, we're going to create an IAM user later in the course, you'll get some experience with the identity center, but for now, go ahead and click I want to create an IAM user and then we need to set a console password for the IAM admin user of the production AWS account. Now again you can use a password manager to auto generate this on your behalf but you do need to make sure that you note it down.

So click on custom password and then enter your chosen password within this box. I'm I'm going to choose to generate a password using my password manager and then I'm going to uncheck "Users must create a new password at next sign in" because I don't want to have to change the password when I first log in to the account and I suggest you do the same. So uncheck this box and then click to move on.

Now we need to give this identity some permissions. Initially it won't have any permissions except those to change the password and basic interaction permissions for the AWS console. So we need to give it admin permissions.

So go ahead and click attach existing policies directly. You could add this user to a group which might have existing permissions or you could copy the permissions from an existing user. In our case though, because we don't have either of these already configured, we're going to attach an existing policy directly.

I'll be talking about all of this functionality elsewhere in the course. For now though, locate administrator access which is a policy which grants full admin control over this AWS account, check the box, and this will mean that this managed policy is going to be associated or attached to this IAM user, and then click to move on. And then you can go ahead and click to create the IAM admin user.

You should see that this has been created successfully, and you're even able to click to send an email with login instructions to this user, but we're not going to do that. We're just going to go ahead and click return to users list and then close down any extra dialogue. Now at this point, go ahead and click on dashboard.

What we need to do now is to test that we can successfully log in as this IAM identity. Remember, we want to use this for the remainder of the course, rather than use the account root user of the production AWS account. So what I want you to do is to copy the sign in URL for IAM users into your clipboard.

And you should probably note this down somewhere safe and then just go to that URL. So paste that into your address bar and then open it. Now this is going to log you out of the account root user and present you with a slightly different login screen.

In this case, sign in as an IAM user. You'll see that this box has been pre-populated and it will either have the account ID or the account alias. Because I created an alias, you'll see that it's using my alias.

In your case, it should be different. Go ahead and enter "iamadmin" in the IAM username box. Then you'll need to enter the password that you picked in the previous step for the IAM admin user of the production AWS account.

Once you've entered all of that information, go ahead and click on Sign In. And now you're logged in to the management console, but this time instead of using the account root user of the production AWS account, now you're logged in to an IAM user of that same AWS account. If you click on this dropdown, you'll be able to see that you're using IAM user IAM admin, and it lists your account number next to my account.

But it's easy to know that we're logged in as an IAM identity because it says it at the top of this dropdown. Now this IAM identity has administrator access and so it does have full control over this account the same level of access as the account root user of this AWS account but from this point forward we're going to be using this account rather than the account root user Now because this is an admin account we do need to fully secure it so we need to set up one-time passwords in the same way that we did for the account root user So to do that click on this drop down and go to my security credentials and we need to follow the same process that we did for the account root user. So scroll down and now we need to click assign MFA device under multi-factor authentication.

Remember because this is done per identity within each AWS account we don't currently have one assigned because previously we set the one up for the account root user. We need to set this up again with a new one-time password profile in your software application for this specific identity so we're not reusing the one that we previously set up for the account root user. Now we need to give this MFA device a name so you can put anything here I'm going to pick something that makes sense to me just make sure that it has I am admin somewhere in that name to help you distinguish from the account root user MFA device name and then you're allowed to choose an MFA device type.

Now the options that we currently have available we've got authenticator app, security key or hardware TOTP token. Now for this demo we're going to pick authenticator app so go ahead and select that option and then click on next and you need to follow the same process. You'll need to click show QR code and then scan that QR code as a new entry within your authenticator application.

Don't reuse the one that you already have. Once you've scanned that QR code and created the new entry in your authenticator application then you'll need to enter two consecutive MFA codes that are generated by this new entry and again And this may take a few moments to do because you need to enter two consecutive codes and once you've done that you can click on Add MFA. And then we need to log out and log back in again to test this one time password.

So click on this drop down and click on Sign Out. You'll need to once again use the URL that you noted down in the previous step which is the sign in URL for IAM identities of the production AWS account. You should see the account ID or account alias pre-populated once again.

Enter IAMADMIN for the IAM username. Once again you'll need to enter the password that you chose. Click on sign in.

This time you'll be prompted for a one-time password because that's what we've just set up. So enter that in this box and then click to log in to the AWS console. And there we go, we now require a one-time password as well as the username and normal password to log in to this IAM admin user and now you've finished the account setup and account securing process.

You have two AWS accounts, the general account and the production account. Both of those AWS accounts have their own individual account root user. Both of them have an IAM identity, it's an IAM user called IAM admin and for IAM admin in both of those accounts you've configured MFA so we have four different identities split across two different accounts and all four identities are fully secured so you need a username a password and a one-time password.

Now that's everything that you'll need to do in this demo lesson go ahead and complete the video and when you're ready I look forward to you joining me in the next. ## aws-accounts-iam-access-keys.txt Welcome back, and by this point, you've got a set of working AWS accounts. You've configured the account security, added billing alarms, set up IAM and created an IAM admin user, and then completed all of that with multifactor authentication.

So far, the AWS access that we've experimented with has been using the console UI in a web browser. It is possible to access AWS using the command line, or even within other applications using APIs, or application programming interfaces. Authentication via the command line is not done via username, password, and MFA.

It's done using IAM Access Keys, and that's the subject of this lesson. So let's jump in and get started. Access keys are long-term credentials available within AWS.

They're not the only type of long-term credential that you need to be aware of. And all long-term credentials are used with IAM users. If you're authenticating to AWS, and you're doing so using an IAM user identity, then generally you'll either use a username and password when you're using the console UI, or access keys when you're using the command line interface.

Now, they're called long-term credentials, because they don't change regularly or rotate. You as the owner of the credentials have to explicitly change them. For example, updating your password.

Access keys, in many ways, are similar to the username and password that you've used to this point, but there are a number of crucial differences. An IAM user has one username and one password. It can't have anymore.

Now, you can actually create IAM users which are only used for command line or API access. And for those, you don't need to assign a password. So a password on an IAM user is actually optional.

The important thing, though, is an IAM user can't have more than one username or one password. Now, you can change the password, but it only ever has a maximum of one at a time. Now, if I ever refer to credentials throughout this course, and a username and password is an example of a set of credentials, there is normally a public part and a private part to those credentials.

With usernames and passwords, the username is the public part of those credentials, and the password is private. You don't need to worry too much if somebody knows your username, but if they know your username and password in conjunction, then that's known as a credential leak, and you're in trouble. An MFA is just another private part to your credentials.

It makes it harder to leak the full credential set. The first difference with access keys is an IAM user can have two sets, two access keys. It can have zero, one or two, but never more.

Access keys can be created, deleted, made inactive, or made active. And logically they default when they're created to be the active state. Now, like username and password credential sets, access keys are actually formed from two parts.

The first part is the access key ID, and the second part is the secret access key. The access key ID looks something like this, and the secret access key, that's longer and more complex. When you create access keys, and I use that term to refer to both parts of the credentials, AWS provides both of these to you, so you're given both the access key ID and the secret access key when you create that set of credentials.

Now, once you're initially provided with both the access key ID and the secret access key, from that point onward, there's no ability to get access again to the secret access key. AWS don't allow any future downloads of the secret access key part of a set of access keys. You can only ever see the access key ID, so it's especially important that that initial time, when you're provided with both, you note down the secret access key and store it safely and securely.

When you make a request to AWS using the command line interface, you use both of these parts, so the public part and the private part. Now, the access key ID, in many ways, is like an IAM username. And the secret access key is like a password.

If you let anyone have access to the secret access key, then it can be used to act as that IAM user, so you need to be really sure that whenever you store the access key ID and the secret access key, you keep the secret access key safe and secure. Now, if you do misplace the secret access key, or you concerned that your credentials have been leaked, then you can't change the secret access key. You need to delete the entire access key, so that's both parts, the access key ID and the secret access key, and then recreate it.

And that will give you a brand new set of credentials, so a brand new access key ID and a brand new secret access key. Now, if you have any command line interfaces or applications, which are configured to use access keys, and you make that set of credentials inactive or delete them, then the command line interface or application will stop working until you either make it active again or generate a new set, and then update those command line interfaces or applications with the new details. If you ever hear the term "Rotating access keys," it simply means to create a brand new set and remove the old one.

It's no more complex than that. That's why an IAM user can have two sets. Generally, if utilizing the first set, then to rotate them you'll create a second set, update all of your applications and command line utilities to that new set, and then delete the old one.

Now, with the exception of the account root user, which can also have access keys, although that's not recommended, IAM users are the only identity which uses access keys, so the only identity that uses long-term credentials. IAM roles don't use access keys. And I'll talk more about those in the IAM section of the course later on.

For now, I just wanted to introduce the basics. It's security related, and I want you to understand how it works from the offset. Now that you've learned the theory of access keys, it's time to experiment.

Now, we're gonna have a demo, and in that demo, we're gonna create access keys in both the general AWS account and the production AWS account. Once you've created those access keys, I'll be showing you how to download and configure the AWS command line tools. And as part of that process, you'll be using these access keys and configuring the command line tools to be able to connect to both the general and the production AWS account.

So at this point, that's everything you need to do. Go ahead, complete this lesson, and when you're ready, I'll see you in the next. ## aws-accounts-creating-access-keys-and-aws-cli-v2-tools.txt Welcome back, and in this lesson, you're going to create access keys for both the iamadmin user in the general AWS account as well as the iamadmin user in the production AWS account, and then I'm going to step you through how to install the AWS command-line tools and configure those tools to access the AWS products and services using the access keys that you create.

So this is going to put you in a position where you're able to use the AWS command-line utilities to interact with both the general AWS account and the production AWS account. Now we're going to start off in the general AWS account, so you'll need to be logged in as the iamadmin user of the general AWS account. Assuming that you are, click on the account drop-down and then select Security credentials because this is where you configure access keys.

So as I mentioned in the previous theory lesson, access keys can be created for IAM users, and this is what we're going to do here. So to create a set of access keys, it's as simple as scrolling down slightly and then clicking Create access key. Now, when you create an access key, you'll need to specify what its intended use is.

In this particular case, we're using it with the Command Line Interface, so we're going to go ahead and check this top box, then scroll down to the bottom and check the understanding confirmation box and click on Next. You'll need to give the access key a description, so I'm gonna go ahead and put LOCAL CLI IAMADMIN-GENERAL in this box. If this were production, you might put the intended purpose or you might put who the access keys are assigned to.

In any case, I'm not going to be using these access keys because I'm going to recreate them in a few moments. So I'm gonna go ahead and click on Create access key. Now, when you create access keys, you're presented with two main pieces of information, the access key, which is this text on the left, and this is non-sensitive information.

You can think of this much like a username. On the right though, we have the secret access key, and this is the secret part, the sensitive part. Anyone with both of these pieces of information can access your AWS account, and so we need to be extremely careful with showing anyone the secret access key.

So for security reasons, I'm not going to show this on screen. I'm gonna go ahead and click on Done, and we can see that now we have one access key created. Now, when you've got a set of access keys, you can click on Actions and go to Deactivate and then confirm to deactivate that access key, and the reverse of this is you can click on Actions and then Activate to reactivate those access keys, and that's useful if you want to suspend access for any reason.

Now, an individual identity can have two sets of access keys. So I could go ahead and click on Create access key again, check this box at the top, scroll down, check this understanding box, click on Next, and enter something into this box and click Create access key, and then I'll click on Done and Continue, and you can see that we have two different access keys created, but we can't create a third. You can only have two access keys, either active or inactive, per identity within AWS.

So I can't create another set of access keys. Now, the ability to have two is useful if you want to rotate access keys. At this point though, I'm gonna go ahead and delete both of these because we're not going to use them.

So click on Actions and then Delete. You'll see that you need to deactivate an access key before you can delete it, so I'll click on Deactivate, and then I'll need to paste in the access key ID into the box and click Delete, and I'll follow the same process for the other access key, and that puts us in the position where we have no access keys for this identity. So now we're going to create the access keys properly that we're going to use with the Command Line Interface.

So go ahead and click on Create access key again. Check the Command Line Interface box. Scroll down to the bottom.

Check this box and click on Next, and then enter a description. I'm going to use LOCAL CLI IAMADMIN-GENERAL, and then click on Create access key. Now you're not able to get access to the secret access key from this point forward if you don't either show it or save it.

So if you ever lose access to the secret access key, you'll need to regenerate the access keys. Now, what I suggest we do is click on Download .csv file, and this is going to save these access keys to a file called iamadmin_accesskeys. Because these are the access keys for the general AWS account, I want you to go ahead and rename this file to iamadmin_accesskeys_general.

Once you've done that, you can go ahead and click on Done, and now we're going to do the same for the production AWS account. Now, I have both of these accounts open in separate browser session tabs. If you don't have this capability, if you don't use Firefox and don't have this add-on, then you'll need to log out of the general AWS account and then re-log in as the iamadmin user for the production AWS account.

Once you've done that, click on the account drop-down at the top right and move to Security credentials. Once you're there, scroll down. Click Create access key again.

Check the box for Command Line Interface. Check the acknowledge box and then click on Next, and then in the description box, go ahead and use the same format, so LOCAL CLI IAMADMIN-PRODUCTION, and click Create access key. Then once again, click on Download .csv file and rename this file to iamadmin_accesskeys_production, and once you've done that, you can go ahead and click on Done, and now we've created the two sets of access keys that we'll use with the Command Line Interface.

Next, you'll need to install version 2 of the AWS Command Line Interface. Now, I've included a link attached to this lesson which details how to download and install the AWS command line for Windows, Linux and macOS. The installation process isn't all that complex.

The important part is the configuration, and the configuration is the same on all of the supported operating systems. So if you open up the URL that's attached to this lesson, it will open a page which should look something like this. You'll see that there are instructions for Linux, macOS and Windows.

So select the correct operating system, so the operating system that you're using on your local machine. If you scroll down, you'll see instructions on how to install it on your particular operating system and you'll find a link to an installation package. So go ahead and click that link and that will open the installation.

We'll be accepting all of the defaults no matter what the operating system. So just perform a default installation. The installation will take a few minutes to complete.

Once it's completed, click on Finish or close down the installation application. Again, this is slightly different depending on which operating system you're using. Then we need to move across to our command prompt or terminal, depending on which operating system you're using.

If I just run an aws and press Enter, if I see usage instructions which look like this, then it's been completed successfully. If you see an error indicating that the application or the command is not found, then you might need to restart your operating system, but in this case, it's completed successfully. You can verify it properly by running aws space -- and then version and press Enter, and if it's working correctly, you should see aws-cli and then a version 2.something.something.

The important part is version 2 because this brings significant enhancements over version 1 that we will be using in this course. What we're going to do now is configure the Command Line Interface. Now, the way that the command line is integrated with our AWS accounts, or more specifically, our identities or users in those accounts, is we need to configure a set of credentials which the Command Line Interface will use to communicate with AWS.

Now, the way that we configure these credentials is to run an aws and then space and then the word configure. Now, if we just use aws configure, then this configures the default configuration profile for the Command Line Interface, and this default configuration profile is what's used if we don't specify what's known as a named profile. So the Command Line Interface allows us to specify named profiles and it's these that we can use to configure multiple AWS accounts.

So we can have a named profile for the iamadmin user in the general AWS account, and we can have another named profile for the iamadmin user in the production AWS account, and that's what we're going to do. So to configure a named profile, all we do is add a space on the end and then --profile and then a space and then the name of this profile. Now, what I suggest you use is iamadmin- and then general.

So this is the name of the profile that will connect to the iamadmin user in the general AWS account. Logically, for the named profile for the production account, we'll be using iamadmin-production. So first, let's configure the profile for the iamadmin user in the general account.

So it should say aws space configure space --profile space iamadmin-general. Go ahead and enter that and press Enter. Now at this point, it's going to ask for a number of pieces of information.

It's going to ask for the access key ID. It's going to ask for the secret access key. It will ask for a default region and then a default output format.

So first, we'll need these credentials. Now, these are contained in these files that you saved earlier. So first, you'll need to open up the document which contains the word general.

So these are the credentials for the iamadmin user inside the general AWS account. So open up this document. Now, this document will contain an access key ID and then a comma and then it will contain the secret access key.

So you need to copy down the access key ID, so the part before the comma. Don't include the comma. Copy that into your clipboard, and then paste this in where it says Access Key ID, and it should look something like this.

Make sure you get all of the characters and then press Enter. Then it will ask for the secret access key, which is the part after the comma within the credentials document. So copy that into your clipboard and then paste that in, and then press Enter.

Next, it will ask for a default region, and we're always going to use Northern Virginia, which is us-east-1. So go ahead and enter that and then press Enter, and then for the default output format, you can just go ahead and press Enter and we'll use the default of None. Now at this point, the Command Line Interface has been configured to integrate with the iamadmin user of the the general AWS account, and to test that, we can use aws space s3 space ls and then a space.

Now this will run a listing of any S3 buckets in this account, and if we don't have any buckets, it will simply return an empty string, and that's fine, but if it returns an error, then we know we have a problem. Now, if we just ran this command on its own, we would get an error because we haven't configured any credentials as part of the default profile. So it will tell us, "Unable to locate credentials." Because we've configured these credentials inside a named profile, we need to specify that named profile on the command line.

So I'm just gonna type that command in again and then follow it with --profile and then a space and then I'm going to use the named profile that I've configured previously, so iamadmin-general. This time, if I press Enter, now that I run the command with the named profile, we won't get the error. This time it will return an empty string, and that's fine because we don't have any S3 buckets within this account.

It's a brand-new account. If you've already created any S3 buckets or if you already have any resources in this account, which you shouldn't do because it's a brand-new account, you might see a list of buckets, but if you're following the instructions as I'm giving them, you should have an empty list here, and that's fine. The only thing you need to worry about is if you receive an error message.

If you receive an error message, it probably means that you haven't copied down either the access key ID or the secret access key in their entirety, and to fix that, you can just go ahead and rerun the aws configure command with this named profile on the end. If we just rerun this, it will offer us the ability to just re-enter those values, but in this case, because we didn't get an error, we don't need to do this. The next thing we need to do is to follow the same process but this time for the iamadmin user inside the production AWS account.

So to do that, aws space configure space --profile space iamadmin-production, and then press Enter and you'll be prompted for those same four pieces of information. So now we need to open the iamadmin credentials for the production AWS account. You'll see the format is the same.

We'll need to copy down the access key ID, which is everything before the comma. Copy that into your clipboard. Paste that in and press Enter.

Then the secret access key, everything after the comma, copy that into your clipboard. Paste that in and press Enter. Again, the region will be us-east-1, so enter that and press Enter, and then press Enter again so that we don't set a default output format, and now we should be able to run aws space s3 space ls space --profile space iamadmin-production, and again, press Enter, and again, if we don't receive an error, if either we receive this empty string or a list of buckets, that means everything's working as expected.

Now, just before I finish up with this lesson, I've been fairly open with showing you these credentials on screen. Now, this is a huge security risk. If you have these credentials right now, then you could log in to my AWS account.

Now, when I'm recording this lesson, what I'm going to do is replace these credentials. So although I've configured my Command Line Interface using these credentials, the minute I stop recording, I'm gonna go back to the AWS console, delete these access keys, and then reconfigure my command line with brand new credentials. The outcome will be the same, but it simply means that I'm invalidating the credentials that you've seen on this video.

For day-to-day usage and for your purposes, you should never show these credentials to anyone who you don't want having access to your AWS account. So whenever you generate credentials, it's important to understand that for anybody who has the access key ID and the secret access key, they can utilize the IAM identity that you've configured together with any permissions that that identity has over this AWS account. So if you leak your iamadmin credentials, then anyone who has those credentials can interact with either your general or production AWS accounts as the iamadmin user.

Because that user has full administration permissions on the account, the results of that can be disastrous. So you need to get into the habit of being extremely careful where you store these credential files and to whom you grant access. So it's really important to start off being really paranoid and really careful about these credentials, and going a step further, at this point, you should probably delete both of these credential files, so the one for the general AWS account and the one for the production AWS account, and that just means that all of these credentials are safely configured within the Command Line Interface, are not stored anywhere where they can be accessed by anyone but you.

Now at this point, you've configured everything that you need to as part of this lesson. So you've set up the AWS Command Line Interface and you've configured two named profiles, iamadmin-general and iamadmin-production, and these are what we're going to use throughout the rest of this course whenever we need to do any work using the command line. At this point, you've done everything that you need to, so go ahead and complete this video, and when you're ready, I look forward to you joining me in the next lesson.

