---
title: Git Basics
updated: 2022-10-20 00:41:27Z
created: 2022-10-15 18:28:55Z
latitude: 52.37021570
longitude: 4.89516790
altitude: 0.0000
---

*Created on: 16.10.2022 2:44 AM*

## <u>Basic commands</u>

- **Step 1:** Initailize to make project folder a GIT repo: `git init`
- **Step 2:** Create files & start working on your project. (To check the *status* of your repo: `git status`)
- **Step 3:** After you have completed a functionality or a milestone *add* your files to the Staging Environment:
    `git add [file_name]...` add using file names
    `git add --all` or `git add -A` add all the created, modified & deleted files
- **Step 4:** Once files are staged, they are ready to commit. Commit is savepoint of your project. You can revert back to any commit or savepoint in case some error occures.
    `git commit -m "Message"`
    You can stage & commit at the same time by using **-a** option: `git commit -a -m "Message"`
    **Warning:** Skipping the Staging Environment is not generally recommended.

## <u>Help</u>

If you are having trouble remembering commands or options for commands, you can use Git help.
There are a couple of different ways you can use the help command in command line:
`git [command] -help` \- See all the available options for the specific command, e.g. `git commit -help`
`git help --all` \- See all possible commands