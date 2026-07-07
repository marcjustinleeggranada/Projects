<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Git Undo, Recovery, and Debugging

**Project Link:** [View Project](https://nextwork.ai/projects/2a174c0b-492b-472c-b8de-11c58f71253a)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/2a174c0b-492b-472c-b8de-11c58f71253a_g4cvohgl)

## Project Overview: Mastering Git Recovery and Debugging

### What this project set out to achieve

In this project, I'm learning how to undo Git commits, recover lost branches, and debug Git history so that I can confidently manage code changes, resolve complex version control mistakes, and maintain a clean and reliable repository without fear of losing my work.

## Setting Up the Repository and Environment

### Goals for this setup step

In this step, I'm setting up Cursor, Git, and my GitHub connection to clone the project repository so that I can establish a fully functional local environment, create my starting files, and safely push them to my remote repository to begin tracking my progress.

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/2a174c0b-492b-472c-b8de-11c58f71253a_g1082umq)

### Configuring Git for this project

I configured my global user name and email using git config because Git requires this identity information to authoritatively sign each commit, ensuring my work is correctly linked to my GitHub account when history is recorded.

## Building a Meaningful Commit History

### Why a rich history matters for practice

In this step, I'm building a structured series of Git commits by adding four distinct documentation sections to my practice file so that I can push these sequential updates to my remote GitHub repository and verify a clean, chronological commit history.

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/2a174c0b-492b-472c-b8de-11c58f71253a_rxiot185)

### The value of granular commits

I committed separately because keeping my commits small and focused—a practice known as creating atomic commits—makes it much easier to track individual changes, troubleshoot errors, and safely revert specific updates in my commit history without impacting other parts of my codebase.

## Undoing Mistakes Safely with Reset and Revert

### Approach to undoing bad commits

In this step, I'm learning how to use git reset --soft and git revert so that I can safely undo both local and pushed Git commits, understand the critical differences between rewriting and preserving history, and confidently manage my commit log.

### Reset vs. revert: choosing the right tool

I would use git reset when I want to undo private, local commits that have not been shared, and git revert when I need to undo changes already shared with others because reset rewrites the commit history by moving the branch pointer backward, whereas revert safely preserves the chronological timeline by creating a new commit that applies the opposite changes.

## Recovering Lost Commits with Git Reflog

### Simulating and recovering from data loss

In this step, I'm simulating losing my progress using a hard reset and finding the SHA of the deleted commit with git reflog so that I can prove that lost work is still fully recoverable and restore it by creating a new branch.

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/2a174c0b-492b-472c-b8de-11c58f71253a_k4mtf1ce)

### How reflog sees what git log cannot

Git reflog can find the lost commit because while git log only traverses the reachable commit history of your current branch, git reflog acts as a temporary local ledger that records every movement of the HEAD pointer—such as checkouts, resets, and commits—allowing you to pinpoint and recover orphaned commits even after they have been disconnected from your visible branch history.

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/2a174c0b-492b-472c-b8de-11c58f71253a_quljmadv)

## Cherry-Picking a Hotfix Across Branches

### Setting up the cherry-pick scenario

In this step, I'm sIn this step, I'm setting up a feature branch containing both new features and a bug fix so that I can selectively cherry-pick only the critical bug fix commit onto my main branch, resolving the issue immediately without introducing any of my unfinished feature code.etting up... so that I can...

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/2a174c0b-492b-472c-b8de-11c58f71253a_glkgbt5x)

### When cherry-pick beats a full merge

I would use cherry-pick instead of merge because git cherry-pick allows me to selectively apply a single, specific commit—such as an urgent bug fix—from a separate branch, whereas merging would bring over the entire branch's history, potentially pulling unfinished features or unstable code into my main branch before they are fully ready.

## Hunting Down a Bug with Git Bisect

### Binary search through commit history

In this step, I'm using git bisect to perform a binary search through my commit history to find the exact bad commit that introduced a hidden bug, allowing me to isolate, inspect, and quickly resolve the culprit without having to manually review every single historic change.

### Identifying the first bad commit

Git bisect identified the commit with message "Add logging config". This was hard to find manually because the regression was a subtle logical error buried inside a massive diff across several files, making it incredibly tedious to locate by reading code, whereas git bisect used a systematic binary search to isolate the bad commit in only a few quick tests.

## Tagging a Release for CI/CD Readiness

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/2a174c0b-492b-472c-b8de-11c58f71253a_2r1c7yrq)

### Annotated vs. lightweight tags

In this project extension, I learned that annotated tags are for official public milestones and production releases because they store critical author, date, and verification metadata directly in the Git repository, while lightweight tags are for temporary, private, or local testing markers because they act as simple, un-annotated pointers to a specific commit without any additional overhead.

## Reflections and Wrap-Up

### Key tools and concepts from this project

The key tools I used include Git, Cursor, and GitHub to set up, track, and manage my local and remote codebases. Key concepts I learnt include configuring default editors, creating atomic commits, understanding the difference between rewinding local state with git reset versus preserving public history with git revert, recovering lost work via git reflog, strategically isolating specific fixes with cherry-picking, debugging codebases efficiently with git bisect, and marking key development milestones using annotated tags.

### Time and challenges

This project took me approximately 90 minutes to complete. The most challenging part was mastering the distinct workflows of git reset versus git revert and configuring Cursor as my default Git editor, but recovering lost commits using git reflog made the entire experience incredibly rewarding.

### Looking ahead

I did this project today to learn how to safely navigate version control mistakes, recover lost work, and systematically debug repository history using tools like git reflog and git bisect. Another skill I want to learn is to master application containerization with Docker and set up automated CI/CD pipelines so I can build, test, and deploy my code securely and efficiently.

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/2a174c0b-492b-472c-b8de-11c58f71253a)*
