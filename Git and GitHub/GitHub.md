# GitHub: Working with Remote

- git clone URL // Git clone is used to clone a remote repository into a local workspace

- git push // Git push is used to push commits from your local repo to a remote repo

- git pull // Git pull is used to fetch the newest updates from a remote repository

- If we want to make a change to a remote branch, Pull the remote branch, merge it with the local branch, 
then push it back to its origin.
 

- View Remote:

    git remote  // Lists remote repos
    
    git remote -v // List remote repos verbosely
    
    git remote show origin // get more info. about remote
    
    git branch -r // List of remote branches that Git is tracking


If someone has updated a repository since the last time you synchronize your local copy, Git will tell you that it's time to do an
update. If you have your own local changes when you pull down the code from the remote repo, you might need to fix merge
conflicts before you can push your own changes. In this way Git let's multiple people work on the same project at the same time.
When pulling new code it will merge the changes automatically if possible or will tell us to manually perform the integrations, if there 
are conflicts. 

So when working with remotes the workflow for making changes has some extra steps. Will still modify stage and commit our local changes.
After committing, we'll fetch any new changes from the remote repo manually merge if necessary and only then will push our changes to the 
remote repo. 

Git supports a variety of ways to connect to a remote repository. Some of the most common are using the HTTP, HTTPS and SSH protocols
and their corresponding URLs. HTTP is generally used to allow read only access to a repository. In other words, it lets people clone the contents of
your repo without letting them push new contents to it. Conversely HTTPS and SSH, both provide methods of authenticating
users so you can control who gets permission to push. 

Remote repositories have a name assigned to them, by default, the assigned name is origin.
This lets us track more than one remote in the same Git directory. After cloning the remote repo we can see the config


Basic Remote Workflow
    1. Pull. pull changes from remote repo to sync local repo before pushing your changes 
        > git pull // downloades all remote branches
        > git pull origin/master // downlaodes remote master branch 
    2. Review. review the conflict, if any. 
        To view commit history > git log --graph --oneline --all
        To view actual changes in file > git log -p origin/master
    3. Resolve. resolve- resolve the conflict by manually editing the conflict file, also, search for '>>>' to ensure that no conflict left
    4. commit
    5. push


- Fetching new changes: Before pushing our changes to remote our local repo must be updated/synced with remote. 
    To do that first fetch the remote changes then merge them to local branches:

    1. First check if any changes made to remote branch > git remote show origin
    
    2. If yes, then fetch > git fetch
        After fetching remote changes, we can view the commit log of origin master:
        > git log origin/master  

        Also, we can checkout to remote branches to view the working tree:
        > git checkout origin/master

    3. Merge remote master into local master
        git checkout master 
        git merge origin/master

    4. Now, we can push our changes > git push origin/master

- Pulling: Since fetching and merging is very common operation, we can do it in single step:
    > git pull // download all remote branches and automatically try to merge them

    It will fetch the remote changes (all the remote branches) and merge them into local repo.
    
    Suppose, pulling fetches a new remote branch which doesn't exist in local repo. All you have to 
    do to have the new remote branch is:

        > git checkout new_remote_branch_name

    If we want to get the contents of remote branches without automatically merging any contents 
    into the local branches, we can call 

        > git remote update // Fetches the most up-to-date objects

    This will fetch the contents of all remote branches so that we can just call checkout or merge as needed.


Pull-Merge-Push Workflow:

Case 1 Master branch merge without conflict: You cloned the repo. Somebody added commits to remote repo. You pull the remote changes. Fast forward merge.

Case 2 Master branch merge with conflict: You cloned the repo. Added some commits to your master. Ready to push, but a teammate/collaborator updated remote. Now you have to sync your master with remote before pushing. If you do `git pull`, merge conflict may arise, results in Three-way-merge. When Git needs to do a three-way merge, we end up with a separate commit for merging the branches back into the main tree. 

Case 3 Feature branch merge with REBASE: When using Git to work on a new feature or a big refactor of some kind, it's recommended best practice to create separate branches.
There are many advantages to doing this. For example, it might take you a while to finish a new feature and in the meantime, there could be a critical bug that needs fixing in the main branch of the code. By having separate branches, you can fix the bug in the main branch, release a new version and then go back to working on your feature without having to integrate your code before it's ready. Another advantage of working in separate branches is that you could even release two or more versions out of the same tree. One being the stable version and the other being the beta version. That way, any disruptive changes can be tested on
a few users or computers before they're fully released. 

    
So, you  create afeature branch on local repo, made commits. Before you merge it to master, push the feature branch to remote. So, that the collaborators can review it.
Then you can push the feature branch > git push -u origin feature
Once feature branch has been properly reviewed and tested, it can get merged back into the master branch. This can be done by us or by someone else.
One option is to use the git merge command that we discussed earlier. Another option is to use the git rebase command. Rebasing means changing the base commit that's used for our branch.

![3way-merge](assets/images/3way-merge-trans.png)

![3way-merge](assets/images/3way-merge-white.png)

![3way-merge](assets/images/3way-merge-black.png)