# vim, git, etc.

## Common workflows with git

* [Use git to manage and backup your work](#use-git-to-manage-and-backup-your-work)
* [Accept someone else's edits to your code](#accept-someone-elses-edits-to-your-code)
* **Pull Requests**
  * [You cannot push your code to others](#you-cannot-push-your-code-to-others-as-a-contributor)
  * [Ask to have your code edits accepted with a pull request (PR)](#ask-to-have-your-code-edits-accepted-with-a-pull-request)

___
### Use git to manage and backup your work
![git daily workflow](/doc/images/git_clone_commit_push.png)

___
### Accept someone else's edits to your code
![PR? and merge](/doc/images/git_pull.png)

___
### Ask somebody to accept your edits to their code
#### You cannot push your code to others (as a contributor)
![No pushing!](/doc/images/Git_push_pull_fork_clone_bad.png)
___
#### Ask to have your code edits accepted with a pull request
![](/doc/images/Git_push_pull_fork_clone.png)


## vim
* `:ls` see the list of current buffers
* `:reg` see the current contents of your registers

### [Placing current line at top/center/bottom of screen in vim](https://unix.stackexchange.com/questions/110251/how-to-put-current-line-at-top-center-bottom-of-screen-in-vim)
:help scroll-cursor    
:set scrolloff?    
:set so?    

keystroke             | description
----------------------|--------------
z[enter]              | puts current line to top of screen
zt                    | puts current line to top of screen, but leave cursor in same col
z.                    | puts current line to center of screen
zz                    | puts current line to center of screen, but leave cursor in same col
z-                    | puts current line to bottom of screen
zb                    | puts current line to bottom of screen, but leave cursor in same col
<line number>z<t|z|b> | puts <line number> at top, center, or bottom

## Games
* https://vim-adventures

## Links
* [Learn vim script the hard way](https://learnvimscriptthehardway.stevelosh.com/chapters/19.html)

## git
* `git commit --amend -m 'Replaces last commit msg'

## Pull Requests (PR)
https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/checking-out-pull-requests-locally
```
git fetch origin pull/$PRID/head:$BRANCHNAME  # BRANCHNAME is new branch that you want to create
git fetch origin pull/13/head:PR13

# Get the filenames of new files from PR (leave out the deleted files)
git --no-pager diff --diff-filter=D --name-only FETCH_HEAD $$(git merge-base FETCH_HEAD main)
```

### Find deleted files
'''
$ git log --diff-filter=D --summary --reverse | grep delete
$ git log --summary --reverse -- src/bin/bash_text_colors.py
$ git show [hash] -- src/bin/bash_text_colors.py | tee bash_text_colors.py
$ git checkout [hash]~1 -- src/bin/bash_text_colors.py
'''

### [Remotes](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories)
* https://stackoverflow.com/questions/14290113/git-pushing-code-to-two-remotes
'''
$ git remote -v
$ git remote add dampierlab [ssh]
$ git push dampierlab main
$ git push dampierlab 
$ git remote add both [ssh]
$ git remote set-url --push both [http]
'''

```
$ git config --list
$ git config user.name
$ git config user.email
$ git config --global user.name <user_name>
$ git config --local user.name <user_name>
```


### Branches
```
$ git branch -d <branch_name>  # Delete local branch if it has been fully merged
$ git branch -D <branch_name>  # Delete local branch irrespective of its merged status
$ git push <remote_name> --delete <branch_name>  # or
$ git push -d <remote_name> <branch_name>
```

## bash
### args
```
!^      first argument
!$      last argument
!*      all arguments
!:2     second argument

!:2-3   second to third arguments
!:2-$   second to last arguments
!:2*    second to last arguments
!:2-    second to next to last arguments

!:0     the command
!!      repeat the previous line
```

## git
### How can I print a plain list of all files that were part of a given commit?
* git diff-tree --no-commit-id --name-only -r bd61ad98 # Preferred (plumbing command) programmatic
* git diff-tree --no-commit-id --name-only -r bd61ad98 # Porcelain; user facing

### List files tracked by git
* git ls-files # List files tracked by git
* git ls-files --other # List files NOT tracked by git
* git diff --name-only --diff-filter=U  # Show Unmerged files (--relative to show paths from cwd)
* git diff --check     # show the list of files containing conflict markers including line numbers.
* git diff --name-only --diff-filter=u  # Show modified, unstaged files, and only the filenames
* git diff --name-only --diff-filter=u --cached # Show modified, staged/cached files, and only the filenames
* git diff --name-only --diff-filter=AM HEAD  # list 'git status -s' filenames only


## awk
gene_result.txt is from NCBI Gene search: (HIV) AND 9606[Taxonomy ID]    
("Human immunodeficiency virus 1"[Organism] OR "Human immunodeficiency virus 2"[Organism] OR "Simian-Human immunodeficiency virus"[Organism] OR HIV[All Fields]) AND 9606[Taxonomy ID] AND ("genetype protein coding"[Properties] AND alive[prop])    
* awk -F '\t' '{printf "%15-s %s\n", $6, $8}' gene_result.txt   # Print Gene Symbol and Description
