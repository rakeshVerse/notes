---
title: GitHub Contribute
updated: 2022-10-21 17:13:15Z
created: 2022-10-17 00:14:42Z
latitude: 52.37021570
longitude: 4.89516790
altitude: 0.0000
---

*Created on: 17.10.2022 5:45 AM*

# Fork
A fork is a copy of a repository. This is useful when you want to contribute to someone else's project or start your own project based on theirs. When you fork a repo., it creates a copy of that repo. in your GitHub account. 
<br>
# Clone
A clone is a full copy of a repository, including all logging and versions of files into your local machine so that we can now proceed to contributing to the project. 

Go to the original repository, and click the green "Code" button to get the URL to clone, then run following command:
`git clone <URL>`  # it will create a folder with original repo. name & download complete repo. inside that folder
`git clone <URL> <folder-name>`  # in case you can name the folder other than the original repo. name

### Configuring Remotes
Basically, we have a full copy of a repository, whose **origin** we are not allowed to make changes to.
Let's see how the **remotes** of this Git is set up: 
`git remote -v` # it gives the URL of remote repo.

We see that **origin** is set up to the original repository, we also want to add our own **fork**.

According to Git naming conventions, it is recommended to name your own repository **origin**, and the one you forked from **upstream**:

1. First, we rename the original **origin** remote to **upstream**: `git remote rename origin upstream`
Now, check the **remotes**, you will see **origin** has been renamed to **upstream**: `git remote -v`

2. Then fetch the **URL** of our own **fork** & set it as **origin**:
	- Go to your fork of the original repo. & Copy the **URL** by clicking on **Code**
	- Add it as **origin**: `git remote add origin <fork-URL>`


Now, `git remote -v` will show 2 remotes repos:
- **origin:** our own fork, where we have read and write access
- **upstream:** the original, where we have read-only access
<br>
# Send Pull Request
Now we can start working on our local repo. Once done:
1. **Commit** your changes to your **forked** repo.
2. Push the **Commit** on your **forked** remote repo.: `git push origin`
3. Send **pull request**: You can now send a pull request form your **forked** repo to **original** repo on GitHub. 
4. **Approving** Pull Requests: Now, the administrators of the **original** repo should be able to view your pull request. They can then review it & if every thing is alright then merge your **commit** to the **original** repo.