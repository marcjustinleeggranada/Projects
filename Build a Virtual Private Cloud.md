<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Virtual Private Cloud

**Project Link:** [View Project](http://nextwork.ai/projects/aws-networks-vpc)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## Build a Virtual Private Cloud (VPC)

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-vpc_2facf927)

---

## Introducing Today's Project!

In this project, I will demonstrate how to design and build a custom Amazon VPC from scratch, configuring key networking components like a public subnet and an internet gateway. I am doing this project to learn the foundational principles of cloud networking, understand how IP addressing and CIDR blocks function, and gain hands-on experience routing cloud-based infrastructure.

### What is Amazon VPC?

Amazon VPC is a logically isolated virtual network that you define within your AWS account, giving you complete control over your own virtual networking environment. It is useful because it allows you to securely launch and run your cloud resources under your own custom configuration—enabling you to organize resources with subnets, manage traffic flow with route tables, and isolate sensitive backend databases from public web servers using security groups.

In today's project, I used Amazon VPC to set up a secure, isolated virtual network from scratch in my AWS account. Within this custom VPC, I provisioned a public subnet and attached an internet gateway to enable external traffic flow, giving me hands-on experience establishing the baseline cloud networking infrastructure.

### Personal reflection

This project took me about 60 minutes to complete because I wanted to make sure I carefully configured each networking component within my custom Amazon VPC. I spent most of my time learning how to coordinate the public subnet with the newly attached internet gateway, ensuring that all IP address configurations and routing rules were set up correctly to establish secure cloud connectivity.

One thing I didn't expect in this project was how many manual configurations are required to make a custom VPC functional compared to the default VPC that AWS automatically provides. I was surprised to learn that simply creating a subnet does not automatically connect it to the internet; you must also explicitly create and attach an internet gateway, configure custom route tables, and enable auto-assign public IP settings to establish external connectivity.

---

## Virtual Private Clouds (VPCs)

### What I did in this step

In this step, I will access the VPC console in AWS and create a custom Virtual Private Cloud because establishing this isolated network provides the secure foundation required to host and manage my cloud resources.

### How VPCs work

VPCs are secure, isolated virtual networks that you can define within AWS to host your cloud resources. They act as private boundaries in the cloud, giving you complete control over networking configurations like IP address ranges, subnets, and route tables so that your servers and databases can communicate safely without being exposed to the public internet.

### Why there is a default VPC in AWS accounts

There was already a default VPC in my account ever since my AWS account was created. This is because AWS automatically provisions a default VPC in every AWS Region to make it easy for beginners to launch resources immediately. This default setup allows services like Amazon EC2 to function right away without requiring users to manually design and build custom network infrastructure, subnets, or routing tables first.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-vpc_2facf927)

### Defining IPv4 CIDR blocks

To set up my VPC, I had to define an IPv4 CIDR block, To set up my VPC, I had to define an IPv4 CIDR block, which is a range of private IP addresses allocated to my network. This block determines the overall scale of my VPC by using a slash notation (like /16) to specify how many leading bits are fixed, leaving the rest available to define unique host addresses across my subnets.which is...

---

## Subnets

### What I did in this step

In this step, I will create and launch a subnet inside my VPC because dividing my virtual network into smaller, isolated segments allows me to organize my AWS resources effectively. This setup is necessary to allocate distinct ranges of IP addresses and prepare specific routing rules for public and private traffic.

### Creating and configuring subnets

Subnets are distinct, smaller partitions of a Virtual Private Cloud that allow you to group your resources based on their security and access needs. There are already subnets existing in my account, one for every Availability Zone in my current AWS Region, because AWS automatically sets them up inside the default VPC to make launching new resources quick and easy.

### Public vs private subnets

The difference between public and private subnets is that public subnets are connected to the internet, while private subnets are isolated to protect secure resources. For a subnet to be considered public, it has to be associated with a route table that directs traffic to an Internet Gateway, allowing resources within that subnet to communicate with external networks.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-vpc_157c4219)

### Auto-assigning public IPv4 addresses

Once I created my subnet, I enabled the auto-assign public IPv4 address setting. This setting makes sure any EC2 instance launched in this subnet automatically receives a public IP address so that it can seamlessly communicate with the internet without requiring me to manually assign an IP address each time.

---

## Internet gateways

### What I did in this step

In this step, I will create an internet gateway and attach it to my custom VPC because establishing this connection bridges my private virtual network with the outside world, allowing resources in my public subnet to send and receive traffic from the public internet.

### Setting up internet gateways

Internet gateways are AWS components that connect your VPC to the public internet. They act as a bridge, allowing resources inside your public subnets to send and receive traffic to and from external networks, which is essential for making applications hosted on your cloud servers publicly accessible.

Attaching an internet gateway to a VPC means establishing a critical network bridge that allows two-way traffic between resources inside your virtual network and the public internet. If I missed this step, my VPC would remain entirely isolated from the outside world, meaning any EC2 instances in my public subnet would have no way to download updates, and external users would be unable to access any web applications hosted there.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-vpc_4ae90410)

---

## Using the AWS CLI

### What I'm doing in this extension

### Exploring CloudShell and CLI

### Debugging my setup

### Comparing CloudShell vs AWS Console

---

---
