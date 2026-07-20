<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Monitoring with Flow Logs

**Project Link:** [View Project](http://nextwork.ai/projects/aws-networks-monitoring)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## VPC Monitoring with Flow Logs

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-monitoring_3e1e79a1)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a service that lets you provision a private, isolated section of the AWS cloud where you can launch AWS resources in a virtual network you define. It is useful because it gives you complete control over your virtual networking environment, including selecting IP address ranges, creating subnets, and configuring route tables and network gateways to secure and isolate your cloud infrastructure.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to set up two isolated networks, bridge them privately with a VPC peering connection, and deploy VPC Flow Logs to capture and track active network traffic records between our EC2 instances.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how quickly a single ping test would generate hundreds of individual network records in our stream. It was fascinating to see how VPC Flow Logs captured the exact byte count and status of each packet, and how easily we could query and visualize that private traffic using CloudWatch Logs Insights.

### This project took me...

This project took me about 60 minutes to complete from start to finish. Most of my time was spent configuring the IAM policy and IAM role permissions, and waiting for the data from our ping tests to generate active logs in Amazon CloudWatch.

---

## In the first part of my project...

### Step 1 - Set up VPCs

In this step, I will use the VPC wizard to set up two separate VPCs because having two distinct networks will allow me to test VPC peering and generate traffic for our monitoring tools later in the project.

### Step 2 - Launch EC2 instances

In this step, I will connect to my first EC2 instance and try to ping the second EC2 instance because doing so generates network traffic that will let us test our VPC Flow Logs and check if VPC peering is active.

### Step 3 - Set up Logs

In this step, I will configure VPC Flow Logs on my VPC and send them to a new Amazon CloudWatch log group because this sets up the continuous tracking and secure storage required to analyze all our inbound and outbound network traffic.

### Step 4 - Set IAM permissions for Logs

In this step, I will create a custom IAM policy and IAM role to grant VPC Flow Logs permission to write and send logs to Amazon CloudWatch, and then finish setting up the flow log on my public subnet because these components require explicit authorization to securely record and transmit our network traffic history.

---

## Multi-VPC Architecture

I started my project by launching an EC2 instance in each of my newly created VPCs. These instances will act as our traffic generators, allowing us to send test packets across our VPC peering connection so we can capture and analyze those network logs in Amazon CloudWatch.

The CIDR blocks for VPC 1 and VPC 2 are 10.1.0.0/16 and 10.2.0.0/16. They have to be unique because overlapping IP addresses would cause routing conflicts and connectivity issues, making it impossible to route traffic properly once a VPC peering connection is established between them.

### I also launched EC2 instances in each subnet

My EC2 instances' security groups allow inbound ICMP traffic from 0.0.0.0/0. This is because we need to perform a ping test between our two instances in different VPCs, and allowing this traffic from any IP address ensures that the network packets can travel successfully to test our VPC peering connection.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-monitoring_e7fa8775)

---

## Logs

Logs are digital diaries that AWS services use to automatically record events, activities, and transactions. They serve as a continuous, historical record of what occurred within a system, allowing engineers to track performance, investigate errors, and monitor network traffic patterns over time.

Log groups are like virtual folders within Amazon CloudWatch that aggregate and organize related logs from a specific source. They allow you to manage retention settings, access policies, and search queries for a collective set of network monitoring data in one centralized, region-specific location.

### I also set up a flow log for VPC 1

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-monitoring_e8398869)

---

## IAM Policy and Roles

I created an IAM policy because, by default, VPC Flow Logs do not have the required permissions to write and store network traffic records in a log group. This policy explicitly grants the necessary actions—such as creating log streams and uploading log events—so my VPC can securely transmit its traffic logs to Amazon CloudWatch for monitoring.

I also created an IAM role because an IAM policy only defines permissions, but cannot be assigned directly to a resource. By creating this role and attaching our policy to it, we establish a secure identity that we can assign directly to VPC Flow Logs, giving the service explicit authorization to write our network traffic data to Amazon CloudWatch.

A custom trust policy is a specialized document attached to an IAM role that defines exactly which external entities or AWS services are allowed to assume that role. It acts like a secure VIP list, ensuring that only the specific principal we define—like VPC Flow Logs—can use the role to perform actions in our account, preventing unauthorized access from other resources.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-monitoring_4334d777)

---

## In the second part of my project...

### Step 5 - Ping testing and troubleshooting

In this step, I will connect to the first EC2 instance and run a ping test to the private IP of the second EC2 instance because generating network traffic between the two peered VPCs allows us to test if our connection works and check if VPC Flow Logs are successfully capturing the activity.

### Step 6 - Set up a peering connection

In this step, I will create a VPC peering connection between VPC 1 and VPC 2 and update their route tables because this establishes a secure, private communication link that allows instances in both VPCs to route traffic directly to each other.

### Step 7 - Analyze flow logs

In this step, I will use CloudWatch Logs Insights to analyze the VPC Flow Logs collected from our public subnet because querying these records helps us identify active network traffic patterns and verify that our VPC peering traffic is being properly recorded.

---

## Connectivity troubleshooting

My first ping test between my EC2 instances had no replies, which means there is currently no direct network route established between our separate VPCs using private IP addresses, indicating that we still need to configure a VPC peering connection and update our route tables to let them communicate.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-monitoring_99d4ba42)

I could receive ping replies if I ran the ping test using the other instance's public IP address, which means that the destination EC2 instance is active and its security group is successfully configured to allow inbound ICMP traffic from the public internet. However, this also shows that the traffic is currently traveling through the internet gateway rather than over a secure, private VPC peering connection.

---

## Connectivity troubleshooting

Looking at VPC 1's route table, I identified that the ping test with Instance 2's private address failed because there is no route configured to direct traffic destined for VPC 2's IP range to a VPC peering connection. Without this explicit routing instruction, VPC 1 has no way of knowing how to direct packets targeting VPC 2's private IP space, causing the communication to fail.

### To solve this, I set up a peering connection between my VPCs

I also updated both VPCs' route tables so that traffic destined for the peer network's CIDR block is directed to our newly created VPC peering connection, allowing private network packets to flow directly and securely between our EC2 instances without traveling over the public internet.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-monitoring_7316a13d)

---

## Connectivity troubleshooting

I received ping replies from Instance 2's private IP address! This means that our VPC peering connection is successfully established and active. It validates that the route tables for both VPCs are correctly configured to direct private traffic directly between our EC2 instances without routing packets over the public internet.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-monitoring_4ec7821f)

---

## Analyzing flow logs

Flow logs tell us about the IP traffic flowing to and from the network interfaces in our VPC. They provide details such as source and destination IP addresses, the number of packets and bytes transferred, the protocols used, and whether the connection was accepted or rejected by security groups and network ACLs.

For example, the flow log I've captured tells us which pairs of IP addresses generated the largest volume of data transfers, specifically highlighting the private traffic flowing between our two EC2 instances. This allows us to verify that our VPC peering connection is actively routing communication and lets us see exactly how many bytes were sent during our ping tests.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-monitoring_d116818e)

---

## Logs Insights

Logs Insights is a powerful feature within Amazon CloudWatch that allows you to search, analyze, and visualize your log data using custom queries. It helps you quickly filter through large volumes of VPC Flow Logs to troubleshoot network connectivity issues, monitor traffic patterns, and gain deep operational insights in real time.

I ran the "Top 10 byte transfers by source and destination IP addresses" query in CloudWatch Logs Insights. This query analyzes our captured VPC Flow Logs by grouping traffic records by their source and destination IP addresses, calculating the total bytes transferred, and sorting the results to show the top ten busiest network connections in our VPC.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-monitoring_3e1e79a1)

---

---
