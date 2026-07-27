<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Connect a Web App with Aurora

**Project Link:** [View Project](http://nextwork.ai/projects/aws-databases-webapp)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## Connect a Web App to Amazon Aurora

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-webapp_1709b26b)

---

## Introducing Today's Project!

### What is Amazon Aurora?

Amazon Aurora is a fully managed relational database service built for the cloud that is highly compatible with MySQL and PostgreSQL. It is incredibly useful because it automates complex database management tasks such as provisioning, patching, and backups, while delivering up to five times the performance of standard databases to ensure that dynamic web applications can retrieve and store user data quickly and securely.

### How I used Amazon Aurora in this project

In today's project, I used Amazon Aurora to act as the secure, relational database backend for an interactive PHP web application hosted on an Amazon EC2 instance. By connecting the web server to the Aurora writer endpoint, I enabled the application to dynamically capture and store user inputs, which I then verified in real time by querying the database cluster directly through the MySQL CLI.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how seamless and automated the network integration is between Amazon EC2 and Amazon Aurora. I anticipated having to spend a significant amount of time manually configuring security group rules to enable traffic between our web server and database cluster, so having AWS handle that background configuration automatically was a fantastic surprise that made setting up our application pipeline much smoother.

### This project took me...

This project took me approximately 1 hour to complete. Setting up the Amazon EC2 instance and hosting the interactive PHP web application was very straightforward, while locating the Amazon Aurora database cluster's writer endpoint took a bit of careful navigation in the console. Overall, it was incredibly rewarding to watch the frontend form dynamically send and save data to the backend database in real time!

---

## Creating a Web App

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-webapp_b7999168)

To connect to my Amazon EC2 instance, I use an SSH client like Git Bash on my Windows machine. First, I navigate to the folder where my private key, NextWorkAuroraApp.pem, is saved. After securing the file, I run the SSH command using the key file and the instance's Public IPv4 DNS address to establish a secure remote connection to my virtual server.

To help me create my web app, I first update the package list on my Amazon EC2 instance and install the Apache web server, PHP, and the database connector module. Then, I verify that my web server is active and running so that it is ready to host and serve the application code from the /var/www/html directory and connect with my Amazon Aurora database cluster.

---

## Connecting my Web App to Aurora

I set up my Amazon EC2 instance's connection details to my database by creating a new configuration directory named inc and defining a new settings file called dbinfo.inc using the nano editor. Inside this file, I defined the server parameters with my Amazon Aurora database cluster's writer endpoint, the master database username, the password, and the initial database name, which allows the PHP script to successfully authenticate and route dynamic queries to our backend database.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-webapp_1709b25b)

---

## My Web App Upgrade

Next, I upgraded my web app by writing an interactive PHP script that features a clean HTML form for user inputs and a dynamic table to display stored records. This interface connects directly to our Amazon Aurora database, allowing users to submit new entries through their web browsers and immediately see the updated database records rendered on the page.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-webapp_2709b25b)

---

## Testing my Web App

To make sure my web app was working correctly, I entered a test name and contact details into the web app form in my browser, and then logged into my Amazon Aurora database cluster via the MySQL CLI on my Amazon EC2 instance. Once connected, I ran a SELECT * FROM employees; query on the database table and successfully verified that the exact record I had just submitted through the frontend form was saved in the database.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-webapp_1409z22b)

---

---
