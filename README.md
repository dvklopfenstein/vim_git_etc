# vim, git, etc.

## Common workflows with git

* [Use git to manage and backup your work](#use-git-to-manage-and-backup-your-work)
* [Accept someone else's edits to your code](#accept-someone-elses-edits-to-your-code)
* **Pull Requests**
  * [You cannot push your code to others](#you-cannot-push-your-code-to-others-as-a-contributor)
  * [Ask to have your code edits accepted using a pull request (PR)](#ask-to-have-your-code-edits-accepted-using-a-pull-request)

___
### Use git to manage and backup your work
![git daily workflow](/doc/images/git_clone_commit_push.png)

___
### Accept someone else's (dvklopfenstein's) edits to your (raefcon's) code
`git pull` is 'git fetch` then `git merge'
![PR? and merge](/doc/images/git_pull.png)

___
### Ask somebody (dvklopfenstein) to accept your (scbarrera) edits to their code
#### You cannot push your code to others (as a contributor)
![No pushing!](/doc/images/Git_push_pull_fork_clone_bad.png)
___
#### Ask (dvklopfenstein) to have your (scbarrera) code edits accepted using a pull request
![](/doc/images/Git_push_pull_fork_clone.png)


## vim
* `:ls` see the list of current buffers
* `:reg` see the current contents of your registers
* `:global/pat/normal O/insert
*      `:g/pat/norm Oinserttxt
* `gUiw` # global UPPERCASE inner(for entire word no matter cursor) word

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

### Character based motions on the current line
* `3fa` move forward to the third occurrence of character `a`
* `ta` move forward to the character just before `a`
* `3tx` move forward to the character just before the third occurrence of character `x`
* `Fa` move backward to the character `a`
* `Ta` move backward to the character just after `a`
* `;` repeat previous `f` or `F` or `t` or `T` motion in the same direction
* `,` repeat previous `f` or `F` or `t` or `T` motion in the opposite direction

### Insert a line above a line that matches a pattern
```
:g/^def /norm O# some_comment<CR>
or in sed
$ sed -i '/^def /i # some_comment' filename.py
```

# gpg

## Checking GCC download
0. https://ftp.gnu.org/gnu/gcc/gcc-13.2.0/  # Download latest compiler
1. gpg gcc-13.2.0.tar.gz.sig  # Get public key name (01234578)
2. gpg --keyserver hkps://keyserver.ubuntu.com --recv-keys 01234567  # Download public key
3. gpg gcc-13.2.0.tar.gz.sig  # Look for "Good signature" this validates the download


## Games
* https://vim-adventures

## Links
* [Learn vim script the hard way](https://learnvimscriptthehardway.stevelosh.com/chapters/19.html)

## git
* `git commit --amend -m 'Replaces last commit msg'
* [git merge fast-forward vs git rebase](https://stackoverflow.com/questions/70627750/git-merge-fast-forward-vs-git-rebase)
* [Resolving a merge conflict using the command line](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line)

### [Undo a commit & redo](https://stackoverflow.com/questions/927358/how-do-i-undo-the-most-recent-local-commits-in-git)
```
$ git commit -m "Something terribly misguided" # (0: Your Accident)
$ git reset HEAD~                              # undo commit. LEAVE FILES ALONE AS IS. Will need to redo 'git add'
[ edit files as necessary ]                    # 
$ git add .                                    # Need to redo 'git add'
$ git commit -c ORIG_HEAD                      # Commit changes, reusing old commit msg OR
$ git --amend -m 'New commit msg'              # Commit changes, using new commit msg
```

### Show repo's toplevel dir; show git dir
```
$ git rev-parse --show-toplevel
$ git rev-parse --git-dir
```

## Pull Requests (PR)
https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/checking-out-pull-requests-locally
```
git fetch origin pull/$PRID/head:$BRANCHNAME  # BRANCHNAME is new branch that you want to create
git fetch origin pull/$PRID/head:$BRANCHNAME --update-head-ok  # if fatal: refusing to fetch into branch 'refs/heads/main' checked out at ...
git fetch origin pull/13/head:PR13

# Get the filenames of new files from PR (leave out the deleted files)
git --no-pager diff --diff-filter=D --name-only FETCH_HEAD $$(git merge-base FETCH_HEAD main)
```

### Find deleted files
```
$ git log --diff-filter=D --summary --reverse | grep delete
$ git log --summary --reverse -- src/bin/bash_text_colors.py
$ git show [hash] -- src/bin/bash_text_colors.py | tee bash_text_colors.py
$ git checkout [hash]~1 -- src/bin/bash_text_colors.py
```

### git show
```
$ git show HEX:filename
```
* https://stackoverflow.com/questions/424071/how-do-i-list-all-the-files-in-a-commit
```
$ git diff-tree --no-commit-id --name-only HEX -r # List all the files in a commit (plumbing)
$ git show --pretty="" --name-only HEX            # List all the files in a commit (porcelain)
```

### git log
####See things missing in main that are on dvk_git
Try to delete branch, dvk_git, while on branch main. But dvk_git has commits main does not.
See a graph using `git log` of what you are missing...
```
$ git branch
  dvk_git
* main

$ git log --graph --left-right --cherry-pick --oneline main...dvk_git
< 3b19970 (HEAD -> main) Add copyright & clean up makefile
> 36e20e4 (origin/dvk_git, dvk_git) Added forks
>   d7ece74 (upstream/main) Merge branch 'dvk_git' of dvklopfenstein/OMICS_dev into main
|\
| > 6ce87e7 Add make target for adding upstream remote (source repo)
| > ae2b839 Add links to Instructor git flow
> fcc49d5 Merge branch 'main' of dvklopfenstein/OMICS_dev into main

```

#### Make a branch tree visual
```
$ git log --all --graph --decorate --oneline --simplify-by-decoration
```

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

### [git pull](https://stackoverflow.com/questions/71768999/how-to-merge-when-you-get-error-hint-you-have-divergent-branches-and-need-to-s)
https://git-scm.com/book/en/v2/Git-Branching-Rebasing
```
$ git pull
  git config pull.rebase false  # merge             $ git pull --no-rebase
  git config pull.rebase true   # rebase            $ git pull --rebase
  git config pull.ff only       # fast-forward only $ git pull --ff-only
```

### [Sync a forked origin to upstream](https://stackoverflow.com/questions/7244321/how-do-i-update-or-sync-a-forked-repository-on-github)
```
$ git remote -v
$ git remote add upstream https://github.com/whoever/repo.git
$ git fetch upstream main
$ git checkout main
$ git merge upstream/main

### Create a new repository on the command line
```
touch README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/OMICS_dev.git
git push -u origin main
```

### Backup onto a local repo
```
# Create a [bare repo](https://www.saintsjd.com/2011/01/what-is-a-bare-git-repository/), which is optimized for sharing and has no working dir
$ git init --bare ~/backup/myproject.git
$ cd /path/to/existing/repo
$ git remote add origin ~/backup/myproject.git
$ git push origin main
$ git clone ~/backup/myproject.git
```

### Push an existing repository from the command line

```
git remote add origin http://github.com/OMICS_dev.git
git push -u origin main
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
* git checkout $(git ls-files -m)
* git ls-files # List files tracked by git
* git ls-files --other # List files NOT tracked by git
* git diff --name-only --diff-filter=U  # Show Unmerged files (--relative to show paths from cwd)
* git diff --check     # show the list of files containing conflict markers including line numbers.
* git diff --name-only --diff-filter=u  # Show modified, unstaged files, and only the filenames
* git diff --name-only --diff-filter=u --cached # Show modified, staged/cached files, and only the filenames
* git diff --name-only --diff-filter=AM HEAD  # list 'git status -s' filenames only

### color diff
* git diff --color-words README.md
* git diff --color-words old.txt new.txt

### If default branch on GitHub is renamed (master->main), do this on your local clone to update:
git branch -m master main
git fetch origin
git branch -u origin/main main
git remote set-head origin -a

## git plumbing
description  # Only used by GitWeb program
HEAD         # ref: refs/heads/main        Points to current branch
config
objects/     # All repo content
objects/info # All repo content
objects/pack # All repo content
refs/        # Stores pointers to commint objects (branches, tags, remotes, ...)
info/
hooks/

$ git ls-files    # Show .git/index: a sorted list of path names w/permissions and SHA1 of blob
$ git cat-file -p 4b825dc642cb6eb9a060e54bf8d69288fbee4904
$ git cat-file -s 4b825dc642cb6eb9a060e54bf8d69288fbee4904
$ git cat-file -t 4b825dc642cb6eb9a060e54bf8d69288fbee4904
$ git count-objects -v
$ git log --pretty=oneline
$ git reflog
$ git log -g
$ git gc --auto
$ git fsck --full


## git and Jupter notebooks
* http://timstaley.co.uk/posts/making-git-and-jupyter-notebooks-play-nice/ nbconvert_jq
* https://www.reviewnb.com/git-jupyter-notebook-ultimate-guide

## grep
* grep -B 10 -A 5 build README.md  # report 10 lines before and 5 lines after lines containing build
* grep -C 5 build README.md        # report  5 lines before and after lines containing build

## Bash cursor
* ctrl-a Go to beginning of line
* ctrl-e Go to end of line

## awk
gene_result.txt is from NCBI Gene search: (HIV) AND 9606[Taxonomy ID]    
("Human immunodeficiency virus 1"[Organism] OR "Human immunodeficiency virus 2"[Organism] OR "Simian-Human immunodeficiency virus"[Organism] OR HIV[All Fields]) AND 9606[Taxonomy ID] AND ("genetype protein coding"[Properties] AND alive[prop])    
* awk -F '\t' '{printf "%15-s %s\n", $6, $8}' gene_result.txt   # Print Gene Symbol and Description
* awk -F"\t" '{print $1, $2, $3, $4, $5}' notebooks/goea_0.05_*_proteincoding_partof_sig_goids.txt
* cut -f1-5 notebooks/goea_0.05_*_proteincoding_partof_sig_goids.txt

* awk '{print NR-1 "," $0}' README.md                    # print lines w/lnum prefixed (NR starts at 1)
* awk '3288<=NR && NR<=3291 {print NR-1 ": " $0}' *.sam  # print specific line numbers
* awk '3288<=NR && NR<=3291' *.sam                       # print specific line numbers
* sed -n '3288,3291p' *.sam

## find
* find ~+ -type d   # Use bash's Tilde Expansion to get the absolute path of the surrent working directory
* find . -name notebooks -exec find {} -name \*.py \;

