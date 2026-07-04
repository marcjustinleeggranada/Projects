<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Website Delivery with CloudFront

**Project Link:** [View Project](http://nextwork.ai/projects/aws-networks-cloudfront)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## Website Delivery with CloudFront

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-cloudfront_1dddddwe)

---

## Introducing Today's Project!

In this project, I will demonstrate how to deliver a website using Amazon CloudFront, a content delivery network (CDN) service. I'll create an Amazon S3 bucket to store my website files, set up a CloudFront distribution to deliver the content globally, manage permissions for both S3 and CloudFront, and compare different methods for hosting my website. I'm doing this project to learn how CDNs work, why fast content delivery matters for users, and how CloudFront fits into the presentation tier of a three-tier architecture.

### Tools and concepts

Services I used were Amazon S3 and Amazon CloudFront. Key concepts I learnt include content delivery network (CDN), which is a network of servers around the world that caches and delivers content to users from the nearest location. I also learnt about Origin Access Control (OAC), which lets CloudFront securely access private S3 objects without making them public. Other key concepts include bucket policies, Block Public Access settings, S3 static website hosting, and the presentation tier of a three-tier architecture.

### Project reflection

This project took me approximately 60 minutes to complete. The most challenging part was troubleshooting the access denied errors — first with CloudFront not being able to access my private S3 objects, and then with S3 static website hosting being blocked by the Block Public Access settings. It was most rewarding to finally see my website load through CloudFront and understand how Origin Access Control (OAC) keeps everything secure while still delivering content globally.

I chose to do this project today because I wanted to understand how content delivery networks work and how CloudFront fits into the presentation tier of a three-tier architecture. Something that would make learning with NextWork even better is more visual comparisons between different AWS services, like side-by-side diagrams showing how S3 static website hosting and CloudFront deliver content differently.

---

## Set Up S3 and Website Files

I started the project by creating an S3 bucket to store my website's files, including the HTML, CSS, and JavaScript that make up my site. I can't use CloudFront for this task because CloudFront is a content delivery network (CDN), not a storage solution. It needs an origin to pull content from, and that's where S3 comes in as the storage backend.

The three files that make up my website are index.html, which is the main file that organises the text, pictures, and everything that makes up my webpage. style.css, which controls the visual appearance of the website's HTML elements like font sizes, colors, and layout designs. And script.js, which adds interaction to the website, like making things move or change when you click a button or submit a form.

I validated that my website files work by right-clicking on the index.html file, selecting Open With, and opening it in my browser. A simple web page loaded successfully, which confirmed that all three files — index.html, style.css, and script.js — were working correctly together.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-cloudfront_qgo7wcd3)

---

## Exploring Amazon CloudFront

Amazon CloudFront is a content delivery network, which means it speeds up the distribution of static and dynamic web content like .html, .css, .js, and image files. It does this by caching your website's content at edge locations around the world. When a user requests your content, the request is routed to the nearest edge location with the lowest latency, so the content loads as fast as possible. Businesses and developers use CloudFront because it ensures their users get a fast, reliable experience no matter where they are in the world — without slow load times caused by distance from the origin server.

To use Amazon CloudFront, you set up distributions, which are a set of instructions that tell CloudFront how to deliver your content. A distribution specifies where your website's files are stored (the origin), how they should be cached, and other delivery settings like security standards. I set up a distribution for my S3 bucket, which stores my website's HTML, CSS, and JavaScript files. The origin is my S3 bucket, which is where CloudFront will pull the website content from to distribute it to users around the world.

My CloudFront distribution's default root object is index.html. This means that when a user visits the root URL of my CloudFront distribution (e.g. d1234abcd.cloudfront.net), CloudFront will automatically serve the index.html file from my S3 bucket without the user needing to specify the file name in the URL.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-cloudfront_qgo7wcdt)

---

## Handling Access Issues

When I tried visiting my distributed website, I ran into an access denied error because my S3 bucket is private by default. CloudFront hasn't been given explicit permission to access the files in my bucket yet, so when it tried to pull the website content from S3, the request was denied.

My distribution's origin access settings were set to Public. This caused the access denied error because setting origin access to public doesn't automatically update the permissions of the objects in my S3 bucket — the objects are still private by default. So even though the origin access was public, CloudFront couldn't access my website's content because the individual objects in the bucket weren't set to public either.

To resolve the error, I set up origin access control (OAC). OAC is a special CloudFront feature that lets you keep your S3 bucket and objects private, while still allowing CloudFront to access and deliver them. Instead of making my S3 content publicly accessible, OAC gives CloudFront a secure, authenticated way to read my bucket's files — keeping everything locked down from direct public access.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-cloudfront_egrhntyu)

---

## Updating S3 Permissions

Once I set up my OAC, I still needed to update my bucket policy because creating an OAC alone doesn't automatically give CloudFront access to my S3 bucket's objects. My S3 bucket keeps all objects private by default — even from the OAC. I needed to add a bucket policy that explicitly grants the OAC permission to read the bucket's contents, so CloudFront can actually access and deliver my website files.

Creating an OAC automatically gives me a policy I could copy, which grants my CloudFront distribution permission to read objects from my S3 bucket. This policy tells S3 to allow requests that come from my specific CloudFront distribution, so CloudFront can securely access and deliver my website files without making the bucket publicly accessible.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-cloudfront_eg98ntyu)

---

## S3 vs CloudFront for Hosting

For my project extension, I'm comparing S3 static website hosting with CloudFront as two different methods of delivering my website. I initially had an error with static website hosting because my S3 bucket's objects are private by default — when I enabled static website hosting, the website URL returned an access denied error since static website hosting requires the objects to be publicly accessible. This is different from CloudFront, which uses Origin Access Control (OAC) to securely access private S3 objects without making them public.

I tried resolving this by updating my S3 bucket policy to allow public access to my website files. I still ran into an error because my S3 bucket has Block Public Access settings enabled by default, which override any bucket policy that tries to grant public access. So even though my bucket policy was set to allow public read access, the Block Public Access settings blocked it from taking effect.

I could finally see my S3 hosted website when I disabled the Block Public Access settings on my S3 bucket. This worked because the Block Public Access settings were overriding my bucket policy that granted public read access. Once I turned off Block Public Access, my bucket policy was able to take effect, allowing anyone to access the website files through the S3 static website hosting URL.

Compared to the permission settings for my CloudFront distribution, using S3 static website hosting meant I had to make my bucket and its objects publicly accessible to everyone. I had to disable Block Public Access settings and add a bucket policy granting public read access. With CloudFront, my S3 bucket stayed private and I only needed to set up an Origin Access Control (OAC) to give CloudFront secure, authenticated access. I preferred CloudFront because it keeps my content private and secure — only CloudFront can access the S3 bucket, rather than exposing it to the entire internet.

---

## S3 vs CloudFront Load Times

Load time means the amount of time it takes for a webpage to fully load and display in your browser after you request it. The load times for the CloudFront site were faster than the S3 site because CloudFront caches my website's content at edge locations around the world. When a user requests my website, CloudFront serves it from the nearest edge location, reducing the distance the data has to travel. With S3 static website hosting, the content is only served from the single region where my bucket is located, so users further away from that region experience slower load times.

Compared to the permission settings for my CloudFront distribution, using S3 static website hosting meant I had to make my bucket and its objects publicly accessible to everyone. I had to disable Block Public Access settings and add a bucket policy granting public read access. With CloudFront, my S3 bucket stayed private and I only needed to set up an Origin Access Control (OAC) to give CloudFront secure, authenticated access. I preferred CloudFront because it keeps my content private and secure — only CloudFront can access the S3 bucket, rather than exposing it to the entire internet.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-cloudfront_12verpuh)

---

---
