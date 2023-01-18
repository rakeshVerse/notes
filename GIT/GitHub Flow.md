---
title: GitHub Flow
updated: 2022-10-20 00:42:20Z
created: 2022-10-16 23:39:18Z
latitude: 52.37021570
longitude: 4.89516790
altitude: 0.0000
---

*Created on: 17.10.2022 5:09 AM*

The GitHub flow is a workflow designed to work well with Git and GitHub.

It focuses on branching and makes it possible for teams to experiment freely, and make deployments regularly.

The GitHub flow works like this:
- **Create a new Branch**
Branching is the key concept in Git. And it works around the rule that the master branch is ALWAYS deployable.
That means, if you want to try something new or experiment, you create a new branch! Branching gives you an environment where you can make changes without affecting the main branch.
When your new branch is ready, it can be reviewed, discussed, and merged with the main branch when ready.
When you make a new branch, you will (almost always) want to make it from the master branch.
- **Make changes and add Commits**
After the new branch is created, it is time to get to work. Make changes by adding, editing and deleting files. Whenever you reach a small milestone, add the changes to your branch by commit.
- **Open a Pull Request**
Pull requests are a key part of GitHub. A Pull Request notifies people you have changes ready for them to consider or review.
 You can ask others to review your changes or pull your contribution and merge it into their branch.
- **Review**
When a Pull Request is made, it can be reviewed by whoever has the proper access to the branch. This is where good discussions and review of the changes happen.
Pull Requests are designed to allow people to work together easily and produce better results together!
If you receive feedback and continue to improve your changes, you can push your changes with new commits, making further reviews possible.
- **Deploy**
When the pull request has been reviewed and everything looks good, it is time for the final testing. GitHub allows you to deploy from a branch for final testing in production before merging with the master branch.
If any issues arise, you can undo the changes by deploying the master branch into production again!
- **Merge**
After exhaustive testing, you can merge the code into the master branch!
Pull Requests keep records of changes to your code, and if you commented and named changes well, you can go back and understand why changes and decisions were made.
