---
title: GitHub Pages
updated: 2022-10-21 17:13:48Z
created: 2022-10-16 23:44:36Z
latitude: 52.37021570
longitude: 4.89516790
altitude: 0.0000
---

*Created on: 17.10.2022 5:15 AM*

With GitHub pages, GitHub allows you to host a webpage from your repository. 

# Create a New Repository
Create a new GitHub Repo to create a GitHub page.
This repository needs a special name to function as a GitHub page. It needs to be your GitHub `username`, followed by `.github.io` i.e. make a repo with name: `username.github.io`

# Push existing Local Repo
1. Add Remote Repo to local: add this new repository as a remote for our local repository, we are calling it gh-page (for GitHub Pages):
`git remote add gh-page <remote-repo-URL>`
2. Push the master branch to the new remote: `git push gh-page master`
3. Now, you can create webpage as your will, then push it to the remote & it will reflect on Github Page by URL:
https://<user_name>.github.io/