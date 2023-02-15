# GIT 

To Do's:
    - Structure the Notes
    - Add Diagrams for Revert, Reset
    - Add table for Reset- soft, mix and hard

### Open source license:

1. Contributor License Agreement (CLA) - It requires contributors to sign an agreement. It's a one time thing.
2. Developer Certificate of Origin (DCO) - It was introduced by Linux foundation in 2004. It's light weight.
But it's recurring. Every commit must be signed-off with '-s' option which specifies the developer name: 
"developer name <deloper@dev.com>"

- Help: 
    git help [command]  
    ```
    git help commit
    ```
    
- View git version: 
 ```
    git -v |--version
```

- Master vs Main: Many hosting system now have renamed the master branch to main.
So when you create a local repo, rename master to main OR just ignore master & create a new branch main and start
working from the main branch:
    - Rename master to main: git branch -m main
    - Create new main branch: git checkout -b main

- Basic Git Workflow:

    ```
    $ mkdir git-test
    $ cd git-test
    $ git init
    ```
    
    // Let's tell git who is responsible for this repository. This needs to be set for each new repo unless you have set
    name & email globally
    ```
    $ git config user.name "Another Genius" 
    $ git config user.email "a_genius@linux.com"
    ```

    // Start working
    ```
    $ echo some junk > somejunkfile // create a file
    $ git add somejunkfile // add file to staging area
    $ git status // watch status
    ```
    
    // watch diff
    ```
    $ echo another line >> somejunkfile
    $ git diff
    ```

    // To actually commit the changes to the repository, we do:
    ```
    $ git add somejunkfile
    $ git commit -m "My initial commit"
    ```
    // Signing Off on Commits to show who is responsible for the changes:
    ```
    $ git commit -s -m "My initial commit" 
    ```
    
    // View commit history
    ```
    $ git log
    ```

- Upstream & Downstream
The parent repository is often considered upstream and the repository you are working on, at one point cloned from the parent,
 is often considered downstream.
Conceptually, any repository to which you send changes is considered upstream; any repository which is based on yours is 
considered downstream.

- File Types:
Git distinguishes between three types of files: tracked, ignored, and untracked, with only the tracked ones residing in the repository.

    - Tracked files: They are already in the repository in their current working state, or have been staged, i.e. changed but not yet committed.

    - Ignored files: Each directory may contain a file named .gitignore which lists either specific files or name patterns which are to be ignored. 
    For instance, all temporary files could be ignored with a specification like *.temp. It is also possible to override the rules 
    by prefixing with !. For example, if your gitignore file includes:
        ```
        *.temp
        !my_driver.temp
        ```
        The second specification overrides the first, more general one, and the file my_driver.temp will be tracked.

    - Untracked files: Files which are neither added to staging area or added to .gitignore.


- Basic File Commands:
    
    - git add
    It can be used either to add new files or stage changed ones. You must add files to staging area before commit.
    There are a number of options in add (see git help add). For instance, you can use -i for interactive choosing of files to stage, 
    or -u to update only files already known to Git. You can also specify wildcard patterns or directory names to add.

    - git rm
    Removes a file from the working tree and the index, but does not remove it from the repository; that only happens when you make 
    a new commit. If you only want to remove the file from the working directory, and not the repository index, just use the normal rm command. 
    While you remove files from the repository, you do not remove them from the history. If you want to remove a file that has been staged but 
    not committed, you have to add the --cached option as in:
    
        $ git add myfile
        $ git rm myfile --cached
    
    
    - `git mv` Renames a file and stages the new filename in the repository. It is equivalent to renaming the working file and then doing a git rm on 
    the old file name and a git add on the new one, i.e. the following operations are equivalent, look at the commands below:
    
        $ git mv oldfile newfile
        $ mv oldfile newfile ; git rm oldfile ; git add newfile

    - `git ls-files` Shows information about files in the index and working tree. By default, this command shows only files in the repository. If you want to show the untracked files, follow the command below where the --others option shows the untracked files, and the --exclude-standard option says to ignore standard exclusions such as .gitignore files.

        $ git ls-files --others --exclude-standard


- Commit
    Let's say you have modified a number of files (i.e. they are staged), but you only want to commit the changes to one file:

        $ git commit -s file1
    
    If you want to commit all changes, any of these forms will do it:
    
        $ git commit -s
        $ git commit ./ -s
        $ git commit -a -s

    - Difference
        Show all differences between your staged working directories and what has been previously committed. After you do the commit,
        it will show nothing differing.
    
            $ git diff
    
    - Bash Script to create a repo and make commits:

        ```
        #!/bin/bash

        mkdir git-test

        cd git-test
        git init

        git config user.name "A Smart Guy"
        git config user.email "asmartguy@linux.com"

        echo file1 > file1
        git add file1
        git commit -s -m "This is the first commit"

        echo file2 > file2
        git add file2
        git commit . -s -m "This is the second commit"

        echo file3 > file3
        echo another line for file3 >> file3
        git add .
        git commit . -s -m "This is the third commit"

        echo another line for file2 >> file2
        git add .
        git commit -a -s -m "This is the fourth commit"

        ```
   
        Execute the bash file and then log to view commit:
            
            $ git log
    
        Also, we can view short version of log:
        
            $ git log --pretty=oneline
        
    
    - Tagging: 
        Commits are named using long hash string which are hard to type. We can use tagging to associate a human readable name
        to commits
            
        ```

            git tag <name> <commit_hash>     
            git tag commit10 6546sdfserf5er6ere6er65er5er5erhft

        ```
            
        To view all the tags: `git tag`
    
    
    - Reverting and Resetting Commits
        From time to time, you may realize that you have committed changes unwisely. 
        Either you may have made changes you never should have, or you committed prematurely. 
        
        - Revert: In case, you made some changes that you never should have, and now you want to revert the working directory to some past commit, 
            use 'revert' command. 
            No previous commit will be removed. Revert adds a new commit, sets HEAD to it, and updates the working 
            directory to reflect reversion. Any uncommitted changes in the working directory will be discarded.

                $ git revert commit_name

            where commit_name can be specified in a number of ways:
                HEAD: most recent commit
                HEAD~: previous commit (the parent of HEAD)
                HEAD~~ or HEAD~2: the grandparent commit of HEAD
                {hash number}: specific commit by full or partial sha1 hash number
                {tag name}: a name for a commit.

        - Reset: 
            In case you want to remove previous prematurely made commits, use 'reset' command, this will not change the working directory
            but will remove the commit only. Any uncommitted changes in the working directory will be discarded. 
            
            
            ```
            $ git reset HEAD~2 // will remove the first two commits and will set the HEAD to 3rd commit
            ```

            - Options: 
                
                --soft: just moves the current branch to prior commit (index unchanged in this case)
                --mixed (default): also updates the index to match new head (un-stages everything)
                --hard: same as --mixed, but also updates working directory to match new head (un-edits your files).
    
            Suppose you have been furiously coding and realize that your last three commits are still a work in progress, but 
            everything before that should be made available to others. Then, you should create a new working branch while resetting 
            the main branch back three commits as in:
            
            ```
                $ git branch work // copy main branch progress to work branch
                $ git reset --hard HEAD~3 // remove first 3 commits
                $ git checkout work // checkout to work where you have all the commits including first 3 commits
            ```
            
            which restores the main branch to its previous state, while leaving the speculative work in work, where you will continue to play. 
          
    
    - Compressing Repository
        As your project grows through a series of commits, your repository may grow large in size. You can optimize and compact your 
        repository using 'gc' where gc stands for garbage collection. 

        - First check the repository size:
        
            $ du -shc .git
    
        - Then issue following command to compact it:
            
            $ git gc

        - Recheck the repository size to see the change in size:
        
            $ du -shc .git

        You can also check your repository for certain kinds of errors with the command git fsck.

    
    - Blame
        It is possible to assign blame for whom is responsible for a given set of lines in a file. For example:

            $ git blame file2

        Shows the responsible commit and author. It is possible to specify a range of lines and other parameters for the search.

            $ git blame -L <start line no.>,<end line no.> <file>

        For example, for a more complicated file in the Linux kernel source:
        
            $ git blame -L 3107,3121 kernel/sched/core.c​

    
    - Bisect
        Suppose you had a version of your code that worked, and now you are many versions (and commits) later and you have found out 
        that it is no longer working.
        Git has the ability to bisect in order to rapidly find the change set that screwed things up. The number of steps is no more than 
        the logarithm to the base 2 of the number of commits, which is much faster than a brute force approach. In other words, if a bad 
        change has been done somewhere in the last 1024 commits, you can find it in no more than 10 bisection steps.

        First, you need to do:
        
            $ git bisect start
            $ git bisect bad
            $ git bisect good V_10
        
        where it is assumed that the current commit is bad and version V_10 is known to be good. Git will then leave you at a commit halfway 
        in between. You then test the code to see if the bug is still there.
        
        If it is, you type:
        
            $ git bisect bad
        
        If the code does not have the bug yet, you type:
        
            $ git bisect good
        
        You continue this iteratively until you find the bug.
        
        Then you type:
        
            $ git bisect reset
        
        to get back to your current working state.
        

- Branch
    - Create branch: $ git branch [branch_name]
    - Checkout/Switch branch: $ git checkout [branch_name] // any files that have been changed will have their contents changed to reflect it
    - We can create & checkout to the created branch using single command: $ git checkout -b [branch_name]
    - View all branches: $ git show-branch OR $ git branch
    - Delete a branch: $ git branch -d [branch_name]
    - Rename branch: $ git branch -M [branch_name]
    
- Getting earlier file version:
    Suppose you want to see an earlier version of a particular file. You can do this with git show if you specify a path name in
    addition to a tag as in (note the colon):

        $ git show v2.4.1:src/myfile.c
    
    If you actually want to restore that version you can do it with (no colon):
    
        $ git checkout v2.4.1 src/myfile.c

- File Difference:
    UXIX shell provides a command to view difference between two files and folders (recursively)

        $ diff file1 file2

    Use -u option for unified diff, it shows the diff. in single file that makes it easier to compare the difference between two files:
        
        $ diff -u file1 file2

    When comparing two directory trees the form used is often:

        $ diff -Nur directory1 directory2

    where the -r option forces a recursive descent into the trees, and the -N option forces files which have been added or deleted to appear 
    in the differencing, instead of just generating a warning that a file is in only one directory tree.

- File Difference in GIT:
    
    - $ git diff // shows the differences between the current working version of your project and the last commit.

    - $ git diff earlier_commit // shows the differences between your current working version and the earlier commit specified by earlier_commit. 
    This may often be specified as a branch name.

    - $ git diff --cached earlier_commit // shows the differences between the staged changes in the index and the commit. 
       In Git versions from 1.6.1 on, you can say --staged instead of --cached which might be more intuitive.

    - $ git diff one_commit another_commit // shows the differences between two commits.
        Options:
         --ignore-all-space // ignore white space differences
        --stat or --numstat // generate brief statistics.

    ​- It is also possible to limit the scope of the diff to a particular part of the directory tree. 
    For example, if you are in the Linux kernel Git repository below command will show only the changes in the Documentation/vm subdirectory:

        $ git diff v4.2.1 v4.2.2 Documentation/vm
    
    - View diff. between two branches: 

        git diff main dev
    

- Merge
    - Merging the dev branch into the current main branch is as simple as doing:

        $ git checkout main // if you are already not at main
        $ git merge dev

    - Merge Conflict
        Git tries to auto-merge the branches but in some cases conflict may happen. In such case, there are two basic approaches you can 
        take to fixing the problems:

        1.Revert the merge - If you have made a mess of things with a premature or accidental merge, it is easy to revert back to where 
        you were with:

            $ git reset --hard main

        2.Resolve the conflict
            - View conflict: $ cat file_name OR open an editor
            - Manually edit files to resolve the conflict
            - Add files to Staging Area
            - Commit

- Rebase
    Suppose you are working on dev branch but the main branch got updated while you are working on dev. And you want the updates of 
    main in dev, in such case you can simply rebase to get all the new changes of main branch in dev branch:
        
        $ git checkout dev
        $ git rebase main dev
    

    To give a concrete common example, suppose you are working on a new feature for the Linux kernel and you began working when 
    the kernel release status was version 4.16. While you are happily coding away, the mainline kernel continues to evolve and version 4.17 
    is released. If you do a rebase, your changes and your patch set are rewritten to apply to the 4.17 code rather than the
    4.16 code, a hopefully simpler situation to deal with in the future. 
    
    All the commits on dev branch will be removed and main branch commit will be added to dev and your work will be updated.
    Obviously, conflicts may emerge and if any are found you will be asked to resolve them as you did when you were merging. 
    As you fix the conflicts, you will have to do git add to update the index, and when you are done fixing conflicts, instead of 
    doing a commit you do:

        $ git rebase --continue

    If things get disastrous somewhere along, then you can revert back to where you were before the attempted rebase with:

        $ git rebase --abort 


- Remote
    - Clone a remote repo to local system
        
        $ git clone git://git.kernel.org/pub/scm/git/git.git
    
        Note the use of the git:// protocol. It is the preferred method, but not the only one that can be used. Other possibilities are:
 
        file:///path/to/repo.git
        ssh://user@remotesite.org[:port]/path/to/repo.git
        user@remotesite.org:/path/to/repo.git
        ht‌tp://remotesite.org/path/to/repo.git
        ht‌tps://remotesite.org/path/to/repo.git
        rsync://remotesite.org/path/to/repo.git

        The git:// method is the fastest and cleanest and should be used whenever it is supported.

    - View repo refrence (content)
        
            $ git show-ref

        To see what is in the remote repository, do:

            $ git ls-remote git://git.kernel.org/pub/scm/git/git.git

        if you notice some additional references in the remote repository which are not reflected in the clone, to sync local with remote
        simply do:

            $ git fetch 
            $ git merge origin/master
                
                    OR

            $ git pull origin main
            
        and if you have the main branch already checked out, you can simply do:

            $ git pull
