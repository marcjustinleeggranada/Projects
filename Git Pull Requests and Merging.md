<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Git Pull Requests and Merging

**Project Link:** [View Project](https://nextwork.ai/projects/3ac00a14-cbfc-476a-9a2f-2d9b678880b9)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/3ac00a14-cbfc-476a-9a2f-2d9b678880b9_hh6gr5ka)

## Project Overview: Collaborating with Pull Requests

### What this project is about

In this project, I am using Git and GitHub to collaborate on a shared codebase by managing feature branches, opening pull requests for review, and safely integrating changes using different merging strategies while resolving any merge conflicts that arise.

## Planning Work with GitHub Issues

### Syncing the repo and creating an Issue

In this step, I'm syncing my local repository with the remote repository and creating a GitHub Issue so that I can align my workspace with the latest codebase and track my feature planning in a structured way.

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/3ac00a14-cbfc-476a-9a2f-2d9b678880b9_uqfpmygx)

### Issue number and planned feature

My Issue number is #2 and it plans to add a Resources section to learning-log.md, including helpful Git learning links to documentation and tutorials for future reference.

## Building a Feature Branch and Opening a Pull Request

### Creating the branch and PR

In this step, I'm creating a feature branch named after my issue so that I can add a Resources section to my learning log, push the updates, and open a pull request that links back to my original GitHub Issue for review.

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/3ac00a14-cbfc-476a-9a2f-2d9b678880b9_680ahudm)

### Linking the PR to the Issue

I added "Closes #2" to my PR body because it automatically links the pull request to my GitHub Issue, which helps track our progress and ensures GitHub automatically closes the associated issue once the code is successfully merged.

## Merging with a Merge Commit and Syncing Locally

### Merging and pulling changes

In this step, I'm merging my pull request on GitHub so that I can integrate my new changes into the main branch, automatically close the linked issue, and safely delete the deprecated feature branch both locally and remotely to keep our repository clean.

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/3ac00a14-cbfc-476a-9a2f-2d9b678880b9_hh6gr5ka)

### Merge strategy and auto-closing the Issue

I merged using the default merge commit strategy on GitHub, and Issue #2 closed automatically because it was linked directly to my pull request using a closing keyword in the description.

**Reference links:** the repository and its issues/PRs for this project have since been deleted, so the original links are no longer available.

### Key commands used in this stage

```
git checkout -b feature/2-add-resources
git add learning-log.md
git commit -m "Add resources section with helpful Git links"
git push --set-upstream origin feature/2-add-resources
# ...after PR is approved and merged on GitHub...
git checkout main
git pull origin main
git branch -d feature/2-add-resources
git push origin --delete feature/2-add-resources
```

## Squash Merging a Second Feature Branch

### Creating the second Issue and branch

In this step, I'm creating a second GitHub Issue for my next feature so that I can build a feature branch with multiple small commits, open a pull request, and perform a squash merge to simplify our repository history in the git log.

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/3ac00a14-cbfc-476a-9a2f-2d9b678880b9_lwk6giz0)

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/3ac00a14-cbfc-476a-9a2f-2d9b678880b9_0vuuamlc)

**Reference links:** as above, this repository has since been deleted, so no live links are available.

### Key commands used in this stage

```
git checkout -b feature/3-add-next-steps
git commit -m "Add Next Steps heading and first item"
git commit -m "Add remaining next steps"
git push origin feature/3-add-next-steps
# ...merged via "Squash and merge" on GitHub, then locally...
git checkout main
git pull origin main
git branch -D feature/3-add-next-steps
```

### Merge commit vs. squash merge: when I'd use each

- **Merge commit** (used for the first feature): keeps every individual commit and preserves the exact history of how the branch evolved. I'd reach for this on longer-lived branches or when a reviewer might want to see the step-by-step progression later — for example, during debugging or a detailed code review.
- **Squash merge** (used for the second feature): collapses all the small, messy, or "WIP" commits into one clean commit on `main`. I'd use this for short-lived branches with noisy commit histories, so the main branch log stays readable and each entry maps to one complete feature or fix rather than every intermediate save point.

In a real team setting, the choice usually comes down to a repo-wide convention rather than a per-PR decision — most teams pick one default strategy (often squash) to keep `main`'s history consistent, and only deviate for exceptions like release branches.

## Adding a Pull Request Template for Every Future PR

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/3ac00a14-cbfc-476a-9a2f-2d9b678880b9_03nvz0yg)

### Why the template must live on the default branch

In this project extension, I learned that the template must be on the default branch because GitHub only scans the repository's default branch to detect and render configuration files like a pull request template. If the template file only exists on an unmerged feature branch, the platform will not find it, and it will fail to auto-populate when users create a new pull request.

## What I'd Do Differently on a Real Team

This project covered the mechanics of the workflow well, but a few things would look different on an actual team:

- **Merge conflicts would be unavoidable**, not optional — with multiple people branching off `main` at the same time, I'd expect to resolve conflicts regularly rather than as an edge case. *(This run-through didn't hit a real conflict, so I'm not documenting a resolution here — I'd rather add a genuine example from a future project than fabricate one.)*
- **PR reviews would involve other people**, with required approvals and CI checks passing before merge, not just a self-review.
- **Branch naming and commit conventions** would follow a shared team standard (e.g. `feat/`, `fix/`, Conventional Commits) rather than whatever felt convenient solo.
- **The final repository history** would normally be worth screenshotting or linking to directly in a post like this — in this case the repository has since been deleted, so I don't have that artifact anymore, but I'd capture it before tearing down a repo next time.

## Reflections and Key Takeaways

### Tools and concepts learned

The key tools I used include Git, GitHub, and my local terminal to execute version control operations. Key concepts I learnt include creating structured pull requests, automatically linking and closing GitHub Issues, and utilizing different merge strategies to safely integrate feature branches into the main codebase.

### Time and challenges

This project took me approximately 90 minutes to complete. The most challenging part was mastering different merge strategies and resolving complex merge conflicts when aligning my local branches with the remote repository on GitHub.

### Final thoughts

I did this project today to learn how to effectively collaborate on a shared codebase using structured branching strategies, pull requests, and clean merge workflows on GitHub. Another skill I want to learn is how to implement automated CI/CD pipelines to seamlessly integrate these version control practices into collaborative deployment workflows.

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/3ac00a14-cbfc-476a-9a2f-2d9b678880b9)*
