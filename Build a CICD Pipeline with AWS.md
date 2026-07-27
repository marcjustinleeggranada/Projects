<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a CI/CD Pipeline with AWS

**Project Link:** [View Project](http://nextwork.ai/projects/aws-devops-codepipeline-updated)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codepipeline-updated_fbdetger)

---

## Introducing Today's Project!

In this project, I will demonstrate how to build a fully automated CI/CD pipeline using AWS CodePipeline to connect my GitHub repository with AWS CodeBuild and AWS CodeDeploy. I am doing this project to learn how to integrate individual DevOps tools into a seamless release workflow, automate application deployments to Amazon EC2, and master automated troubleshooting techniques like pipeline rollbacks.

### Key tools and concepts

Services I used were AWS CodePipeline, AWS CodeBuild, AWS CodeDeploy, and Amazon EC2. Key concepts I learnt include automating a CI/CD pipeline, configuring GitHub triggers, packaging build artifacts, and orchestrating deployments.

### Project reflection

This project took me approximately 3 hours to complete. The most challenging part was troubleshooting the CodeDeploy agent installation and resolving the target Amazon EC2 instance mismatch on the web server. It was most rewarding to finally see the agent logs successfully polling with a 200 status code and watching our automated CI/CD pipeline execute the entire build and deployment smoothly.

---

## Starting a CI/CD Pipeline

AWS CodePipeline is a fully managed continuous delivery service that automates release pipelines for fast and reliable application and infrastructure updates. It acts as the central orchestrator of the CI/CD pipeline, automatically pulling new code changes from GitHub whenever they are pushed, triggering AWS CodeBuild to compile and test the application, and finally instructing AWS CodeDeploy to deploy the built artifacts onto Amazon EC2 instances. This automation eliminates manual handoffs, reduces human errors, and ensures a consistent and rapid delivery cycle.

AWS CodePipeline offers different execution modes based on how we want to handle concurrent pipeline runs. I chose Superseded mode because it ensures that if a new code commit is pushed while a run is active, the older run is cancelled so that only the latest update is built and deployed, making it the most efficient choice for our CI/CD pipeline. Other options include Queued mode, which handles runs one after another in order, and Parallel mode, which allows multiple runs to execute concurrently and independently.

A service role gets created automatically during setup so that AWS CodePipeline has the secure, delegated permissions required to interact with other AWS services on our behalf. This newly created IAM role grants our pipeline the explicit authorization to retrieve source files from Amazon S3, kick off compilation tasks in AWS CodeBuild, and hand off the built artifacts directly to AWS CodeDeploy to execute the release seamlessly.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codepipeline-updated_gdnhtm)

---

## CI/CD Stages

The three stages I've set up in my CI/CD pipeline are the Source stage, the Build stage, and the Deploy stage. While setting up each part, I learnt about how AWS CodePipeline automatically retrieves fresh commits from GitHub, coordinates with AWS CodeBuild to package the source files, and directs AWS CodeDeploy to execute the deployment on our Amazon EC2 instances while keeping rollbacks enabled for safety.

AWS CodePipeline organizes the three stages into a clear, visual workflow diagram that displays the real-time execution status of our pipeline runs. In each stage, you can see more details on the exact commit ID and update details pulled from GitHub in the Source stage, the build progress and compile logs in the Build stage, and the target instance status and lifecycle events in the Deploy stage.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codepipeline-updated_fbdetger)

---

## Source Stage

In the Source stage, the default branch tells AWS CodePipeline which parallel version of our code in the GitHub repository it should actively monitor for updates. By specifying a branch like master, the pipeline knows exactly which environment to pull code from and target. Whenever a developer pushes a new commit or merges a pull request into this designated branch, the configured webhook automatically triggers a fresh run of our CI/CD pipeline to build and deploy only the most stable codebase.

The source stage is also where you enable webhook events, which act as real-time digital notifications that connect our GitHub repository directly to AWS CodePipeline. These events are critical in a CI/CD pipeline because they remove the need for manual polling, ensuring that the very second a developer pushes new code to the monitored branch, the pipeline automatically detects the change and triggers a fresh build and deployment run instantly.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codepipeline-updated_sergt)

---

## Build Stage

The Build stage sets up the automation step where our raw code is compiled and packaged into a deployable format. I configured this stage to use our existing AWS CodeBuild project, nextwork-devops-cicd. The input artifact for the build stage is SourceArtifact, which is the ZIP file containing our retrieved GitHub source code. It is the required input because CodeBuild needs access to these exact source files to run the compilation commands and package our application successfully.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codepipeline-updated_j1k2l3m4)

---

## Deploy Stage

The Deploy stage is where our compiled build artifacts are retrieved from AWS CodeBuild and published to our live environment. I configured this stage to use AWS CodeDeploy as our deployment provider, targeting our existing application and deployment group, and enabled automatic rollback so that our web application running on Amazon EC2 automatically reverts to the last stable release if a deployment fails.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codepipeline-updated_m4n5o6p7)

---

## Success!

Since my CI/CD pipeline gets triggered by webhook change detection, I tested my pipeline by adding a new line of text to my index.jsp file and pushing that fresh commit directly to the master branch of my GitHub repository to watch the automated deployment process execute.

The moment I pushed the code change to my GitHub repository, AWS CodePipeline instantly detected the update through webhook events and started a new execution. The commit message under each stage reflects the exact update we made to our web application, giving us complete visibility as our code moves automatically through the build phase in AWS CodeBuild and is deployed to our server by AWS CodeDeploy.

Once my pipeline executed successfully, I checked my web server's public IP address in a new browser tab to see if my updated homepage greeting loaded. By refreshing the page and seeing the newly added text, I successfully verified that AWS CodePipeline pushed the latest build artifact to my Amazon EC2 instance, confirming that our automated CI/CD pipeline is fully operational.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codepipeline-updated_e1f2g3h4)

---

## Testing the Pipeline

---

---
