<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Cloud Security with AWS IAM

**Project Link:** [View Project](http://nextwork.ai/projects/aws-security-iam)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-security-iam_1c864649)

---

## Introducing Today's Project!

### Project overview

In this project, I will demonstrate how to configure secure access control using AWS IAM by creating custom IAM policies and user groups. I am doing this project to learn how to restrict permissions for development and production EC2 instances, manage separate IAM users, and implement real-world cloud security principles to ensure users only have the exact access they need to do their jobs.

### Tools and concepts

The services I used in this project were Amazon EC2 and AWS IAM to secure our cloud infrastructure. Key concepts I learnt include writing custom IAM policies using JSON, managing permissions scaleably via IAM user groups, restricting actions to specific environments using resource tags, and configuring an account alias to simplify console logins for IAM users.

### Project reflection

This project took me approximately 1 hour to complete. The most challenging part was configuring the custom JSON policy conditions to restrict actions based on specific tags. It was most rewarding to log in with the new IAM user credentials and successfully verify that production EC2 instances were protected while development servers remained fully manageable.

---

## Tags

### What I did in this step

In this step, I will launch two Amazon EC2 instances representing different environments in the AWS console. I am doing this because we need to boost NextWork's overall computing power to support upcoming student traffic, while setting up distinct virtual servers where we can safely test secure access control using AWS IAM policies.

### Understanding tags

Tags are key-value pairs that assign custom metadata to your AWS resources. They are incredibly useful for labeling, organizing, and searching for your assets, as well as managing costs and applying targeted security permissions to specific groups of EC2 instances.

### My tag configuration

The tags I’ve used on my EC2 instances are called Name and Env. The values I’ve assigned for my instances are nextwork-dev-Granada and development for the development environment, and nextwork-prod-Granada and production for the production environment.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-security-iam_2e0e5a5d)

---

## IAM Policies

### What I did in this step

In this step, I will create a custom IAM policy using a JSON policy document in the AWS IAM console. I am doing this because we need to define specific permissions that allow our new intern to manage the development EC2 instance while strictly restricting them from modifying or accessing our production environment to maintain strong cloud security.

### Understanding IAM policies

IAM policies are JSON documents that define permissions by specifying what actions are allowed or denied on AWS resources. They are attached to IAM users, groups, or roles to safely manage access and enforce the principle of least privilege.

### The policy I set up

For this project, I’ve set up a policy using JSON instead of the visual editor. I chose this method because pasting a pre-defined JSON policy document allows me to easily configure precise security parameters, such as restricting Amazon EC2 actions to only apply when resources have a specific development tag.

### Policy effect

I’ve created an IAM policy that grants full Amazon EC2 management permissions only when the resource has an Env tag value of development. It also allows viewing all instances while strictly denying the ability to create or delete resource tags so users cannot bypass these security restrictions.

### Understanding Effect, Action, and Resource

In a JSON policy, the Effect attribute specifies whether the permission is allowed or denied (using Allow or Deny), the Action attribute lists the specific AWS API operations that can be performed, and the Resource attribute defines the exact AWS assets to which this statement applies.

---

## My JSON Policy

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-security-iam_1c864649)

---

## Account Alias

### What I did in this step

In this step, I will create a custom Account Alias for my AWS account to replace the default 12-digit account ID in the sign-in URL. I am doing this because a friendly, customized alias makes the login link to the AWS Management Console much easier to remember and share when onboarding our new IAM users.

### Understanding account aliases

An account alias is a unique, friendly name that you can create to replace your 12-digit AWS account ID in your login URL. It simplifies the sign-in process for IAM users by making the URL to access the AWS Management Console much easier to remember and share with your team.

### Setting up my account alias

Creating an account alias took me about 2 minutes. Now, my new AWS console sign-in URL is https://nextwork-alias-granada.signin.aws.amazon.com/console/, which is much easier to remember and share than using my 12-digit AWS account ID.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-security-iam_0eb4439b)

---

## IAM Users and User Groups

### What I did in this step

In this step, I will create a dedicated IAM user group called nextwork-dev-group, attach our custom environment policy to it, and set up a new IAM user for our intern with AWS Management Console access. I am doing this because managing permissions at the group level simplifies user administration, ensuring our new intern automatically inherits the precise permissions they need to work on development resources safely without affecting production.

### Understanding user groups

IAM user groups are collections of IAM users that allow you to manage permissions for multiple accounts at once. Instead of attaching IAM policies to each individual person, you attach them directly to the group so that every member automatically inherits the same security settings, simplifying administrator tasks as your team grows.

### Attaching policies to user groups

I attached the policy I created to this user group, which means any IAM user added to this user group will automatically inherit those defined permissions. This ensures our new DevOps intern can instantly manage the development EC2 instance without us having to configure policies individually, making it easy to securely scale access controls in AWS IAM.

### Understanding IAM users

IAM users are individual identities created within an AWS account that represent specific people or services that need to interact with AWS resources. Each user has their own unique security credentials, such as a custom password for the AWS Management Console, and can be assigned specific permissions using IAM policies to safely control what they can see and do.

---

## Logging in as an IAM User

### Sharing sign-in details

The first way is to open a private or incognito browser window and sign in using our custom account alias login URL as the new IAM user. This lets me directly test the security configurations from the intern's perspective, verifying that they can successfully manage the development EC2 instance while being strictly blocked from altering the production server.

### Observations from the IAM user dashboard

Once I logged in as my IAM user, I noticed that several panels on the AWS Management Console dashboard displayed Access denied errors. This was because my new user account only has permissions defined by our custom IAM policy, which strictly limits my permissions to managing development EC2 instances and does not grant any access to other AWS services or global account settings.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-security-iam_6f2ab446)

---

## Testing IAM Policies

### What I did in this step

In this step, I will log into the AWS Management Console using the intern's IAM user credentials and attempt to stop both the production and development EC2 instances. I am doing this because we must test and verify that our newly created IAM policy successfully restricts access to the production environment while safely allowing the intern to manage development resources.

### Testing policy actions

I tested my JSON IAM policy by logging in with the intern's IAM user credentials and attempting to stop both of our virtual servers. I verified that trying to stop the production instance resulted in an authorization error, whereas stopping the development EC2 instance was successful, proving that our resource-based tags are correctly enforcing permissions.

### Stopping the production instance

When I tried to stop the production instance, the console displayed an unauthorized error banner. This was because the custom IAM policy attached to my IAM user group restricts Amazon EC2 management actions to resources tagged with a development environment value, ensuring the production EC2 instance remains secure and protected from unauthorized changes.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-security-iam_0e7a9d6a)

### Stopping the development instance

When I tried to stop the development instance, the action was successful and the state immediately changed to stopping. This was because our custom IAM policy explicitly grants Amazon EC2 management permissions for resources tagged with an Env value of development, proving that the restricted access we configured is working exactly as intended.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-security-iam_1811801c)

---

## IAM Policy Simulator

To extend my project, I'm going to configure a strong password policy and enable Multi-Factor Authentication for my intern's IAM user. I'm doing this because enforcing credential complexity and requiring a second layer of verification are essential cloud security practices that safeguard our AWS account from unauthorized access.

### Understanding the IAM Policy Simulator

The IAM Policy Simulator is a testing tool provided by AWS that allows you to evaluate and debug IAM policies in a safe, simulated environment. It is useful for testing whether specific permissions are successfully allowed or denied for your IAM users, groups, or roles without having to log in as those users or run actual actions on live resources, making security troubleshooting significantly faster and safer.

### How I used the simulator

I set up a simulation for our DevOps intern's IAM user to test their permissions to stop Amazon EC2 instances. The results were that the action was allowed for resources with the development tag, but denied for production resources. I had to adjust the simulator's context attributes to include our specific Env resource tag to ensure the IAM Policy Simulator could accurately evaluate our resource-based security restrictions.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-security-iam_069d8a621)

---

---
