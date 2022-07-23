# vim, git, etc.
* [vim](#vim)
  * [Place current line elsewhere](#placing-current-line-at-topcenterbottom-of-screen-in-vim)
* [git](#git)
  * [Find deleted files](#find-deleted-files)

## vim

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

### Find deleted files
'''
$ git log --diff-filter=D --summary --reverse | grep delete
$ git log --summary --reverse -- src/bin/bash_text_colors.py
$ git show c34875b5aa8663a82a147d4f05953c38cf3a0ba3 -- src/bin/bash_text_colors.py | tee bash_text_colors.py
$ git checkout c34875b5aa8663a82a147d4f05953c38cf3a0ba3~1 -- src/bin/bash_text_colors.py
'''

### [Remotes](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories)
'''
$ git remote -v
$ git remote add dampierlab [ssh]
$ git push dampierlab main
$ git push dampierlab 
$ git remote add both [ssh]
$ git remote set-url --push both [http]
'''
