title: 如何使用git
---

## Version Control
There are three types of version control systems.  
- Local Version Control Systems
- Centralized Version Control Systems
- Distributed Version Control Systems
  And git is the third one.  

## Git's born
When the linux kernel project can't use BitKeeper(a DVCS),they invented free git.  

## Git baiscs
Git thinks of its data more like a set of snapshots of a miniature filesystem. Every time you commit, or save the state of your project in Git, it basically takes a picture of what all your files look like at that moment and stores a reference to that snapshot. To be efficient, if files have not changed, Git doesn’t store the file again, just a link to the previous identical file it has already stored. Git thinks about its data more like a stream of snapshots.  
The basic Git workflow goes something like this:  

1.  You modify files in your working tree.

2.  You stage the files, adding snapshots of them to your staging area.

3.  You do a commit, which takes the files as they are in the staging area and stores that snapshot permanently to your Git directory.  

## Initialize repository
- In a new directory , type`git init`
  OR
- `git clone <repo>`

If you want start version controling exiting files,use `git add` to track files, and `git commit -m 'initial project version'` to do the first commit .  
## the status of files
untracked (add)-> staged (commit)-> unmodified (edit)-> modified ( stage)-> staged (commit) ->unmodified  
check status ` git status`  
实际操作一下就明了了。一个新文件或者一个修改过的文件，使用`git add`添加进stage，然后`git commit -m 'comment'`。  

## working with remote
To see what remote servers are worked with, use `git remote`.  
To add a remote , use `git remote add <shortname> <URL>`.Commonly,the shortname is origin.  
About `git clone` `git fetch` `git merge` `git pull`,see [this](https://help.github.com/articles/fetching-a-remote/)  
To push to the remote, use `git push -u <shortname> <branch>`.

## Concepts 
Branch:A branch is a parallel version of the main line of development in the repository, or the default branch (usually master). Use branches to:
1.  Develop features
2.  Fix bugs
3.  Safely experiment with new ideas

## Add profile

```bash
git config --global user.name "..."
git config --global user.email "..."
```
