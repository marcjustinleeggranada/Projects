<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Infrastructure as Code with CloudFormation

**Project Link:** [View Project](http://nextwork.ai/projects/aws-devops-cloudformation-updated)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-cloudformation-updated_bd8b836b)

---

## Introducing Today's Project!

In this project, I will demonstrate how to transform my manually configured web application infrastructure into a repeatable, automated template using AWS CloudFormation. I am doing this project to learn the core principles of Infrastructure as Code, understand how resources depend on each other during deployment, and practice troubleshooting template errors to build consistent, professional-grade DevOps environments.

### Key tools and concepts

Services I used were AWS CloudFormation, Amazon S3, AWS CodeArtifact, and AWS CodeDeploy. Key concepts I learnt include defining and deploying resources via Infrastructure as Code, managing resource creation order using the DependsOn attribute, and resolving circular dependencies to establish a stable, automated pipeline.

### Project reflection

This project took me approximately 2 hours to complete. The most challenging part was diagnosing and resolving the circular dependency error between the IAM roles and policies within my template. It was most rewarding to successfully deploy the updated CloudFormation stack and watch my resources spin up automatically, proving that my infrastructure is fully automated as code.

This project is part six of a series of DevOps projects where I'm building a CI/CD pipeline! I'll be working on the next project, Build a CI/CD Pipeline with AWS, tomorrow to tie all of these independent services together. I am excited to use AWS CodePipeline to automatically detect my GitHub commits, trigger AWS CodeBuild, and orchestrate the final rollout with AWS CodeDeploy for a fully automated, professional-grade workflow.

---

## Generating a CloudFormation Template

The IaC Generator is an AWS CloudFormation tool that scans an AWS account to automatically discover active resources and generate their corresponding template code. It works in a three-step process where you first scan your entire account for existing resources, next select the discovered resources to bundle into a template, and finally import that template into CloudFormation to manage them all together in a single stack.

A CloudFormation template is a declaration file written in YAML or JSON that serves as a blueprint to define, deploy, and manage AWS infrastructure as code. The resources that I could add to my template include Amazon S3 buckets, IAM roles and policies, AWS CodeArtifact repositories, and AWS CodeDeploy applications, allowing me to automatically provision and version control the entire foundational architecture of my CI/CD pipeline in a single repeatable deployment.

The resources I couldn't add to my template using the IaC Generator were my AWS CodeBuild project and AWS CodeDeploy deployment group. This occurred because these particular resources require complex, custom configuration settings and advanced security permissions that the automated scanner is unable to evaluate, process, or define automatically.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-cloudformation-updated_0495b046)

---

## Template Testing

Before testing my template, I deleted all of my manually created CI/CD resources because CloudFormation will fail its stack deployment if resources with the exact same names already exist in my AWS account, and removing them first ensures a smooth, conflict-free test of my automation script.

I tested my template by deploying it as a new stack in the AWS CloudFormation console. The result of my first test was a failure that triggered an immediate stack rollback (ROLLBACK_IN_PROGRESS) because of dependency conflicts within the scanned template, specifically due to IAM roles and policy resources attempting to reference one another in a circular loop before they were actually created.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-cloudformation-updated_f56730fd)

---

## DependsOn

To resolve the error, I added the DependsOn attribute to my four IAM policies in the template, pointing them directly to my IAM role. The DependsOn attribute means that AWS CloudFormation is instructed to pause and ensure the specified role resource is fully created and active before it attempts to provision or attach the dependent policies, successfully resolving our resource creation order conflict.

The DependsOn line was added to four different parts of my template: the AWS CodeBuild service role policy, the AWS CodeDeploy service role policy, the Amazon EC2 instance profile policy, and the AWS CodeArtifact consumer policy. For the CodeArtifact policy, the DependsOn line was specifically configured to wait for the IAM role that grants CodeArtifact access to my EC2 instance, ensuring the role is fully provisioned before the policy attempts to attach to it.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-cloudformation-updated_f0df8018)

---

## Circular Dependencies

I gave my CloudFormation template another test! But this time, I ran into a circular dependency error that caused my stack deployment to fail. The AWS CloudFormation engine got stuck in an endless loop because my IAM role template definition referenced my custom policies, while those exact policies simultaneously depended on the role to be created first, preventing either resource from being successfully provisioned.

To fix this error, I opened my CloudFormation template in my code editor, located the definition for my IAM role, and deleted the five lines listed under the ManagedPolicyArns section. Removing these policy references broke the circular reference loop between the role and its policies, allowing CloudFormation to successfully determine the correct creation order and provision the stack without getting stuck.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-cloudformation-updated_e6fd85ed)

---

## Manual Additions

---

## Success!

I could verify all the deployed resources by visiting the Resources tab of my CloudFormation stack in the AWS Management Console, which displays a comprehensive list of every active resource provisioned by my template alongside convenient hyperlinks to jump directly to their respective service consoles.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-cloudformation-updated_bd8b836b)

---

---
