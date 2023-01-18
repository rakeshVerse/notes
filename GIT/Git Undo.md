---
title: Git Undo
updated: 2022-10-21 17:18:13Z
created: 2022-10-19 23:55:44Z
latitude: 52.37021570
longitude: 4.89516790
altitude: 0.0000
---

*Created on: 20.10.2022 5:31 AM*

# Git Revert
**revert** is the command we use when we want to take a previous **commit** and add it as a new **commit**, keeping the log intact.

![img_revert_part1.gif](../_resources/img_revert_part1.gif)

![img_revert_part2.gif](../_resources/img_revert_part2.gif)

**Step 1: Find the previous commit**
To do that, we need to go through the **log**.
To avoid the very long log list, we are going to use the **--oneline** option, which gives just one line per commit: `git log --oneline`
O/p shows the first seven characters of the commit hash & the commit message.

**Step 2: Use it to make a new commit**
We revert the latest **commit** using git **revert HEAD** (**revert** the latest change,  and then **commit**), adding the option **--no-edit** to skip the commit message editor (getting the default revert message):
`git revert HEAD --no-edit`

> Note: To revert to earlier commits, use git revert HEAD~x (x being a number. 1 going back one more, 2 going back two more, etc.)

<br>

# Git Reset
**reset** is the command we use when we want to move the repository back to a previous **commit**, discarding any changes made after that **commit**.

![img_reset_part1.gif](../_resources/img_reset_part1.gif)

![img_reset_part2.gif](../_resources/img_reset_part2.gif)

**Step 1: Find the previous commit:** `git log --oneline`

**Step 2: Move the repository back to that step**
We reset our repository back to the specific commit using git reset commithash (commithash being the first 7 characters of the commit hash we found in the log): `git reset 9a9add8`

> **Warning:** Messing with the commit history of a repository can be dangerous. It is usually ok to make these kinds of changes to your own local repository. However, you should avoid making changes that rewrite history to remote repositories, especially if others are working with them.

### Git Undo Reset
Even though the commits are no longer showing up in the log, it is not removed from Git. If you know the commit hash you can reset to it: `git reset e56ba1f`


<br>


# Git Amend
**commit --amend** is used to modify the most recent **commit**. It combines changes in the **staging environment** with the latest **commit**, and creates a new **commit**. This new **commit** replaces the latest **commit** entirely.

### Git Amend Commit Message
One of the simplest things you can do with --amend is to change a commit message. Let's update the README.md and commit: `git commit -m "Adding plines to reddme"`

Oh no! the commit message is full of spelling errors. Let's amend that: `git commit --amend -m "Added lines to README.md"`

This will replace the previous **commit** with the amended one.

> **Warning:** Messing with the commit history of a repository can be dangerous. It is usually ok to make these kinds of changes to your own local repository. However, you should avoid making changes that rewrite history to remote repositories, especially if others are working with them.

### Git Amend Files
Adding files with **--amend** works the same way as above. Just add them to the **staging environment** before committing.