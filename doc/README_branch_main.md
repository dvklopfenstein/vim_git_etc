# How to replace branch, master, with main

* [1. Locally, create a new branch called "**main**"](#1-locally-create-a-new-branch-called-main)
* [2. Push the new "**main**" branch to the remote repo](#2-push-the-new-main-branch-to-the-remote-repo)
* [3. On the gogs web page, switch the default branch to "**main**"](#3-on-the-gogs-web-page-switch-the-default-branch-to-main)
* [4. Delete branch "**master**" from the remote repo on gogs](#4-delete-branch-master-from-the-remote-repo-on-gogs)
* [5. Delete branch "**master**", from your local repo](#5-delete-branch-master-from-your-local-repo)


## Quick notes
```
$ git checkout -b main
$ git push --set-upstream origin main
$ git push --delete origin master
$ git branch -d master
```

## 1. Locally, create a new branch called "main"
```
# Create new branch 'main' and switch to it
$ git checkout -b main
Switched to a new branch 'main'

$ git branch
* main
  master
```

## 2. Push the new "main" branch to the remote repo
The remote repo is on the [gogs web page](http://10.11.19.24:3080/)
```
# You may be asked for more info before pushing the new main branch
$ git config --global user.email "me123@drexel.edu"
$ git config --global user.name "DV Klopfenstein, PhD"
$ git config --global init.defaultBranch main
```

```
# Your remote_name (as opposed to your repo local copy) is likely origin
$ git push --set-upstream origin main
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```
## 3. On the [gogs web page](http://10.11.19.24:3080/), switch the default branch to "main"
GitHub and gogs have a default branch, git does not, so travel to your gogs repo:    

http://10.11.19.24:3080/{login_name}/{repo}/    

* On the repo page, click "Settings"
* On the Settings page, under the Settings Menu header on the left, click "Branches"
* On the "Default Branch" panel, click the pull-down menu to switch your branch to "main"

## 4. Delete branch "master" from the remote repo on gogs
The name of your remote repo on gogs is likely "origin"
```
$ git push --delete origin master
 - [deleted]         master
```

## 5. Delete branch "master", from your local repo
```
$ git branch
* main
  master

$ git branch -d master
Deleted branch master (was 2504065).

$ git branch
* main
```

Copyright (C) 2022-present, DV Klopfenstein, PhD. All rights reserved.
