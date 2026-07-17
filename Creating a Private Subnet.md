<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Creating a Private Subnet

**Project Link:** [View Project](http://nextwork.ai/projects/aws-networks-private)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## Creating a Private Subnet

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-private_afe1fdbd)

---

## Introducing Today's Project!

### What is Amazon VPC?

An Amazon VPC is a logically isolated virtual network dedicated to your AWS account that mimics a traditional network operating in a physical data center. It is useful because it provides complete control over your virtual networking environment, allowing you to secure and group your resources using custom subnets, configure route tables, assign specific IP address ranges, and establish robust security boundaries via security groups and network ACLs to safely isolate sensitive backend data from the public internet.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to design a secure multi-tier architecture by deploying a dedicated private subnet to isolate backend resources. By configuring a custom private route table to prevent direct routing to the internet gateway, and attaching a strict network ACL that denies all traffic by default, I successfully established a secure, isolated environment within my virtual network.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project is that custom network ACLs deny all inbound and outbound traffic by default, unlike the default network ACL which allows everything. This was an eye-opening realization about how AWS enforces a "secure-by-default" posture, showing me that we must be entirely intentional about explicitly defining allow rules for any traffic to pass into our private subnet.

### This project took me...

This project took me about 45 minutes to complete as I worked through setting up the virtual resources. Most of my time was spent configuring and verifying the private route table and the custom network ACL to ensure my private subnet was completely secure and isolated, which really helped solidify my understanding of "secure-by-default" cloud networking principles.

---

## Private vs Public Subnets

The difference between public and private subnets is that a public subnet is associated with a route table that has a direct path to an internet gateway, allowing resources inside to be assigned public IP addresses and communicate with the external internet. In contrast, a private subnet does not route traffic to an internet gateway, ensuring that sensitive backend resources remain isolated from direct public internet access within the Amazon VPC.

Having private subnets are useful because they allow us to isolate and protect sensitive backend resources—such as databases and application servers—from direct exposure to the public internet. By ensuring these subnets have no direct route to an internet gateway, we block unauthorized inbound traffic and external scans, creating a highly secure layer where backend systems can safely process data and only communicate with approved resources within the Amazon VPC.

My private and public subnets cannot have the same IPv4 CIDR block or overlapping IP address ranges. Within a single Amazon VPC, every subnet must be assigned a unique range of IP addresses so that network traffic can be routed to the correct destination without any conflicts or errors.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-private_afe1fdbd)

---

## A dedicated route table

By default, my private subnet is associated with the default network ACL of the VPC. This default network ACL automatically permits all inbound and outbound traffic, which means that even though the subnet does not have a route to the internet, its network-level traffic rules remain completely open and permissive until we explicitly create and associate a custom network ACL to restrict traffic.

I had to set up a new route table because the default route table for my VPC has a route that directs traffic to the internet gateway, which would make my subnet public if associated with it. Creating a dedicated private route table without any internet-bound routes allows me to explicitly isolate my private subnet and ensure that all its traffic remains strictly local and secure from external networks.

My private subnet's dedicated route table only has one route with a local target that allows bidirectional internal traffic within our VPC. This single rule permits all resources inside the private subnet to communicate with other subnets in the same network, while completely blocking any outbound or inbound traffic to the public internet because there is no route pointing to an internet gateway.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-private_b4b904b5)

---

## A new network ACL

By default, my private subnet is associated with the VPC's default network ACL. This default security filter automatically allows all inbound and outbound traffic, meaning our private subnet's network-level traffic remains completely unrestricted and open until we explicitly create and associate a custom network ACL to enforce tighter security rules.

I set up a dedicated network ACL for my private subnet because the default network ACL automatically allows all inbound and outbound traffic, which leaves our isolated resources vulnerable. If another part of my Amazon VPC, such as the public subnet, were to be compromised, an attacker could exploit those open rules to access sensitive backend databases. Creating a custom network ACL that denies all traffic by default adds an essential layer of defense-in-depth security at the subnet boundary.

My new network ACL has two simple rules - one inbound rule and one outbound rule, both marked with an asterisk (*), which deny all traffic by default. This ensures my private subnet starts with a baseline of absolute security, completely blocking any unauthorized traffic at the network boundary until we explicitly define custom allow rules.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-private_1ed2cb07)

---

---
