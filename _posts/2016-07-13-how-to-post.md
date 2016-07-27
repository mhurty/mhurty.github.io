---
layout: post
title: "How To Post"
date: 2016-07-13
---

Once you have cloned the repository on your local system:
---------------------------------------------------------

- git checkout -b < name-of-your-editing-branch >

do all your editing, and once you are done ... 
----------------------------------------------

- git status
(this should show a list of files that have been edited and need to be committed.)
- git add < name-of-file >
- git commit -m <“note”>
(this commits your files in preparation for merging)
- git push origin < name-of-your-editing-branch >
(this pushes a copy of your editing branch to github)
- git checkout master
(switch to the master branch on your local machine so that you can merge your working branch into your local master branch. This keeps your local master up-to-date.)
- git merge < name-of-your-editing-branch >
(this merges your branch into the copy of master on your laptop.)

create a pull request
------------------------
Before merging your new or revised query into Github, you will create a Pull Request and ask for a review from the members of your team. To create a pull request, login to Github and select the repository in which you are working.

- Click the green "New Pull Request" button.
- Compare the master branch to your working branch.
- Click the green "Create Pull Request" button to create the actual pull request.
- Share the Pull Request (PR) with your team.
- Process the feedback from your team.
- Once you get an emoji from your team members, merge your branch with master. (You can merge the branch into the original git master using the merge button on github, or you can merge using the command below.)

- git push origin master (this pushes your local copy of "master" to the github "master")

delete the working branch from your local system
------------------------------------------------

- git checkout master
- git branch -d < name-of-your-editing-branch >