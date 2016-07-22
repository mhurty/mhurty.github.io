---
layout: post
title: "How To Post"
date: 2016-07-13
---

git status

git checkout -b < name-of-your-editing-branch >

— do all your editing —

git status

git add < name-of-file >

git commit -m <“note”>

git push origin < name-of-your-editing-branch >

git checkout master

git merge < name-of-your-editing-branch >
(this merges your branch into the copy of master on your laptop.)

— [create a pull request](/blog/2016/07/22/pull-requests) —
(You can merge the branch into the original git master using the merge button on github, or you can merge using the command below.)

git push origin master
(this pushes your local copy of "master" to the github "master")

— delete the working branch from your local system — 

git checkout master

git branch -d < name-of-your-editing-branch >