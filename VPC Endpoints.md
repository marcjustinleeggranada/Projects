<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Endpoints

**Project Link:** [View Project](http://nextwork.ai/projects/aws-networks-endpoints)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## VPC Endpoints

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-endpoints_09bcaa8a)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a logically isolated virtual network defined in the AWS cloud, and it is useful because it gives you complete control over your virtual networking environment, enabling you to launch resources like EC2 instances into secure, custom subnets with tailored route tables and network gateways.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to establish a highly secure, private connection between my EC2 instance and an Amazon S3 bucket. By configuring a gateway VPC endpoint and updating my public subnet's route table, I routed all S3-bound data traffic directly through AWS's internal network, allowing me to restrict bucket access with a strict bucket policy that blocks all public internet access while keeping our private server communications open and secure.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how applying the strict S3 bucket policy would immediately block my access to the bucket's objects inside the AWS Management Console. Since my web browser request was coming from the public internet rather than our private VPC endpoint, the policy worked exactly as designed by locking my console view out, which really drove home how powerful and instantaneous AWS resource-based policies can be.

### This project took me...

This project took me approximately 45 minutes to complete, spanning from the initial VPC setup to the final testing of our policy restrictions. The most valuable part of the time was spent configuring the secure S3 bucket policy and seeing it interact with our gateway VPC endpoint to instantly lock down public network access while keeping our internal data pathway open.

---

## In the first part of my project...

### Step 1 - Architecture set up

In this step, I will build the baseline cloud infrastructure by creating a VPC, launching an EC2 instance, and provisioning an Amazon S3 bucket because I need these foundational resources ready before I can test and secure their network communications.

### Step 2 - Connect to EC2 instance

In this step, I will connect directly to my EC2 instance using EC2 Instance Connect because I need to gain terminal access to the server to verify its baseline outbound internet path to my S3 bucket before we restrict public access.

### Step 3 - Set up access keys

In this step, I will create access keys for my IAM user and configure them on my EC2 instance because the server requires these programmatic credentials to securely authenticate and access my S3 bucket.

### Step 4 - Interact with S3 bucket

In this step, I will connect back to my EC2 instance and run S3 commands using the AWS CLI to copy a test file to my S3 bucket because I need to verify that our configured access keys successfully authorize the server to interact with AWS services over the public internet.

---

## Architecture set up

I started my project by launching a custom VPC with one public subnet and provisioning a new EC2 instance to use as my test server

I also set up an Amazon S3 bucket named nextwork-vpc-project-marc and successfully uploaded two sample image files to prepare the bucket for testing secure, private access from our server.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-endpoints_4334d777)

---

## Access keys

### Credentials

To set up my EC2 instance to interact with my AWS environment, I configured my Access Key ID, my Secret Access Key, my default AWS Region, and the default output format using the AWS CLI.

Access keys are programmatic AWS credentials consisting of an Access Key ID and a Secret Access Key. They allow developers, applications, and external servers to securely authenticate and issue commands to AWS services via the AWS CLI or programmatic APIs without needing to log into the AWS Management Console.

Secret access keys are private, cryptographic credentials that function as the password paired with an Access Key ID. They are used by the AWS CLI or applications to sign and authenticate programmatic requests to AWS, and they must be kept highly secure because they grant direct access to resources within your AWS account.

### Best practice

Although I'm using access keys in this project, a best practice alternative is to use an IAM role attached directly to the EC2 instance. By leveraging an IAM role, the instance automatically acquires temporary, self-rotating security credentials to access Amazon S3 securely without the need to store long-lived credentials on the server's local file system.

---

## Connecting to my S3 bucket

The command I ran was aws s3 ls. This command is used to list all the Amazon S3 buckets within my AWS account using the AWS CLI, which helps verify whether our EC2 instance can communicate with the S3 service.

The terminal responded with a list of my AWS account's buckets, specifically showing the CloudFormation templates bucket and nextwork-vpc-project-marc. This indicated that the access keys I set up were correctly configured, successfully authenticating my EC2 instance so it can programmatically access and view resources in Amazon S3.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-endpoints_4334d778)

---

## Connecting to my S3 bucket

I also tested the command aws s3 ls s3://nextwork-vpc-project-marc, which returned a list of the specific objects inside the bucket, displaying mech1.jpg and mech2.jpg along with their sizes and upload timestamps. This output confirmed that my EC2 instance has the necessary programmatic permissions to inspect the contents of my S3 bucket.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-endpoints_4334d779)

---

## Uploading objects to S3

To upload a new file to my bucket, I first ran the command sudo touch /tmp/nextwork.txt. This command creates an empty, zero-byte text file named nextwork.txt inside the temporary /tmp directory using administrative privileges, giving us a local file that is ready to be copied to Amazon S3.

The second command I ran was aws s3 cp /tmp/nextwork.txt s3://nextwork-vpc-project-marc. This command will copy the local nextwork.txt file created on my EC2 instance and upload it directly to my Amazon S3 bucket named nextwork-vpc-project-marc.

The third command I ran was aws s3 ls s3://nextwork-vpc-project-marc, which validated that the nextwork.txt file was successfully uploaded to my S3 bucket. Seeing the file listed in the terminal with a size of 0 bytes confirmed that our EC2 instance has both write and read permissions to Amazon S3 through the public network path.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-endpoints_3e1e79a2)

---

## In the second part of my project...

### Step 5 - Set up a Gateway

In this step, I will create a VPC endpoint for Amazon S3 within my VPC because establishing this private gateway ensures our data traffic stays securely inside the AWS network rather than traveling across the public internet.

### Step 6 - Bucket policies

In this step, I am going to configure a strict bucket policy on my S3 bucket that denies all access to the bucket unless the request originates from my specific VPC endpoint. This allows me to safely verify our private connection by ensuring that the EC2 instance can still communicate with S3, while all other public internet traffic is completely blocked.

### Step 7 - Update route tables

In this step, I will test our VPC endpoint connectivity and troubleshoot any routing issues because I need to verify that my EC2 instance can still communicate privately with my Amazon S3 bucket even after restricting public access.

### Step 8 - Validate endpoint conection

In this step, I will test my S3 connectivity from the EC2 instance again to confirm the private route is working, and then restrict our VPC's access by editing the VPC endpoint policy because I need to verify how endpoint policies can instantly block S3 traffic at the network boundary.

---

## Setting up a Gateway

I set up an S3 Gateway, which is a specific type of VPC endpoint designed to establish private routing between my VPC and Amazon S3. It works by automatically adding an entry to my public subnet's route table that redirects S3-bound traffic directly to the gateway instead of sending it over the public internet.

### What are endpoints?

A VPC endpoint is a secure AWS service that enables private, direct connections between a VPC and other AWS services like Amazon S3 without routing traffic over the public internet, ensuring that sensitive data remains entirely within the AWS network.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-endpoints_09bcaa8a)

---

## Bucket policies

A bucket policy is a resource-based IAM policy written in JSON that is attached directly to an Amazon S3 bucket. It is used to manage access permissions by specifying exactly which principals are allowed or denied access to the bucket and the objects stored within it.

My bucket policy will explicitly deny all programmatic actions and requests to my S3 bucket and its objects from any source, unless the traffic is routed directly through my designated VPC endpoint. This creates a highly secure, private communication channel that blocks all public internet access while preserving seamless connectivity for my authorized EC2 instance.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-endpoints_7316a13d)

---

## Bucket policies

Right after saving my bucket policy, my S3 bucket page showed 'denied access' warnings. This was because my newly applied S3 bucket policy explicitly denies all actions on the bucket from any source other than our specific VPC endpoint. Since I was viewing the bucket from the AWS Management Console over the public internet rather than through the private endpoint, my console session was correctly blocked and denied access.

I also had to update my route table because, without an explicit route directing S3-bound traffic to our newly created gateway VPC endpoint, requests from my EC2 instance would continue attempting to access Amazon S3 via the public internet gateway instead of keeping the traffic private and secure.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-endpoints_4ec7821f)

---

## Route table updates

To update my route table, I went to the VPC console, selected my S3 VPC endpoint, and clicked Manage route tables to associate it with my public subnet's route table. This action automatically appended a route directing all Amazon S3 traffic through our private gateway rather than over the public internet.

After updating my public subnet's route table, my terminal could return the list of objects in my bucket, successfully showing files like mech1.jpg and nextwork.txt along with their sizes and timestamps. This successful response indicates that the route table is now directing Amazon S3 requests through our private VPC endpoint rather than the public internet, satisfying the bucket policy and restoring our access.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-endpoints_d116818e)

---

## Endpoint policies

An endpoint policy is an IAM resource-based policy attached directly to a VPC endpoint that controls which AWS principals can access which resources through that specific gateway or interface. It allows you to define granular network boundaries, such as blocking all traffic during an attack or restricting access to specific S3 buckets, completely independent of individual user or resource permissions.

I updated my endpoint's policy by editing the JSON document to change the Effect statement from Allow to Deny. I could see the effect of this right away, because running the S3 list command from my EC2 instance immediately returned an access denied error, proving that the updated VPC endpoint policy was applied instantly and successfully blocked our private path to Amazon S3.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-endpoints_3e1e79a3)

---

---
