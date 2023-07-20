# Git

* git diff --name-status main..dvk    # List files that are different in the branches

## Fixing a conflict manually

$ git fetch upstream main
$ git merge upstream/main
$ vim -p doc/README_week01.md
$ git rm LINKS_SLIDES_etc.md
$ git commit -a -m 'rm conflict in doc/README_week01.md & rm new file'
$ git push origin BRANCHNAME


```
# --------------------------------------------------------------------------------
$ git fetch upstream main
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (4/4), 945 bytes | 189.00 KiB/s, done.
From http://10.11.19.24:3080/courses/OMICS_dev
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> upstream/main

# --------------------------------------------------------------------------------
$ git remote -v
origin 	http://10.11.19.24:3080/dvklopfenstein/OMICS_dev.git (fetch)
origin 	http://10.11.19.24:3080/dvklopfenstein/OMICS_dev.git (push)
upstream       	http://10.11.19.24:3080/courses/OMICS_dev.git (fetch)
upstream       	http://10.11.19.24:3080/courses/OMICS_dev.git (push)

# --------------------------------------------------------------------------------
$ git merge upstream/main
Auto-merging doc/README_week01.md
CONFLICT (content): Merge conflict in doc/README_week01.md
Automatic merge failed; fix conflicts and then commit the result.

# --------------------------------------------------------------------------------
$ vim -p doc/README_week01.md

# --------------------------------------------------------------------------------
git status -uno
On branch main
Your branch is up to date with 'origin/main'.

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Changes to be committed:
       	new file:   LINKS_SLIDES_etc.md
       	modified:   MEETING_NOTES.md

Unmerged paths:
  (use "git add <file>..." to mark resolution)
       	both modified:   doc/README_week01.md

# --------------------------------------------------------------------------------
$ rm LINKS_SLIDES_etc.md
$  git rm LINKS_SLIDES_etc.md
rm 'LINKS_SLIDES_etc.md'

# --------------------------------------------------------------------------------
$ git status
On branch main
Your branch is up to date with 'origin/main'.

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Changes to be committed:
       	modified:   MEETING_NOTES.md

Unmerged paths:
  (use "git add <file>..." to mark resolution)
       	both modified:   doc/README_week01.md

# --------------------------------------------------------------------------------
$ git commit -a -m 'rm conflict in doc/README_week01.md'
[main 7cbef13] rm conflict in doc/README_week01.md

# --------------------------------------------------------------------------------
$ git push origin main
Enumerating objects: 12, done.
Counting objects: 100% (12/12), done.
Delta compression using up to 20 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 1.22 KiB | 1.22 MiB/s, done.
Total 6 (delta 1), reused 0 (delta 0), pack-reused 0
Username for 'http://10.11.19.24:3080':
Password for 'http://dvklopfenstein@10.11.19.24:3080':
To http://10.11.19.24:3080/dvklopfenstein/OMICS_dev.git
   ad50969..7cbef13  main -> main

# --------------------------------------------------------------------------------
THEN MERGE AT UPSTREAM URL PAGE WILL WORK
