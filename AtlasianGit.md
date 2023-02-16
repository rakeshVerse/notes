- Aliases
  - Using git config 
    ```
    git config --global alias.st status 
    git config --global alias.co checkout 
    git config --global alias.br branch 
    git config --global alias.up rebase 
    git config --global alias.ci commit
    git config --global alias.amend ci --amend
    ```
  - Directly editing Git config files
    ```
    [alias]
      co = checkout
      br = branch
      ci = commit
      st = status
    ```
  for more [info](https://www.atlassian.com/git/tutorials/git-alias)
  
- Git Stash -
  Temporarily shelves (or stashes) changes you've made to your working copy so you can work on something else, and then come back and re-apply 
  them later on. Stashing is handy if you need to quickly switch context and work on something else, but you're mid-way through a code change and aren't 
  quite ready to commit.
  - Create Stash - `git stash` give you clean working directory. You're free to make changes, create new commits, switch branches, and perform any other 
    Git operations; then come back and re-apply your stash when you're ready. Note that the stash is local to your Git repository; stashes are not 
    transferred to the server when you push. Tt's good practice to annotate your stashes with a description, using `git stash save "message"`
    By default, `git stash` will only stash **tracked files**
      - To stash untracked files also: `git stash -u`
      - To stash ignored files also: `git stash -a | --all`
      
  - Get Stash back - `git stash pop` Popping your stash removes the changes from your stash and reapplies them to your working copy.
    Alternatively, you can reapply the changes to your working copy and keep them in your stash with `git stash apply`.
    
    for more [info](https://www.atlassian.com/git/tutorials/saving-changes/git-stash)
    
- Tag - Tagging is an additional mechanism used to create a snap shot of a Git repo. Tagging is traditionally used to create semantic version number 
  identifier tags that correspond to software release cycles. The git tag command is the primary driver of tag: creation, modification and deletion. 
  There are two types of tags; **annotated** and **lightweight**. Annotated tags are generally the better practices as they store additional valuable meta data about the tag.
  
    - Lightweight - `git tag <tagname>`
    - Annotated - `git tag -a <tagname>` Ex. `git tag -a v1.4`
    - Runnig these commands will associate tag to lastest commit. To tag past commit: `git tag -a <tagname> <commit_hash>`
    - Pushing Tags to Remote: Tags have to be explicitly passed to `git push` - `git push origin v1.4`
    - Checking Out Tags - You can view the state of a repo at a tag by using the `git checkout` command - `git checkout v1.4`

- Checkout- Checking out an old file does not move the HEAD pointer. It remains on the same branch and same commit, avoiding a 'detached head' state. You can then commit the old version of the file in a new snapshot as you would any other changes. So, in effect, this usage of git checkout on a file, serves as a way to revert back to an old version of an individual file.

  `git checkout a1e8fb5`
  
  This makes your working directory match the exact state of the a1e8fb5 commit. You can look at files, compile the project, run tests, and even edit files without worrying about losing the current state of the project. Nothing you do in here will be saved in your repository. To continue developing, you need to get back to the “current” state of your project:

    `git checkout main`
    
    [Add checkout, reset, revert diagrams for Atlassian](https://www.atlassian.com/git/tutorials/undoing-changes/git-reset)
  

- `git rm <file>' is equivalent to `rm <file>` + `git add <file>`

- Remove untracked files: `git clean`. Options, n - dry run, f-force removal, d - remove untracked directories
  
- View commit history reference: `git reflog`
  
- Update feature branch with origin main: `git pull --rebase origin main` The --rebase option tells Git to move all of feature branch commits to the tip of the main branch after synchronising it with the changes.
