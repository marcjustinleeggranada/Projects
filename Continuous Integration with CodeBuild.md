<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Continuous Integration with CodeBuild

**Project Link:** [View Project](http://nextwork.ai/projects/aws-devops-codebuild-updated)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codebuild-updated_35588a47)

---

## Introducing Today's Project!

In this project, I will demonstrate how to automate software builds by setting up a continuous integration pipeline using AWS CodeBuild connected to my code repository. I am doing this project to learn how to use a buildspec.yml file to run automated tests and package applications, which helps eliminate manual errors and ensures reliable software delivery in a modern DevOps workflow.

### Key tools and concepts

Services I used were AWS CodeBuild, Amazon S3, AWS CodeConnections, and AWS IAM. Key concepts I learnt include setting up an automated continuous integration pipeline, writing step-by-step compilation instructions in a buildspec.yml file, and resolving permission errors by granting a service role secure access to pull our Java dependencies from AWS CodeArtifact using Maven.

### Project reflection

This project took me approximately two hours to complete. The most challenging part was navigating the regional queue limits in Singapore, which required making the strategic decision to migrate my resources to us-east-1 and troubleshoot the permissions required for the CodeBuild service role to pull from AWS CodeArtifact. It was most rewarding to finally see that green "Succeeded" status on AWS CodeBuild and find our compiled WAR file safely packaged and uploaded inside our Amazon S3 bucket.

This project is part four of a series of DevOps projects where I'm building a CI/CD pipeline! I'll be working on the next project, Deploy a Web App with CodeDeploy, where I will configure AWS CodeDeploy to pull my compiled WAR file from Amazon S3 and install it onto my Amazon EC2 web server because this establishes the continuous delivery portion of our workflow, turning our raw build packages into a live, running application automatically.

---

## Setting up a CodeBuild Project

CodeBuild is a continuous integration service, which means it automatically compiles source code, runs automated tests, and packages software artifacts whenever code is updated. Engineering teams use it because it scales automatically on demand, eliminating the need to set up, maintain, and pay for idle build servers, which streamlines the continuous integration workflow and accelerates product delivery.

My CodeBuild project's source configuration means specifying exactly where my application's source code is securely stored so the build runner knows where to pull the files, and I selected GitHub because it directly integrates our code repository with the automated pipeline, enabling CodeBuild to access our code and automatically detect the buildspec.yml file to run our build instructions.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codebuild-updated_fewgrhte)

---

## Connecting CodeBuild with GitHub

There are multiple credential types for GitHub, like Personal Access Tokens and OAuth Apps. I used the GitHub App because it is the most secure and simple option, allowing AWS CodeConnections to manage the link automatically without requiring me to manually create, store, or rotate sensitive access tokens.

The service that helped connect my AWS account with my GitHub repository is AWS CodeConnections. This service acts as a secure, managed bridge that handles the authentication handshake behind the scenes, allowing AWS CodeBuild to safely pull my application code without requiring me to manage or expose sensitive credentials.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codebuild-updated_a7c98e2d)

---

## CodeBuild Configurations

### Environment

My CodeBuild project's Environment configuration defines the operating system, programming runtimes, and compute resources used to run our builds. It includes settings like the on-demand provisioning model, which spins up temporary build servers only when needed to minimize costs, and configures an Amazon EC2 compute type running Amazon Linux with the Java Corretto 8 runtime environment to support our web application's compilation requirements.

### Artifacts

Build artifacts are the tangible outputs generated during a software build process. They're important because they represent the final, deployable application package that will actually run on our servers. My build process will create a WAR file to neatly bundle all our compiled Java web application files. To store them, I created a dedicated Amazon S3 bucket to serve as a highly scalable, secure, and easily accessible home for our finished release packages.

### Packaging

When setting up CodeBuild, I also chose to package artifacts in a Zip file because it compresses our compiled files into a smaller size for faster uploads to Amazon S3, reduces storage costs, and organizes all of our deployment resources into one tidy, easily accessible package.

### Monitoring

For monitoring, I enabled CloudWatch Logs, which is a managed monitoring service that collects, monitors, and stores log files from AWS resources. It provides a real-time stream of our AWS CodeBuild execution steps, making it easy to track build progress, view compilation output, and quickly troubleshoot any compilation errors directly from the AWS console.

---

## buildspec.yml

My first build failed because AWS CodeBuild could not locate a buildspec.yml file in the root of my GitHub repository, triggering a YAML_FILE_ERROR. A buildspec.yml file is needed because it acts as the step-by-step instruction manual for the build runner, defining the exact phases, commands, and environment settings required to compile our code and package our build artifacts automatically.

The first two phases in my buildspec.yml file are install and pre_build, which set up our Java Corretto runtime and securely authenticate our build runner with AWS CodeArtifact to fetch our cached dependencies. The third phase is build, where we run our Maven compilation and package commands to compile our application and run tests. The fourth phase is post_build, which handles the final packaging steps and confirms that our compiled WAR file has been generated and is ready to be securely uploaded to Amazon S3.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codebuild-updated_35588a47)

---

## Success!

My second build also failed, but with a different error that said the build phase failed because the container could not access our private packages. To fix this, I attached the required consumer permission policy to the CodeBuild service role in the IAM console, granting our build runner secure authorization to pull the Java web application dependencies from AWS CodeArtifact.

To resolve the second error, I navigated to the IAM console, located my CodeBuild service role, and attached the IAM policy named codeartifact-nextwork-consumer-policy to grant it the necessary read permissions. When I built my project again, I saw the build status update to Succeeded with a green checkmark, confirming that AWS CodeBuild was able to securely fetch our Java dependencies from AWS CodeArtifact and compile the application.

To verify the build, I checked my Amazon S3 bucket named nextwork-devops-cicd-marc. Seeing the nextwork-devops-cicd-marc.zip artifact tells me that our Java application was successfully compiled and packaged into a deployable WAR file, confirming that our automated continuous integration pipeline completed without errors and securely stored our final deliverables for the next deployment stage.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codebuild-updated_d9cc6191)

---

## Automating Testing

---

---
