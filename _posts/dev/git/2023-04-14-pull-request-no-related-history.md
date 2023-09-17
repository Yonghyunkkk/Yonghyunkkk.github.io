---
title: "[Git] Make pull request when branch & master have no related history"
date: 2023-04-14
categories: [Dev, Git]
tags: [Git]
---

## Problem

Recently, I have been working on a project and I started developing on branch_x without checkout from master. This caused no common ancestor between branch_x and master. So, when I tried to make a pull request to master, I got the error : **"There isn't anything to compare. Master and branch_x are entirely different commit histories."**

## Solution

To solve this problem, I added the **"--allow-unrelated-histories-flag"**. This option will tell Git that we allow merging branches with no common history base, which then should finish the merge without errors.

```text
git pull origin master(or whatever branch) --allow-unrelated-histories
git push origin branch_x
```

After executing this command, you should be able to compare and make a pull request. Before executing this command, you should checkout to the branch that you want to make a pull request.
