<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build Instant Failover with CloudFront Origin Groups

**Project Link:** [View Project](http://nextwork.ai/projects/ai-disaster-recovery-failover)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-disaster-recovery-failover_n4p8r2t6)

---

## Introducing Today's Project!

In this step, I'm going to create a CloudFront origin group by gathering my two App Runner origins (us-east-1 and us-west-2) into a single failover group. CloudFront is important because it handles failover at the edge level, automatically rerouting traffic to the healthy secondary origin in seconds without any DNS propagation delays.

### Key services and concepts

The key tools I used include CloudFront for edge-level content delivery and failover routing, App Runner for hosting multi-region services, CloudWatch for monitoring the 4xxErrorRate metric, and SNS for sending email alerts. Key concepts I learnt include origin groups for bundling primary and secondary origins, failover criteria (especially why 404 is needed for paused App Runner services), automatic failback when the primary recovers, and production-grade observability using CloudWatch alarms paired with SNS notifications.

### Challenges and wins

This project took me approximately 2 days, spread across setting up CloudFront, testing failover/failback, and configuring CloudWatch alerting. The most challenging part was getting the CloudWatch alarm to actually fire — I had to troubleshoot the SNS action being set to "OK" instead of "In alarm", and learn that the origin group was masking errors from viewers so I needed to pause both services. It was most rewarding to see the full pipeline come together — from CloudFront automatically switching to us-west-2 within seconds, to receiving that SNS email confirming the alarm fired.

---

## Setting Up Multi-Region Prerequisites

This project requires completing the Deploy Multi-Region project first. I have App Runner services running in us-east-1 (primary) and us-west-2 (secondary), both responding with their region name. These services are needed because CloudFront origin groups require two origins to enable automatic failover between regions.

---

## Creating a CloudFront Distribution

I created a CloudFront distribution with my us-east-1 App Runner service as the primary origin. The origin is my App Runner default domain (e.g. fu3zrm5itf.us-east-1.awsapprunner.com/), configured with HTTPS only since App Runner only accepts HTTPS connections. My CloudFront URL is dnl8qyld5hvcd.cloudfront.net

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-disaster-recovery-failover_n4p8r2t6)

---

## Configuring Origin Groups for Failover

In this step, I'm going to add a secondary origin (us-west-2) and create an origin group that bundles both origins together for automatic failover. Origin groups enable failover by letting CloudFront detect error responses (like 404 or 5xx) from the primary origin and immediately rerouting the request to the secondary origin at the edge level, making failover nearly instantaneous.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-disaster-recovery-failover_e7f3g9h1)

### Failover criteria configuration

I created an origin group with my primary origin (us-east-1) and secondary origin (us-west-2) bundled together as a failover pair. The failover criteria include 404, 500, 502, 503, and 504 because these cover both standard server errors and the 404 that App Runner returns when a service is paused — without 404, CloudFront would keep trying the paused primary and never fail over.

### Testing the CloudFront URL

I tested my CloudFront URL and saw "Round-trip latency (ms):
us-west-2: 975.3, us-east-1: 1050.3" confirming it's routing to the primary origin. Round-trip latency was 975.3ms for us-west-2 and 1050.3ms for us-east-1. This confirms that CloudFront is routing to my primary origin group member (us-east-1) as expected, even though us-west-2 has slightly lower latency — because the origin group always tries the primary first.

---

## Testing Automatic Failover

In this step, I'm going to test failover by pausing the us-east-1 App Runner service to simulate a regional outage, then checking that CloudFront automatically switches to us-west-2. I'll verify failback by resuming the us-east-1 service and confirming CloudFront routes traffic back to the primary. This tests that CloudFront origin groups handle both automatic failover and failback without any manual intervention or DNS changes.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-disaster-recovery-failover_x3y7z1a5)

### Simulating primary origin failure

I paused the us-east-1 service and CloudFront automatically detected the failure within about 30 seconds. The response changed from "Round-trip latency (ms):
us-west-2: 975.3, us-east-1: 1050.3" to "Round-trip latency (ms): us-west-2: 739.1, us-east-1: ERROR (Failed to fetch)" — confirming that the origin group failover criteria caught the 404 from the paused service and rerouted traffic to the secondary origin instantly at the edge.

---

## Verifying Automatic Failback

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-disaster-recovery-failover_f6g1h5i9)

### Restoring the primary origin

I resumed the us-east-1 service and CloudFront automatically detected the recovery within about 30-60 seconds. The response returned to "Round-trip latency (ms): us-west-2: 777.3, us-east-1: 1024.6" — confirming that CloudFront's origin group prefers the primary origin once it starts returning healthy 200 OK responses again, completing the full failover/failback cycle with zero manual intervention.

---

## Building Production Alerting with CloudWatch

I'm going to build alerting with CloudWatch and SNS to get instant email notifications the moment CloudFront detects an origin failure and triggers failover. This is important because automatic failover alone doesn't tell you it happened — without alerting, you could have a regional outage and never know until a customer complains. Production-grade systems need observability so engineers can investigate the root cause while failover keeps users unaffected.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-disaster-recovery-failover_sm2j7n4r)

### Configuring CloudWatch alarms

I created a CloudWatch alarm on the 4xxErrorRate metric with a static threshold set to trigger when the error rate exceeds 5% over a 5-minute period. The SNS topic will notify me via email the moment CloudFront starts returning elevated 4xx errors — which is exactly what happens when the primary origin goes down and returns 404s. When the threshold exceeds 5%, the alarm transitions to "In alarm" state and SNS automatically sends an email so I can investigate the root cause while failover keeps users unaffected.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-disaster-recovery-failover_sm4g5l6w)

### Verifying alerting works

I tested the alarm by pausing both my us-east-1 and us-west-2 App Runner services so CloudFront had no healthy origin and returned 404s to viewers. After waiting about 5 minutes for the evaluation period, the alarm transitioned from OK to "In alarm" and I received an email from SNS showing the alarm name, reason ("Threshold Crossed: 4xxErrorRate exceeded 5%"), and the timestamp of the event. This confirms that my CloudWatch alarm and SNS notification pipeline is fully working — I now have production-grade observability that alerts me the moment a failover event occurs, so I can investigate root cause while CloudFront keeps users unaffected.

---

## Wrapping Up

I did this project today to learn how to build automatic failover at the edge level using CloudFront origin groups, so my applications can survive regional outages without any manual intervention or DNS propagation delays. Another disaster recovery skill I want to learn is multi-cloud disaster recovery with Pulumi, where I can build 3-way failover across AWS and GCP using Infrastructure as Code.

---

---
