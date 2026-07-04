<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Multi-Cloud Disaster Recovery with Pulumi

**Project Link:** [View Project](http://nextwork.ai/projects/ai-disaster-recovery-pulumi)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-disaster-recovery-pulumi_k5j9m2v7)

---

## Introducing Today's Project!

In this project, I'm going to use Pulumi to manage my AWS and GCP infrastructure as TypeScript code — importing existing resources like App Runner and CloudFront, and deploying new ones like GCP Cloud Run. Multi-cloud disaster recovery is important because if AWS itself goes down, a multi-region setup on AWS alone won't save you — you need a second cloud provider as a backup. Infrastructure as Code helps by making every deployment consistent, version-controlled, and reproducible, so environments don't drift apart over time.

### Key tools and concepts

In this step, I'm going to install Pulumi CLI and initialize a TypeScript project to manage my infrastructure as code. Importing infrastructure means "adopting" existing AWS resources like App Runner so Pulumi can manage them without recreating them. This is useful because I can bring my already-deployed services under code control with zero downtime.

### Challenges and wins

In this step, I'm going to deploy to GCP Cloud Run which is Google's serverless container platform, similar to AWS App Runner. Multi-cloud is important because if AWS itself goes down, my multi-region setup is useless — GCP acts as a completely independent backup. I'll import it into Pulumi so all my infrastructure across both clouds is managed from one TypeScript codebase.

---

## Initializing a Pulumi TypeScript Project

I created a Pulumi project by running pulumi new aws-typescript in a new directory. The stack name I chose was dev, which represents my development environment. Pulumi stores state in Pulumi Cloud, a secure backend that tracks what resources exist so it knows what to create, update, or skip on each deployment.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-disaster-recovery-pulumi_x4c7z1y9)

### Importing existing AWS infrastructure

I imported my App Runner services by running pulumi import with each service's ARN, which generated TypeScript code I pasted into index.ts. The pulumi preview command showed "no changes," meaning my code exactly matches what's deployed. This confirms that Pulumi has successfully adopted my existing resources without recreating them.

---

## Deploying to GCP Cloud Run

I deployed to Cloud Run by running gcloud run deploy with the --source flag, which built a container from my code automatically. The response shows "Hello from GCP Cloud Run!" at the /api/region endpoint, confirming the K_SERVICE env var detection works. This confirms my app is running on GCP as a second cloud provider alongside AWS.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-disaster-recovery-pulumi_q3r7t1u5)

### Managing multi-cloud infrastructure with Pulumi

I imported Cloud Run into Pulumi by running pulumi import with the Cloud Run service's resource path from GCP. Now my Pulumi code manages both AWS App Runner services, a CloudFront distribution, and a GCP Cloud Run service from one index.ts file. This is multi-cloud IaC because I control infrastructure across two cloud providers in a single TypeScript codebase.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-disaster-recovery-pulumi_a1b5c8e3)

---

## Configuring CloudFront Multi-Cloud Failover

In this step, I'm going to configure CloudFront to use GCP Cloud Run as the secondary origin instead of us-west-2, creating true multi-cloud failover. Failover works by CloudFront automatically routing requests to GCP when the primary AWS origin returns 5xx errors. This gives me disaster recovery because if all of AWS goes down, traffic seamlessly switches to GCP with no manual intervention.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-disaster-recovery-pulumi_g5h8j3k7)

### Setting up origin groups for automatic failover

I configured the origin group with two origins from different cloud providers. The primary origin is my us-east-1 App Runner service on AWS. The secondary origin is gcp-cloud-run, my Cloud Run service on GCP. Failover triggers when CloudFront receives 500, 502, 503, or 504 errors from the primary, automatically routing traffic to GCP.

---

## Testing Multi-Cloud Disaster Recovery

I tested failover by pausing my us-east-1 App Runner service in the AWS console. When AWS was paused, CloudFront automatically routed traffic to GCP Cloud Run — visiting /api/region showed "Hello from GCP Cloud Run!" instead of "Hello from us-east-1!". This proves my DR setup works because traffic switches to a completely different cloud provider with zero manual intervention.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-disaster-recovery-pulumi_r2s5t8u1)

---

## Building a CloudWatch Monitoring Dashboard

In this secret mission, I'm going to use Cursor to generate Pulumi code for a CloudWatch dashboard that monitors my multi-cloud DR system. The dashboard will show health metrics for all three origins — App Runner us-east-1, App Runner us-west-2, and GCP Cloud Run — in a single view. This helps with DR because I can see the health of my entire multi-cloud setup at a glance and detect issues before they trigger failover.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-disaster-recovery-pulumi_j8k2l5m9)

### Real-time observability for disaster recovery

I deployed the dashboard using pulumi up after generating the CloudWatch dashboard code with Cursor AI. It shows health metrics for all three origins — App Runner us-east-1, App Runner us-west-2, and GCP Cloud Run — in a single CloudWatch view. When I tested failover, the metrics showed the primary origin's error rate spike while GCP Cloud Run picked up the traffic seamlessly.

---

---
