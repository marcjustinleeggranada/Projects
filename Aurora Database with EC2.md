<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Aurora Database with EC2

**Project Link:** [View Project](http://nextwork.ai/projects/aws-databases-aurora)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## Connect a Web App to Amazon Aurora

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-aurora_44443546)

---

## Introducing Today's Project!

### What is Amazon Aurora?

Amazon Aurora is a fully managed, high-performance relational database engine built for the cloud that is fully compatible with MySQL and PostgreSQL. It is incredibly useful because it automatedly manages complex tasks like provisioning, patching, and backups, while delivering up to five times the throughput of standard MySQL by using an auto-scaling storage system and multi-node database clusters for high availability.

### How I used Amazon Aurora in this project

In today's project, I used Amazon Aurora to deploy a highly available relational database cluster and configure its network pathways to securely communicate with an Amazon EC2 instance. By taking advantage of AWS's automated connectivity features, I established a secure link between our compute and database tiers, laying down a robust, scalable backend infrastructure designed to host and manage dynamic application data.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how seamlessly AWS automates the network integration between separate compute resources and our backend relational database. I expected to manually configure subnet groups and write complex rules for our security groups to bridge the two; instead, simply selecting our target EC2 instance inside the Amazon Aurora setup console allowed the platform to automatically provision the necessary security group rules behind the scenes, completely bypassing the typical manual troubleshooting required to get database traffic flowing securely.

### This project took me...

This project took me approximately 1 hour to complete. Most of the time was spent waiting for the Amazon Aurora database cluster to provision in the background, while launching the Amazon EC2 instance and setting up the automated integration between both resources went incredibly quickly.

---

## In the first part of my project...

### Creating an Aurora Cluster

In this step, I will create an Amazon Aurora relational database cluster from scratch. I am doing this to establish a highly scalable and resilient data tier for my cloud architecture, which will allow me to understand how database engines operate in AWS and practice configuring secure, production-ready cluster settings before connecting it to a compute resource.

Amazon Aurora is a good choice when you need a highly scalable, high-performance relational database that can handle large-scale enterprise workloads with maximum uptime. It is ideal for critical business applications requiring high availability, automatic scaling, and fast read replicas to distribute query traffic. Because it leverages a multi-node database cluster design, it is perfect for scenarios where you need automated failover protection and seamless recovery without manual intervention.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-aurora_44443546)

---

## Halfway through I stopped!

I stopped creating my Amazon Aurora database because I needed to launch my target Amazon EC2 compute resource first. Since the AWS Management Console encourages choosing a target host to automatically handle networking, pausing the database setup allowed me to deploy the web server first, ensuring I could seamlessly link the database cluster to my active EC2 instance during the connectivity phase.

### Features of my EC2 instance

I created a new key pair for my Amazon EC2 instance to ensure secure administrative access to the virtual machine. Because cloud-hosted servers do not use traditional passwords, this key pair acts as my digital login credentials, enabling me to establish an encrypted SSH connection to safely manage, configure, and update my web application using the downloaded private key file.

When I created my EC2 instance, I took particular note of the Public IPv4 DNS and the key pair name. The Public IPv4 DNS is critical because it acts as the public address of my virtual server on the internet, while the key pair acts as the unique cryptographic key required to secure my login. Both details are essential because knowing the location of my server is useless without the digital keys needed to establish a secure SSH connection and access its command line.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-aurora_91b9fd1g)

---

## Then I could finish setting up my database

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-aurora_1fddb0b5)

Aurora Database uses clusters because grouping multiple database instances together ensures continuous data availability and high resilience. By combining a single writer instance for modifying data with multiple read replicas for handling queries, the database cluster can distribute heavy workloads efficiently. Furthermore, if the primary instance encounters a failure, Amazon Aurora can trigger an automatic failover to promote one of the backups, keeping the application online without manual intervention.

---

---
