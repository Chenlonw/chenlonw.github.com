---
layout: post
title:  "Git tutorial - the best version control software ever"
date:   2016-05-24
excerpt: "Some notes made by myself when I was learning git"
tag:
- git 
- version control 
- tutorial 
comments: true
---

> This is a post that tells you what the git is and gives explanations of some basic git commands.
> I also suggests some good materials that you can used for learning git better.

### A short history of Git

[Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds) is the creator and, for a long time,
principal developer, of the Linux kernel. The management of different versions of Linux, however, was
becoming more and more complicated due to the increasing contributors from all over the world. In
2002, the Linux kernel project began using a proprietary distributed version control system called
BitKeeper. Unfortunately, In 2005, the relationship between the community that developed the Linux
kernel and commercial company (the BitKeeper) broke down. Linus Torvalds had no choice but created a
version control system by himself. He gave this system a name of Git. Until now, it has become the
most famous version control system.

### Advantanges

Git is not the first version control system. The major difference between Git and the other similar
systems (CVS, Subversion, Perforce, and so on) is the way Git thinks about data. Most other systems
store information as a list of file-based changes. Git thinks about its data more like a *stream of
snapshots*.

+ **Distributed system**
Most operations in Git need local files and resources to operate. No information is needed from
another computer on your network. It makes checking or updating your repository really simple and
instant.

+ **Integrity**
Everything in Git is check-summed. It is impossible to change the contents of your repository
without Git knowing it. It is the philosophy of Git system.

+ **Git only adds data**
Git adds data to the repository when you take any action with Git. It means everything in your
repository is undoable.

### Basics of Commands

*Git setup*

$ git config --global user.name "your name"  
$ git config --global user.email username@example.com
{: .notice}

*Git basics*

1. `git init`: initials your directory by git, it will automatically create an invisible directory
called `.git`
1. `git status`: checks the status of your git directory
1. `git add filename`: tells git start to tracking this file it also can with the wildcard like `git
add *.txt`, it will start to tracking all the *.txt* files in the main directory.
1. `git commit -m "message"`: let git take a snapshot of your directory, and leave a message for it
1. `git log`: to see the messages in this directory. `--pretty-oneline`
1. `git remote add origin https://github.com/try-git/try_git.git` : add local git directory into the
github server. The `origin` is only the name of your remote, but typically we call it `origin`
1. `git remote set-url origin git@github.com:USERNAME/REPOSITORYNAME`: you can create a new
repository in the server from your side.
1. `git push -u origin master`: push our directory to **GitHub**, where the `origin` is the name of
the remote repository with URL `https://github.com/try-git/try_git.git`; `master` is the name of our
local branch.  the argument `-u` is telling git to remember this combination, so next time you only
need to type `git push`.
1. `git pull origin master`: after sometimes your remote repository might be modified by others, you
can use this to get the updates
1. `git stash` and `git stash apply`: sometimes you might not want to commit the modification on
your own directory, you can use `git stash` to hide them and after pull, you can re-apply them by
`git stash apply`
1. `git diff HEAD`: let you diff the newest version with the last commit. The `HEAD` here is a
pointer which points to the last commit, otherwise, you need the `SHA`. 
1. `git diff --stage`: to see the changes you just staged.
1. `git reset filename`: to unstage files
1. `git checkout -- finename`: after reset the file, it will be unstaged, but if you want a file
back to the status when last time you committed, you can you this commands. the `--` means no more
options after the `checkout`, otherwise, if you happen to have a branch called the same name by
filename, it won't check out the branch.
1. `git branch branch_name`: when you want to debug, you can create a copy of you code with this
command. after debugging, you can merge the branch back to the main branch and push to the server. 
1. `git branch`: you can see the info about branches you have
1. `git checkout branchname`: you can switch to the branch called `branchname`
1. `git checkout -b branchname`: you can create a new branch and switch to it in one command instead
of the combination of steps 14 and 16
1. `git rm filename`: git will remove the `filename`, after that, you need to `commit` your change.
if you want to remove a file, you need the argument `-r`, but after that you still need to `git rm`
all the files inside. but a smart way is by adding an argument `-a` when you commit.  
1. `git checkout master`: after you fixed something in the branch, you need to back to the main
branch called master.
1. `git merge branchname`: merge the fixed things in `branchname` to the main branch.
1. `git branch -d branchname`: after merge you might need to delete the branch.  however if you
haven't merged, you really want to delete, you need argument `-D`
1. `git push`: to update your modification to the remote server.

**suggested references**  

+ Official [Git book](http://git-scm.com/book/en/v2)
+ A good website for [trying Git](https://try.github.io/levels/1/challenges/1)
