GIT
==========
Git is a distributed version control system

problems without VCS:
====================
file content can't be tracked before some timestamp
since you store files in your Hard disk
Collabaration. multiple person can't edit the same file at a time
branching
tagging

1st generation:
===============
files are in the some sharepoint of sites.
Here one person can able to edit the chnages it cannot allow multiple persons to edit the same file at a time

2nd generation:
=====================
Centeralised control system: (Svn)
=============================

Dev1 (working copy)----> commit the changes ---> Cloud(remote copy) ----> checkout the changes ----> new dev-2 ---> he will make changes and again he will commit the chnages ----> cloud ----> again Dev1 will checkout the hanges made by Dev2

- here if the remote copy crash they are poc for the code 
- if it crashed there no poc for get the previous version

3rd generation:
================
Distributed/ de centralised version control system
==================================================
There are 3 developers and one remote repo

Dev1 --> 
He will clone the repo from remote repo (pull the code) --> He contain one working directory and one local repo 
1st we will move the changes to local repo then ---> push the changes --> remote repo

Same thing for all developer 

Here if remote repo crash but every dev have the copy of entrie repo
branching and merging features are improved in GIT over SVN

for connecting remote server we need client software ---> git bash
git server ---> git client

conside floder ---> repo (git init) ---> It will create .git hidden floder ---> It will ytrack everything
It will contain all realated to VCS

git status ---> status of the files
git add <filename> ---> This i called staging and temporary area
It is a temporary area where you stage the files for commit. Usaually we stage the file which your confident about the changes

local repo:
=====================

[ Working Directory ] --(git add)--> [ Staging Area ] --(git commit)--> [ Local Repository ]
                         (all on your laptop) -----> push -----> cenatrl repo

Remote Repo (GitHub)
       ↑
   git push
       ↑
Local Repo (.git folder on laptop)
       ↑
   git commit
       ↑
Staging Area (git add)
       ↑
Working Directory (your files/folders)

git commit-m " message" ---> commits into local repo
git push origin master ---> pushes the commits into central repo
.gitignore ---> contains the files which can be igonred by git
git config --global user.name ""---> set the username 1st time
git config --global user.email ""----> set the mail
git log ---> It will give the history of the commits

Instead of git some company install bitbucket into their servers admins will manage this ...

physical server:
====================
phsical space
power connection
network connection
space
resources to mange servers
os installation

cloud:
============
one programming langugae ---> java,python
one os ---> linux
networking
database
version control system




