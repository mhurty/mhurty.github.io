---
layout: post
title: "Deploy a SQL query to Material Girl in Ecto"
date: 2016-08-15
---

To create a new materialized view in Ecto/Material_Girl
--

If this is the first time you've worked in Ecto, clone the **ecto** repository to your laptop. 
In the terminal, navigate to your git documents directory

- `git clone git@github.com:educationsuperhighway/ecto.git`

This will create a folder named ecto in your personal git directory

If you've already worked in the **ecto** repository, you should refresh your local copy from Master. Navigate to your ecto folder, make sure you are in the master branch, and issue the command:

- `git pull origin master`

This will bring your local master branch up to date with the current master on github

While you are at it, you will also need a copy of the **berks** repository on your laptop, so repeat the above steps with the **berks** repository.

Add or update your files
------------------------

Once you have cloned or updated the repositories on your local system, open the **ecto** repository and checkout a new branch for editing:

- `git checkout -b name-of-your-editing-branch`

Add your queries:
-----------------

Components go in the folder appropriate for the fiscal year. (There are currently `fy2015_districts` and `fy2016_districts` folders for the components.) Endpoints go in the endpoints folder. You may need to edit the FROM statement in your endpoint query to add the folder to the component view name. E.g., if you're editing a query with components in the fy2016_districts folder you need to prepend that to the name of the component in your endpoint query.

When you are done uploading/editing ... 

Edit `versions.rb` in the **ecto** repository to show the updated version. The version will be something like 1.5.2 and you will increment the middle number to indicate that this is a minor enhancement. (i.e., in this case you would change the version to 1.6.2)

- `git status`
(this will show a list of files that have been edited and need to be committed.)
- `git add name-of-file` (or `git add -A` to add all the files)
- `git commit -m "add-your-short-descriptive-note-here”`
(this commits your files in preparation for merging)
- `git push origin name-of-your-editing-branch `
(this pushes a copy of your editing branch to github)

create a Pull Request and Review App
--

Before merging your new or revised query into **ecto**, you will create 2 Pull Requests and a review app and ask for a review from the members of your team. To create the first pull request, login to Github and select the **ecto** Repository.

- Click the green "New Pull Request" button.
- Compare the master branch to your working branch.
- Click the green "Create Pull Request" button to create the actual pull request.

Switch to the **berks** repository on your laptop and create a new branch so you can update the `Gemfile` with the path to your working branch in ecto so that you can create a Review App. (For simplicity, consider using the same name for the berks repository as the branch name you are using on the ecto repository.):

- `git checkout -b name-of-your-editing-branch`

Open the `Gemfile` and look for the line "# ESH data access" and replace the "branch:" attribute (shown below as "master") with the _name-of-your-editing-branch:_

>... 

> `# ESH data access`
`gem 'ecto', git: 'https://github.com/educationsuperhighway/ecto.git', branch: 'master'`

>...

Then commit this branch to the **berks** repository on Github and create a pull request with that commit. (You'll repeat the same steps as you did above when you created the **ecto** PR.):

- `git commit -m "add-your-short-descriptive-note-here”`
- `git push origin name-of-your-editing-branch `

Launch Github in your browser and get into the **berks** repository: 

- Click the green "New Pull Request" button.
- Compare the master branch to your working branch.
- Click the green "Create Pull Request" button to create the actual pull request.

Create the **berks** Review App using the tools on Heroku. **Process to be further clarified here. My credentials won't allow me to create a review app, but the process is spelled out in [Steve's review app documentation](https://educationsuperhighway.atlassian.net/wiki/display/SOFTWARE/New+Heroku+Deploy+with+pipelines) on the ESH wiki.**

- Share the Pull Request (PR) and Review App with your team.
- Process the feedback from your team (making updates in the **ecto** branch). 
- Once you get an emoji from your team members (at least one analyst and one developer), merge your **ecto** branch with master.

You only need to merge into **ecto** -- the **berks** editing branch should *not* be merged.

In **ecto** on your local system: 

- `git checkout master`
- `git pull origin master`
- `git merge test`
- `git push origin master`

(This updates your local master to match the master on github, then merges your local editing branch into your local master then pushes your updated local master to the github master.)


Switch to **berks** and delete the working branch from your local system
------------------------------------------------

- `git checkout master`
- `git branch -d name-of-your-editing-branch`