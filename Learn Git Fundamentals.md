<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Learn Git Fundamentals

**Project Link:** [View Project](https://nextwork.ai/projects/8bf3bcb5-a70d-418a-9c76-251365f69028)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/8bf3bcb5-a70d-418a-9c76-251365f69028_l5jsusg6)

## Project Overview: Learning Git Version Control

### Goals and objectives

In this project, I'm building a local Git repository and connecting it to GitHub to version-control a markdown file, create development branches, and resolve deliberate merge conflicts so that I can master the foundational source control workflows required to track code changes, collaborate with other developers, and safely manage my codebase in real-world software projects.

## Setting Up the Development Environment

### Installing Git and Cursor

In this step, I'm setting up Git and my code editor on my computer, while also creating a GitHub account, so that I can track changes to my code locally and publish my projects to a remote repository.

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/8bf3bcb5-a70d-418a-9c76-251365f69028_ryyzlsf8)

## Configuring Git and Creating the Learning Log

### Setting up Git identity and project file

In this step, I'm setting up my Git identity with my name and email and creating a project folder with a markdown file, so that my local commits are correctly attributed to me and I have a structured space to document my progress.

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/8bf3bcb5-a70d-418a-9c76-251365f69028_d6lm2bxt)

### Understanding global Git configuration

The --global flag means my identity configuration will apply to every Git repository on my computer rather than just a single project. I used a specific email because it matches my GitHub account, which ensures that my local commits are correctly linked and credited to my profile when I publish them online.

## Initializing a Repository and Making Commits

### Creating the first commits

In this step, I'm initializing a local Git repository in my project folder and making my first commits so that I can capture snapshots of my file changes and track my progress over time.

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/8bf3bcb5-a70d-418a-9c76-251365f69028_blkivqea)

### Understanding git add vs git commit

git add stages specific file modifications to prepare them for the next snapshot, while git commit permanently saves those staged changes as a historical snapshot in the Git repository.

## Branching and Working in Parallel

### Creating and switching branches

In this step, I'm creating a new Git branch and making isolated changes before making conflicting edits on the main branch, so that I can intentionally trigger and learn to resolve a merge conflict.

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/8bf3bcb5-a70d-418a-9c76-251365f69028_drz4zcda)

### Why merge conflicts occur

A merge conflict happens because Git cannot automatically determine which changes to keep when two different branches modify the exact same line of a file. Since Git does not know whether to prioritize the edits from your feature branch or the main branch, it pauses the merge process and asks you to manually decide how to combine them.

## Merging Branches and Resolving Conflicts

### Merging feature branches into main

In this step, I'm merging two conflicting branches and reading the conflict markers in my file, so that I can manually resolve the differences and safely complete a merge commit.

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/8bf3bcb5-a70d-418a-9c76-251365f69028_0e34g9cu)

### Interpreting Git conflict markers

The conflict markers show me the exact boundaries where competing changes have occurred in a file. The HEAD section contains the changes from my current active branch, while the other section contains the incoming edits from the branch I am attempting to merge.

## Publishing to GitHub

### Creating a remote repository

In this step, I'm creating a public GitHub repository and pushing my local repository to it, so that I can backup my work in the cloud and make my commit history and branches visible online.

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/8bf3bcb5-a70d-418a-9c76-251365f69028_l5jsusg6)

### Pushing local commits to GitHub

I ran git push to upload my local commits to my remote repository on GitHub so they are securely backed up. I needed a remote because Git requires a defined destination URL to know exactly where in the cloud to send and sync my codebase.

## Bonus: Building a GitHub Profile README

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/8bf3bcb5-a70d-418a-9c76-251365f69028_5y2qcn3e)

### Commands used to publish the Profile README

In this project extension, I used the commands git add to stage my new file, git commit to record the snapshot of my profile changes, and git push to upload and display my completed README directly on my GitHub profile.

## Reflections and Key Takeaways

### Tools and concepts mastered

The key tools I used include Git, Cursor, and GitHub to manage and host my codebase. Key concepts I learnt include repository initialization, staging files, creating local commits, managing parallel branches, resolving merge conflicts using markers, and pushing code to remote repositories.

### Time and challenges

This project took me approximately 45 minutes. The most challenging part was manually resolving the merge conflict because I had to carefully inspect the conflict markers to determine which changes from each branch to keep, clean up the helper lines, and finalize the file structure before creating the merge commit.

### Looking ahead

I did this project today to learn how to manage version control, work with parallel branches, and confidently resolve merge conflicts using Git. Another skill I want to learn is application containerization with Docker and setting up CI/CD pipelines so that I can easily package, automate, and deploy my web applications securely.

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/8bf3bcb5-a70d-418a-9c76-251365f69028)*
