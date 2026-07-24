<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Deploy a Web App with CodeDeploy

**Project Link:** [View Project](http://nextwork.ai/projects/aws-devops-codedeploy-updated)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codedeploy-updated_val-27)

---

## Introducing Today's Project!

In this project, I will demonstrate how to automate the deployment of a Java web application to an Amazon EC2 instance using AWS CodeDeploy. I am doing this project to learn how to configure deployment groups, create appspec.yml files with lifecycle hooks, and implement automated rollbacks to secure a continuous deployment pipeline.

### Key tools and concepts

### Project reflection

---

## Deployment Environment

To set up for CodeDeploy, I launched an EC2 instance and a custom VPC because we need a dedicated, secure production environment to host our live web application. The VPC establishes the isolated network infrastructure and routing rules, while the EC2 instance serves as the target deployment host where the CodeDeploy Agent will receive instructions, copy our build artifacts, and run our installation scripts.

Instead of launching these resources manually, I used CloudFormation to define my infrastructure as code, which allowed me to provision my entire network and servers consistently in minutes. When I need to delete these resources, I can simply delete the CloudFormation stack from the AWS console, which automatically tears down resources like the EC2 instance, subnets, and security groups in the correct order to keep my account tidy and prevent unnecessary charges.

Other resources created in this template include a VPC, subnets, Route Tables, and an Internet Gateway. They're also in the template because defining these networking components alongside our virtual server allows us to provision a completely self-contained, secure, and reproducible environment that manages its own traffic routing and firewall permissions automatically.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codedeploy-updated_val-5)

---

## Deployment Scripts

Scripts are files containing lists of commands that the system runs automatically to eliminate manual execution errors. To set up CodeDeploy, I also wrote scripts to gracefully stop the active Tomcat server, install the required Java application dependencies on the target EC2 instance, and start the web server again once the new build artifact is securely in place.

The install_dependencies.sh script will run during the BeforeInstall lifecycle hook to automatically update system packages and install necessary software dependencies, like Java Corretto and the Tomcat web server, on our target EC2 instance. This ensures that the hosting environment is fully prepared and configured before CodeDeploy copies our web application's WAR file into the destination directory.

The start_server.sh script will use the systemctl tool to automatically start both the Apache web server and Tomcat application server during the ApplicationStart deployment phase. It also configures these services to automatically launch if the EC2 instance reboots, ensuring our live web application is continuously available to users.

The stop_server.sh script will run during the ApplicationStop deployment hook to safely shut down both the Apache and Tomcat services on our target EC2 instance. It uses the pgrep tool to verify whether these server processes are currently active, ensuring that we only attempt to stop running services and preventing false-alarm execution errors that could halt the CodeDeploy pipeline.

---

## appspec.yml

Then, I wrote an appspec.yml file to provide AWS CodeDeploy with a structured instruction manual on how to install and configure our application on the target server. The key sections in appspec.yml are files, which specifies the source WAR file and copies it to the destination directory on the EC2 instance, and hooks, which triggers our custom scripts during precise deployment lifecycle events like stopping the server, installing dependencies, and restarting the service.

I also updated buildspec.yml because we need to instruct AWS CodeBuild to package both our appspec.yml configuration file and our deployment scripts folder into the final build artifact. This ensures that when CodeDeploy retrieves our application from Amazon S3, it has all the instructions and lifecycle hooks necessary to install dependencies, run the server, and successfully complete the deployment process.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codedeploy-updated_val-12)

---

## Setting Up CodeDeploy

A CodeDeploy application serves as an overall organizational container or namespace that groups all deployment configurations, revisions, and settings for a specific software project. In contrast, a deployment group is a specific subset within that application that defines exactly where (such as target EC2 instances filtered by tags) and how (such as utilizing the CodeDeployDefault.AllAtOnce configuration) those software revisions are actually deployed to different environments like staging or production.

To set up a deployment group, you also need to create an IAM role to grant AWS CodeDeploy secure permissions to manage AWS resources on your behalf. This role allows the service to retrieve build artifacts from Amazon S3, interact with and target your tagged EC2 instances, and write deployment metrics to CloudWatch while adhering to the principle of least privilege.

Tags are helpful for organizing, tracking, and dynamically targeting cloud resources without relying on static IP addresses or resource IDs. I used the tag role: webserver to instruct CodeDeploy to automatically identify and deploy our application code to the correct EC2 instance managed by our deployment group.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codedeploy-updated_val-18)

---

## Deployment configurations

Another key setting is the deployment configuration, which affects the speed and safety of our rollout by determining how many servers are updated at the same time. I used CodeDeployDefault.AllAtOnce, so CodeDeploy will deploy the application to all target EC2 instances simultaneously. This is the fastest deployment method, but also the riskiest, as any error will immediately impact the entire environment at once.

In order to connect our hosting server with the continuous deployment pipeline, a CodeDeploy Agent is also set up on the target EC2 instance to poll AWS CodeDeploy for deployment instructions, pull our compiled zip archives from Amazon S3, and execute the lifecycle bash scripts outlined in our appspec.yml file.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codedeploy-updated_val-20)

---

## Success!

A CodeDeploy deployment is a single, specific execution of updating your application, representing a unique event with its own ID that tracks the progress of copying files and running lifecycle scripts. The difference between it and a deployment group is that the deployment group is a permanent configuration folder that defines the target environment (such as specific EC2 instances and deployment rules), whereas a deployment is the actual, one-time action of releasing a specific code revision to those target servers.

I had to configure a revision location, which means specifying the precise storage destination where CodeDeploy can fetch our application's deployment bundle and lifecycle scripts. My revision location was the S3 URI pointing to the compiled ZIP file within my nextwork-devops-cicd-artifact bucket.

To check that the deployment was a success, I visited the Public IPv4 DNS of my EC2 instance in a web browser using the http:// prefix. I saw our live Java web application home page load successfully, confirming that AWS CodeDeploy executed all script lifecycle hooks and successfully unpacked our WAR file artifact on the server.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codedeploy-updated_val-27)

---

## Disaster Recovery

---

---
