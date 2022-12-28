# vim, git, etc.
* [vim](#vim)
  * [Place current line elsewhere](#placing-current-line-at-topcenterbottom-of-screen-in-vim)
* [git](#git)
  * [Find deleted files](#find-deleted-files)

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

```
$ git branch -d <branch_name>
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
* git diff --name-only --diff-filter=u  # Show modified, unstaged files, and only the filenames
* git diff --name-only --diff-filter=u --cached # Show modified, staged/cached files, and only the filenames

* git diff --name-only --diff-filter=AM HEAD  # list 'git status -s' filenames only


## awk
gene_result.txt is from NCBI Gene search: (HIV) AND 9606[Taxonomy ID]    
("Human immunodeficiency virus 1"[Organism] OR "Human immunodeficiency virus 2"[Organism] OR "Simian-Human immunodeficiency virus"[Organism] OR HIV[All Fields]) AND 9606[Taxonomy ID] AND ("genetype protein coding"[Properties] AND alive[prop])    
* awk -F '\t' '{printf "%15-s %s\n", $6, $8}' gene_result.txt   # Print Gene Symbol and Description
