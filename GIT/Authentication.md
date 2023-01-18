---
title: Authentication
updated: 2022-10-20 00:41:19Z
created: 2022-10-16 15:24:46Z
latitude: 52.37021570
longitude: 4.89516790
altitude: 0.0000
---

*Created on: 16.10.2022 8:55 PM*

You need to let Git know who you are. This is important for version control systems, as each Git commit uses this information. Provide the user-name & email of your GitHub/BitBucket account:
`git config --global user.name "user-name"`
`git config --global user.email "email@address.com"`
`git config --list`  or `git config -l`  view config file containts, .gitconfig file can be found in user Home 
Change the user name and e-mail address to your own. You will probably also want to use this when registering to GitHub later on.

**Note:** Use `global` to set the username and e-mail for every repository on your computer.
If you want to set the username/e-mail for just the current repo, you can remove `global`

When you try to push or pull from a remote repo, it ask you your credential (user-name & password).
GitHub no longer authenticate user using password, so you need to create a **Personal Access Token:**

> *My Account → Settings → Developer settings → Personal access tokens → Generate new token*

After creating the token save it somewhere safely.
