<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build Multi-Region Apps on AWS

**Project Link:** [View Project](http://nextwork.ai/projects/ai-disaster-recovery-multiregion)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-disaster-recovery-multiregion_s1d6r9t4)

---

## Introducing Today's Project!

In this project, I'm going to build multi region apps in AWS. The tools I will use include the AWS app runner in order to deploy my app in two regions: us-east-1 and us-west-2. Multi-region architecture matters because it allows your apps to recover from crashes by rerouting traffic to a different region as soon as the first one gets traffic issues

### Key services and concepts

The key tools I used include AWS App Runner for deploying my Node.js app without managing servers, GitHub for storing my code and enabling automatic deployments, and Cursor as my code editor. Key concepts I learnt include multi-region architecture for higher availability and lower latency, why AWS resources are region-specific and each region needs its own GitHub connection, and how environment variables like AWS_REGION let my app detect which region it's running in.

### Challenges and wins

This project took me approximately 2 hours. The most challenging part was setting up the GitHub connections — I ran into errors with existing connection names and browser popup issues during authentication. It was most rewarding to see both regions responding with their own region names, like 'Hello from us-east-1!' and 'Hello from us-west-2!', proving that multi-region deployment actually works.

### Project Reflection

I did this project today to learn how to deploy an app across multiple AWS regions for higher availability and lower latency. This project met my goals — I now understand why AWS resources are region-specific and how to set up automatic deployments from GitHub to App Runner. Another skill I want to learn is building instant failover using CloudFront origin groups, which is the next project in this series — so that traffic automatically routes to a healthy region when one goes down.

---

## Creating a Node.js Express App

In this step, I'm going to create a GitHub account and deploy it to the AWS App Runner in us-east-1. This sets up auto deployments so that every code push goes live in minutes.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-disaster-recovery-multiregion_s1b8m3p9)

### Pushing code to GitHub

I pushed my code by running git push. GitHub stores my code so that it can act as a cloud storage for my code

---

## Deploying to AWS App Runner (us-east-1)

I verified my deployment by checking the service status showed Running, then opening the Default domain URL in my browser to confirm it displayed 'Hello from AWS!' App Runner automatically provides HTTPS with a TLS/SSL certificate, a public URL, load balancing, and auto-scaling.

---

## Expanding to a Second Region (us-west-2)

In this step, I'm going to deploy my app to us-west-2 (Oregon), setting up a second App Runner service so the same app runs in two regions. Each region needs its own GitHub connection because AWS resources are region-specific — us-west-2 can't see or access resources created in us-east-1. This means I need to create a new connection called github-connection-west to link my GitHub repo to App Runner in this region.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-disaster-recovery-multiregion_s2c5n2r8)

### Creating a region-specific GitHub connection

I created a new GitHub connection named github-connection-west because AWS resources are region-specific — each region operates independently and can't access resources from another region. The github-connection-east connection I created in us-east-1 doesn't exist in us-west-2, so I needed to create a separate connection to link my GitHub repo to App Runner in this new region.

### Benefits of multi-region architecture

I verified both regions by opening the Default domain URL for each App Runner service — us-east-1 and us-west-2 — and confirming both displayed 'Hello from AWS!' Multi-region provides higher availability, so if one region goes down, the other can still serve users, and lower latency, since users connect to the region closest to them for faster response times.

---

## Adding Region-Aware Responses

In this step, I'm going to update my app to read the AWS_REGION environment variable so that I can tell which region is serving each request. Instead of both regions showing the same 'Hello from AWS!' message, each region will display its own name — like 'Hello from us-east-1!' and 'Hello from us-west-2!' — making it easy to verify which App Runner service is responding.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-disaster-recovery-multiregion_s3c7n1p4)

### Using environment variables for region detection

I used Cursor to update my index.js file so it reads the AWS_REGION environment variable and displays 'Hello from {region}!' instead of the generic 'Hello from AWS!' message. The AWS_REGION variable is set by App Runner automatically — no manual configuration or .env file needed, it just knows which region the service is running in. Automatic deployment means that when I push my code to GitHub, both App Runner services detect the new commit and independently pull, build, and deploy the updated code — so both regions stay in sync without any manual intervention.

### Why region visibility matters

I verified region detection by opening the Default domain URL for each App Runner service and confirming that us-east-1 displayed 'Hello from us-east-1!' and us-west-2 displayed 'Hello from us-west-2!' — each region showing its own unique response. This matters for failover because when I set up automatic failover with CloudFront in the next project, I need to be able to tell which region is actually serving the traffic. If one region goes down and traffic reroutes, seeing the region name instantly confirms the failover worked correctly.

---

## Measuring Real-World Latency

In this secret mission, I'm going to measure real-world latency by adding response timing to my app, so I can see the actual performance difference between us-east-1 and us-west-2. Latency matters because it directly impacts user experience — regions closer to users deliver faster loading times. Amazon found that every 100ms of latency costs 1% in sales, so choosing the right region to route users to can have a real business impact.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-disaster-recovery-multiregion_sm4r8t2w)

### Building a latency test page

I added timing by updating my index.js to record timestamps at the start and end of each request. The code measures server-side response time using Node.js's Date.now() — it captures the time when a request arrives, processes the response, then calculates the difference in milliseconds to show how long the server took to respond. This lets me compare real-world latency between us-east-1 and us-west-2.

### Latency results and insights

The latency to us-east-1 was 1.18 seconds and us-west-2 was 223ms. The closer region had lower latency because us-west-2 (Oregon) is geographically closer to the Philippines than us-east-1 (Virginia) — data packets have a shorter physical distance to travel across the Pacific, resulting in a significantly faster response time. This shows exactly why multi-region matters: by routing users to their nearest region, I can cut response times by over 80%.

---

---
