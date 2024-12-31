---
layout: post
title:  "Difference between Merge and Rebase"
date:   2021-08-29
category: tech
comments_id: 2
---

In my initial days of git, I was a lot confused about merge and rebase. Though both works, it was not much clear which one to use. This post dives into the basic difference between the two.

<!--more-->

Consider the scenerio when you are working on a feature branch. The feature branch has moved some commits ahead, and so is the main branch. 

<img src="https://wac-cdn.atlassian.com/dam/jcr:1523084b-d05a-4f5a-bd1a-01866ec09ca3/01%20A%20forked%20commit%20history.svg?cdnVersion=1781">

Now we want to get all the extra new commits from the main branch into the feature branch. There are two ways we can do it, we can either merge main branch to our feature branch, or we can rebase our feature branch on the main branch.  What is the differenece between the two appraoches

### Git Merge
Git Merge takes all the new commits from the main branch, combines it together and applies it as big commit on our feature branch.

<img src="https://wac-cdn.atlassian.com/dam/jcr:4639eeb8-e417-434a-a3f8-a972277fc66a/02%20Merging%20main%20into%20the%20feature%20branh.svg?cdnVersion=1781">

### Git Rebase

The Git Rebase applies the commits from the feature branch one by one, on the top of the main branch first. Then it makes the feature branch point to the head of this new commits.

<img src="https://wac-cdn.atlassian.com/dam/jcr:3bafddf5-fd55-4320-9310-3d28f4fca3af/03%20Rebasing%20the%20feature%20branch%20into%20main.svg?cdnVersion=1781">

The main differene between the two is that how the git commit history is maintained. In the git merge case, all the commits of the merge branch will be present as a single commit in our feature branch. Whereas in the git rebase case all the commits of the main branch are as it is available in our feature branch and it will look like we started working from the HEAD of the main branch. 

### References and Image Credit
* [Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
* [Detailed Internal Working of Rebase](https://stackoverflow.com/questions/65225055/how-does-git-rebase-work-under-the-hood)


