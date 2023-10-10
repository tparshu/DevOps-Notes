What is Git?
-----------------------

Git is  a Version controlling tool  /  SCM  tool.  ( Source code mgmt tool )


Version control systems are tools that help a software team manage changes to source code over time.

For almost all software projects, the source code is like the crown jewels - a precious asset whose value must be protected. 

VCS are sometimes known as SCM (Source Code Management) tool.

Most widely used modern version control system in the world today is Git. Git is a mature, actively maintained open source tool originally developed in 2005 by Linus Torvalds, the famous creator of the Linux operating system kernel. 

Two types Version Controlloing
1) Centrailized Version controlling 
2) Distributed Version controlling

Git is Distributed Version controlling.

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


What is gitbash ?

How to configure username and email for git

$ git init

$ git config --global   user.name "sunilkumark11"
$ git config --global   user.email  "sunilkumark11@gmail.com"

 TO check the configurations
$ git config  --global  --list

working directory ------> staging area -------> LR

untracked files
staged files
commited files

+++++++++++++

How to make working directory as git repository

$ git init

-Observation -

++++++++++++++++





Branching
--------------

This feature is provided in git, so that developers can create code related to different functionalities  on seprate branches.
This helps the development team in creating the code in an uncluttered way.
Later this code can be merged with master branch.
Default branch of git is "Master"


Developer

Home Page   --  f1  f2   f3
Services   --  f4  f5
Contact US  --  f6  f7   f8

branch


git  init  --  master

+++++++++++++++++++++++++++++++++


git branch  branchname 

git  branch test

++++++++++++++


Git  rebase
==============
This is called as fastforward merge.
The commits from the child branch are added to the top of the master branch.
This is helpful when we want code from a branch to be reflected as the latest working version on master.


Rearrange the commit order
---------------------------
git rebase -i HEAD~4


Merge the commit's using "squash"
--------------------------------
git rebase -i HEAD~4
Remove the pick word and replace it with squash

------------------

How to selectively pickup the commit's from child branch ( Cherry-pick )

$ git  cherry-pick   af7f4dc    6b8166d     ( commit id's)


+++++++++++++++++++++

+++++++++++++++++++++


Git Amend
----------------

$ git commit  --amend  -m "a"


How to go back to previous version of code
----------------------------------------------
git reset --hard c9187df
