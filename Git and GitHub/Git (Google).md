- Diff and Patch: Suppose your script is not working, you send it to your friend, your friend fixes the script and sent you new working copy.
    Now, you can replace your original file with his file. But that is not a good idea. As, his copy may not be updated as you may have 
    work on the original file after sending him to fix bug. 
    Better way is to apply the lines he added or removed only to the original file that coping his entire code.
    To do that:

    - Diff: Get the diff of two files (original & friend's file) and print the diff in a new file:

        > diff -u yourfile friendsfile > newfile.diff

    - Patch: Now, instead of applying the changes manually we automate the merge by passing newfile.diff as an input to patch command
        Patch is useful for applying file differences:

        > patch yourfile < newfile.diff

        Patch will apply the changes that come from newfile.diff to yourfile.


Git Flow:
    - Config. To view config: > git config -l
    - Initialize git
    - Create files
    - Add files to Staging Area/Index
    - Commit will save what have been added to index only, unstaged and modified files will be ignored
    
Repo structure: Each repo has .git directory, a working tree and staging area
    - .git folder contains all the info- commits, index, config, branches, remote, etc
    - Working tree is present working directory

File States: Files can be in 3 different states
    - Modified - Add, Delete, Edit file and its contents. Whenever we make changes in Working Tree git will mark those changed 
    files as modified.
    - Stage - Add files to Index
    - Commit the changes to save/capture a snapshot

Commit:
    - Never use the -m <msg> / --message=<msg> flag to git commit. It gives you a poor mindset right off the bat as you will feel 
that you have to fit your commit message into the terminal command

    - A more useful commit message might be:

        Redirect user to the requested page after login
        
        https://trello.com/path/to/relevant/card
        
        Users were being redirected to the home page after login, which is less
        useful than redirecting to the page they had originally requested before
        being redirected to the login form.
        
        - Store requested path in a session variable
        - Redirect to the stored location after successfully logging in the user


    To write such commit message

        > git commit 
        
    It will open an editor to write commit message. The first line should explain the changes briefly. Then an empty line.
    After that you can add paragraphs to explain the changes in more detail

- Skipping Staging:
    We can skip the Staging/Indexing and directly commit the changes using -a option with commit command.
    Important to note that -a is not same as 'git add'. 
    'git add' will add the unstaged/untracked files  & changes to tracked files to Staging Area. 
    While -a will Stage any changes to tracked files (files that are already added to Stage using git add) and commit them in one step.
    Also, While using -a option we cannot write descriptive comments. 
    
        > git commit -a -m "Commit message"

- HEAD- Git uses HEAD alias to represent currently checked-out snapshot of your project. HEAD defined the current content of
    the working tree. HEAD can be considered as a bookmark. We can shift the HEAD to any commit from the past and the working tree
    will be updated to reflect the snapshot of the commit.

- Getting more info. about our changes:
    Committed changes: 

        - git log 
        - git log --stat // additional statistics of changes 
        - git log -p // view associate patches also
        - git log -p -2 // -2 flag will limit the log to latest 2 commits
        - git log --graph --oneline // --graph shows the commit graph & --oneline shows one line per commit
        - git show <commit_hash> // view patches of the any commit using commit hash

    Un-committed changes: 
        If you are working on big feature, and you want to review changes before adding them.
            - git diff // shows the diff between staged and unstaged files, it is equivalent of 'diff -u', useful to review changes before adding them to index
            - git diff --staged // view changes that are staged but not commited (diff of HEAD and Index), useful to review the staged changes before committing them. An alias to --cached, this will show all staged files compared to the named commit
            - git diff main.js // to see the diff of particular file instead of entire working tree
    
        Another way of reviewing your changes before staging is to use -p flag with git add, it will show the changes and ask 
        for confirmation where you want to stage those changes or not.
            - git add -p // Allows a user to interactively review patches to add to the current commit

- Removing and Renaming/Moving files
    - Remove a file and stage the change `> git rm [file_name]`, After that you can commit, 
        it's equivalent of `rm <file_name>` & `git add [file_name]`
    - Rename/Move a file and stage the changes `> git mv [old_file] [new_file]`, now you can commit
    - .gitignore - A file containing a list of files or filename patterns for Git to skip for the current repo. there could be some 
    files in our working tree that we don't want to tracked, create a .gitingore file and 
        insert the name of file which you want to be ignored:
        `> echo test.txt > .gitignore`
       Now, add .gitignore file to Index to be tracked.
       List of some common .gitignore file config: https://gist.github.com/octocat/9257657   
   
- Undoing Changes (Checkout, Reset & Revert)
    - Undoing Changes Before Commit
        - Undoing Unstaged Changes
            If you make some changes to a file but you don't want them to be statged or commit. You want to get rid of those changes.
            Checkout command will help  you with that
                > git checkout <file_name> // restore the file to the latest stored snapshot/commit, it will revert the changes to
            modified files before they get Staged
    
            - we can also use -p flag to get interative mode which shows the diff line by line, which helps to review the file before restoring.
        
        - Undoing Staged Changes
            If you added the changes to Staging Area that you don't want to commit, you can unstage our changes by using git reset 
                > git reset HEAD <file_name>
            It resets the file with the file in current snapshot i.e. HEAD. Reset is opposite of Add. Add adds file to index. Reset 
            removes files from index. Also, you can use -p flag to get interactive window.

            For example, you used git add * to stage the Files, but there is a test.txt file you want to remove from staging Area/index
                > git reset HEAD test.txt
            So, the file test.txt is never committed. So HEAD doesn't have it. So reset to HEAD will remove the file from staging area.
            But what if the file is already committed and you want to reset it. Discussed next
            
    - Undoing Changes After Commit
        Amend: What if you made a commit. The commit message has typo or is incomplete. Or The commit message doesn't reflect the 
        changes made in commit in such cases you want to amend a commit. Amend removes the latest commit with the new one. That's
        why you should never amend a public commit. It should only be used in local repo.
            > git commit --amend
        
        For example,
        You made few changes in two files - index.html and sidebar.js. Then you add index.html and commit it saying "Add sidebar ta Homepage".
        Notice, you forgot to add sidebar.js to the commit. Also, the message is short and has a typo.
        In such case we can make a new commit using --amend flag which will update the last commit with the new one. 
        For the new commit, first add sidebar.js to Index, then 
            > git commit --amend
        Excluding -m will let you add descriptive commit from a text editor.

    - Rollback (Revert the latest commit) : What if you made a public commit and it introduce errors. Now, you cannot fix the errors and amend commit
        as it will modify the commit history and for public repo, we want out commit history to be consistent.
        In such, case we can Revert to rollback to previous state but the commit history will be intact.
        Git revert doesn't just mean undo. Instead, it creates a commit that contains the inverse of all the changes made in
        the bad commit in order to cancel them out. For example, if a particular line was added in the bad commit, then in the 
        reverted commit, the same line will be deleted. This way you get the effect of having undone the changes, but the history 
        of the commits in the project remains consistent leaving a record of exactly what happened.
            So git revert will create a new commit, that is the opposite of everything in the given commit. We can revert the latest 
        commit by using the HEAD alias. Since HEAD points to your current commit, when we pass it to the revert command we tell Git
        to rewind that current commit. 
        
            > git revert HEAD
        
        So once we issue that git revert command, we're presented with the text editor commit interface. 
        The first-line mentions that it's reverting the commit, it's usually a good idea to add an explanation of why we're doing the 
        rollback.
        
        Now, we can see both the bad commit and the reverted commit in the log.
            > git log -p -2 // get the latest two commits with patch info
        
        So in the log, you will see that, git created a new commit that's the inverse of the previous bad one.
        The bad commit is reverted and the error stopped.
        In this example, we reverted the latest commit in our tree. But what if we had to revert a commit that was done before that? 

    - Rollback (Revert past commit): Rollback to any past commit using commit id:
        First what is commit id: They are generated using SHA1 algo.
        They provide the consistency that is critical for distributed systems such as Git.
        They are created using the commit message, date, author, and the snapshot taken of the working tree.

            > git revert commit_id 
        
        We can use first 5-8 characters of commit id rather that using entire hash. Also, tags can be used.
        The above command will reset the changes made in the named commit and add a new commit. 


- git-checkout - Switch branches or restore working tree files
    > git checkout -b <new_branch> <startpoint>
      Where, <startpoint> is The name of a commit at which to start the new branch. Defaults to HEAD.
    We can also checkout to particular commit using commit id

- Branches
    A branch at the most basic level is just a pointer to a particular commit. But more importantly, it represents
    an independent line of development in a project. Branches make it really easy to experiment with new ideas or 
    strategies and projects. When you want to add a feature or fix something, you can create a new branch
    and do your development there.
        You can merge back into the master branch, when you've got something you like, or discard your changes without
    negative impact if they don't work out.  
    
    git-branch - List, create, or delete branches
        - Create a branch and checkout to it
            > git branch [branch_name]
            > git checkout [branch_name]
    
                        OR
    
            > git checkout -b [branch_name]

        - Delete branch 
            > git branch -d [branch_name]

            Use -D flag to force delete

        - Rename branch
            > git branch -m [old_branch_name] [new_branch_name]

            Use -M flag to force Move/Rename

        - List branch
            - List local branches: > git branch
            - List remote and local branches: > git branch -a
    
    - Merge: 
        > git checkout master
        > git merge [new_branch_name]
        On Merge both the branches are pointed at the same commit.
    
    - Merge Conflict
        Git uses two different algorithms to perform a merge, fast-forward and three-way merge.
        
        1. fast-forward merge is performed when the commit history of both branches doesn't diverge.
        In these cases, all Git has to do is update the pointers of the branches to
        the same commit, and no actual merging needs to take place.

        2. On the other hand, a three-way merge is performed when the history of the merging
        branches has diverged in some way, and there isn't a nice linear path to combine them via fast-forwarding.
        This happens when a commit is made on one branch after the point when both branches split.
        For example, this could have happened if we made a commit on the master branch
        after creating the other branches. When this occurs, Git will tie the branch histories together with a new commit.
        And merge the snapshots at the two branch tips with the most recent common ancestor, the commit before the divergence.
        To do this successfully, Git tries to figure out how to combine both snapshots. If the changes were made in different 
        files, or in different parts of the same file, Git will take both changes and put them together in the result.
        If instead the changes are made on the same part of the same file, Git won't know how to merge those changes, 
        and the attempt will result in a merge conflict.

        To resolve conflict: Open the file where conflict has occurred, Decide who's version to keep, you can keep both or one, 
        Stage and Commit. 

         
    


