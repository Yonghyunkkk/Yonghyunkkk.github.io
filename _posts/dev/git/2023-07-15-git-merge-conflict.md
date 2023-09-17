---
title: "[Git] Merge Conflict"
date: 2023-07-15
categories: [Dev, Git]
tags: [Git]
---

## Problem

When working with your colleagues using git, you may have all experienced merge conflict. It is easy to encounter merge conflict whenever we collaborate code with others. Merge conflict occurs when two different branches or commits in a version control system (such as Git) modify the same file(s) in conflicting ways.

Recently, I have been experiencing merge conflict a lot, since me and my colleague had some miscommunication, which lead us modifying the same file(s). I wanted to know the best practices of solving a merge conflict, and there were mainly 3 options that we could choose.

## Solution

First, we have to move to the branch that we are unable to merge to another branch due to merge conflict. Then, we use the command `git merge {other_branch_name}` to merge the branch that has the merge conflict with the current branch. In case we want to undo the merge, we can use the command `git merge --abort`. Lastly, we check the file(s) that have the conflicts using our editor.

There will be 3 options displayed, which are ‘Accept Current Change’, ‘Accept Incoming Change’, and ‘Accept Both Changes’.

- Accept Current Change accepts only the change that you have made to the file(s).
- Accept Incoming Change accepts only the change that the other branch have made to the file(s).
- Accept Both Changes accept both changes that you and the other branch have made. It is you and your team’s decision to choose the best option for your project!

After you have made the changes, use `git add .` and `git commit -m {msg}` to push your code and merge it without having a merge conflict.
