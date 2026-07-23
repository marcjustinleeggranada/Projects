<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Connect a GitHub Repo with AWS

**Project Link:** [View Project](http://nextwork.ai/projects/aws-devops-github)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## Connect a GitHub Repo with AWS

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-github_dd9d254e)

---

## Introducing Today's Project!

In this project, I will demonstrate how to securely store and manage a Java web application's source code by connecting a local development environment on an Amazon EC2 instance to a remote repository on GitHub. I'm doing this project to learn the fundamentals of Git version control, repository initialization, and secure authentication, establishing a strong foundation for building automated CI/CD pipelines in DevOps.

### Key tools and concepts

The services I used in this project were Amazon EC2, GitHub, and VS Code for secure remote development. Key concepts I learnt include local version control with Git, staging files using the staging area, saving version snapshots via commits, linking local environments to a remote cloud origin, and authenticating secure pushes using a personal access token instead of a traditional password.

### Project reflection

This project took me approximately 1.5 hours to complete. The most challenging part was troubleshooting the Git authentication process and configuring my personal access token with the correct scopes after encountering a 403 permission error in the terminal. It was most rewarding to execute a final push and see my local commits from the Amazon EC2 instance instantly sync and update my remote repository on GitHub.

I did this project because I want to master the fundamentals of DevOps engineering, and securing my web application's codebase in a cloud-based repository is the next critical step after setting up my environment on Amazon EC2. By connecting my remote server workspace to GitHub using Git, I am transitioning to modern version control and establishing the vital foundation needed to build automated CI/CD pipelines.

This project is part two of a series of DevOps projects where I'm building a CI/CD pipeline! I'll be working on the next project, Store Dependencies in CodeArtifact, tomorrow to learn how to securely manage software dependencies with AWS CodeArtifact.

---

## Git and GitHub

Git is a distributed version control system that tracks changes in source code and helps developers collaborate on software projects. I installed Git on my Amazon EC2 instance by running the package manager commands sudo yum update -y to refresh the system package database, followed by sudo yum install git -y to download and install the software.

GitHub is a cloud-based platform that hosts software development projects and manages version control using Git. I'm using GitHub in this project to act as the central remote host for my codebase, which allows me to securely store my files in the cloud and connect my local Amazon EC2 workspace to a remote repository for seamless version tracking.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-github_efaadbf7)

---

## My local repository

A Git repository is a digital storage space where all the files, folders, and historical changes of a software project are tracked using Git version control. It acts as a complete timeline for your codebase, allowing developers to save secure snapshots of their work, collaborate with others on the same files without overwriting changes, and revert to previous versions if errors occur.

Git init is a command that initializes a new, local Git repository in a project folder, setting up the necessary hidden files for Git to track code changes and history. I ran git init in my nextwork-web-project directory on my Amazon EC2 instance so that I could start tracking versions of my web application locally before connecting it to GitHub.

A branch in Git is an independent line of development that allows you to work on new features or bug fixes in isolation without affecting the main codebase. After running git init, the response from the terminal was Initialized empty Git repository in /home/ec2-user/nextwork-web-project/.git/, confirming that the hidden directory has been successfully created to start tracking all local version history within my project folder.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-github_7bf21bae)

---

## To push local changes to GitHub, I ran three commands

### git add

The first command I ran was git add . to stage all my project files for our first commit. A staging area is a middle-ground workspace in Git where you assemble and review the specific changes you want to include in your next snapshot before permanently recording them to your repository history.

### git commit

The second command I ran was git commit -m "Initial commit" to save my staged files and capture the first snapshot of my project. Using the -m flag stands for "message" and allows me to write a short, descriptive commit message directly in the command line, bypassing the need to open an external text editor to record the changes to my local repository history.

### git push

The third command I ran was git push -u origin main to upload my local commits to my remote repository. Using the -u flag stands for upstream, which links my local branch to the remote branch on GitHub. This simplifies my workflow because it configures the default remote destination, allowing me to run simple git push or git pull commands in the future without specifying the remote and branch names every time.

---

## Authentication

When I commit changes to GitHub, Git asks for my credentials because it needs to verify my identity and confirm that I have the authorized write permissions to push code modifications to the connected remote repository. Since HTTPS connections are stateless, Git requires this security check to prevent unauthorized users from altering the codebase hosted in the cloud.

### Local Git identity

Git needs my name and email because it uses this information to associate my identity with every commit I make, baking my authorship directly into the project's version history. This ensures that in collaborative workflows, teammates can easily identify who introduced specific changes and track the evolution of the codebase over time.

Running git log showed me that my local commit history is being successfully tracked, displaying a detailed record of the snapshot I created. The terminal output displayed the unique commit hash, my author name and email, the precise timestamp of the commit, and the commit message "Initial commit," confirming that my local changes are permanently recorded in the repository.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-github_9a27ee3b)

---

## GitHub tokens

GitHub authentication failed when I entered my password because GitHub phased out traditional password authentication for Git operations over HTTPS to prevent credentials from being intercepted over the internet. To minimize these security risks, GitHub now requires a unique and more secure credential, such as a personal access token (PAT), to verify my identity and authorize changes pushed from the command line.

A GitHub token is a highly secure, unique string of characters that acts as an alternative to a password for authenticating programmatic command-line actions. I'm using one in this project because GitHub has deprecated standard password authentication for HTTPS operations, meaning I must provide this token to prove my identity and securely push my web application files from my Amazon EC2 instance to my remote repository.

I could set up a GitHub token by navigating to my GitHub account settings, clicking on Developer settings at the bottom of the navigation panel, and selecting Tokens (classic) under the Personal access tokens menu. Once there, I select the option to generate a new classic token, assign it a descriptive note, set a safe expiration limit of 7 days, and check the box for the repo scope before generating and copying the final token to use as my secure command-line credential.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-github_fa11169d)

---

## Making changes again

I wanted to see Git working in action, so I edited my index.jsp file in VS Code by adding a new paragraph of HTML code and saving it. I couldn't see the changes in my GitHub repository initially because saving files in the editor only updates my local workspace on the Amazon EC2 instance, meaning I had to explicitly run git add, git commit, and git push to actually upload those local modifications to my remote origin in the cloud.

I finally saw the changes in my GitHub repository after running git add . to move my updated index.jsp file to the staging area, permanently recording the snapshot locally with git commit -m "Add new line to index.jsp", and executing git push. Once I authenticated by entering my username and pasting my personal access token, the terminal successfully uploaded the new commit to my remote origin, making the code updates immediately visible on my browser tab.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-github_6becb2bc)

---

## Setting up a READMe file

---

---
