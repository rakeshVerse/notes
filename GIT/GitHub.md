---
title: GitHub
updated: 2022-10-21 17:16:40Z
created: 2022-10-15 23:11:24Z
latitude: 52.37021570
longitude: 4.89516790
altitude: 0.0000
---

*Created on: 16.10.2022 4:41 AM*

# 1. Create/Login to GitHub

<br>

# 2. Initial Push/Pull Repo
There are two ways we can go about it:
**=>** If you have an existing Local Repo, then first **create** a GitHub Repo & then **Push** the Local Repo to the GitHub Repo
**=>** If you have an existing GitHub Repo, then first **create** a Local Repo & then **Pull** GitHub Repo to that Local Repo
1.  **Push Local Repo to the GitHub**
	1. **Add remote repo:**  `git remote add origin <repo-url>`
	E.g.: `git remote add origin https://github.com/w3schools-test/hello-world.git`
		<br>
		Now, when you try to push or pull from a remote repo, it ask you your GitHub/BitBucket account credential (user-name & password). But GitHub no longer uses password for authenticating user, so you need to provide **Personal Access Token** instead. 
	**Note:** If you don't want to provide credentials at the time of push or pull then directly provide *Personal Access Token* at the time of adding remote repo. This will skip authentication while push & pull:
	`git remote set-url origin https://<token>@github.com/<username>/<repo>`
	2. **Push:** Now that we have added remote repo to our local repo, we can upload/push local files to GitHub: 
	`git push --set-upstream origin master`  push local master branch to the origin url, and set it as the default remote branch
2. **Pull GitHub Repo to Local**
	1. **Create Local Repo:** 
	`mkdir <project-name>`
	`cd <project-name>`
	`git init`
	2. **Add remote repo:**  `git remote add origin <repo-url>`
	3. **Pull:** `git push -u origin`
Edit some code on GitHub


<br>

# 3. Git Pull from GitHub
Pulling to Keep up-to-date with Changes.
First edit some code on GitHub to demonstrate Pull. Lets edit README.md file on GitHub.
Now there are two ways to Pull the remote changes to the Local Repo:
1. **fetch & merge**
	1. **fetch:** gets all the change history of a tracked branch/repo: 
		`git fetch origin` # see what has changed on GitHub
		Now that we have fetched the changes, we can check what exactly has changed on remote branch by using one of the following commands:
		 `git status`  # show status
		 `git log origin/master` # show commit log
		 `git diff origin/master` # show the differences between local master and origin/master
		 
	2. **merge:** combines the current branch, with a specified branch. 
	Now that we have confimed that remote branch has some changes, we can now combine the local branch (master), with a remote branch (origin/master) to update the Local Repo:
	`git merge origin/master`
3. **pull**
	We can **fetch** & **merge** with single command only:
	`git pull origin` # update local Git
	

<br>

# 4. Git Push to GitHub
Edit some code on Local Repo & commit. Now, check the status `git status`. It will show that the local branch is ahead of remote branch by 1 commit.
We can now push this update to remote branch (origin/master): `git push origin`


<br>

# 5. Branch

**<u>Pull branch for Github</u>**
1. Create a new branch on Github & make some changes to any file. Now we have a new branch with its own veriosion of code
2. Now on local, pull from our GitHub repository so that our code is up-to-date: `git pull`
		It will Pull all the remote repo changes (branches, file changes, etc).
		Now that we have pulled from remote, we can view the list of branches:
		`git branch` # show all local branches
		`git branch -a` # show all local & remote branches
		`git branch -r` # show remote branches
3. Checkout to the new remote branch: `git checkout <new-remote-branch>`
4. Check if it is all up to date: `git pull`

That is how you pull a GitHub branch to your local Git.

**<u>Push local branch to Github</u>**
1. Create a new branch on local 
2. Make some changes & commit.
3. Push the branch to Github: `git push origin <branch-name>`  
4. Now that we have 2 branches other than master branch, Github will show the notification to create a **Pull Request**.
A pull request is how you propose changes. You can ask someone to review your changes or pull your contribution and merge it into their branch. A Pull request lets you review the changes and merge them to a branch. Since this is your own repository, you can merge your pull request yourself.
The pull request will record the changes, which means you can go through them later to figure out the changes made.
After merging, to keep the repo from getting overly complicated, you can delete the now unused branch by clicking "Delete branch".


