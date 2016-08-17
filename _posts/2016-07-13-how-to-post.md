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

While you are at it, you will also need a copy of the **berks** repository on your laptop, so repeat the above steps with the **berks** repository. Before cloning the **berks** repository, make sure you are not working inside the **ecto** repo -- we want to keep these two folders separate on your local system so that **berks** doesn't end up inside of **ecto**. As an example, here's how my local folder is set up:

![my git folders](/img/git-folders.png)

Add or update your files
------------------------

Once you have cloned or updated the repositories on your local system, open the **ecto** repository and checkout a new branch for editing:

- `git checkout -b name-of-your-editing-branch`

Add your queries to the Material\_Girl instance in ecto
-----------------

Components go in the folder appropriate for the fiscal year. (There are currently `fy2015_districts` and `fy2016_districts` folders for the components.) For example for 2016 district metrics, the components would go into:

`ecto/db_ecto/material_girl/component/fy2016_districts` 

Endpoints go in the endpoints folder:

`ecto/db_ecto/material_girl/endpoint/`

You may need to edit the FROM statement in your endpoint query to add the folder to the component view name. E.g., if you're editing a query with components in the fy2016_districts folder you need to prepend that to the name of the component in your endpoint query.<sup id='fnref1'>[1]</sup>

When you are done uploading/editing ... 

Edit `version.rb` in the **ecto** repository to show the updated version. The version will be something like 1.5.2 and you will increment the middle number to indicate that this is a minor enhancement. (i.e., in this case you would change the version to 1.6.2)

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
- Compare the master branch to your working branch. <sup id='fnref2'>[2]</sup>
- Add a comprehensive note on the content of the Pull Request so that your reviewers will know what they are looking for in the new or updated code. 
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

Merge your new work into Master.
--------------------------------

You only need to merge into **ecto** -- the **berks** editing branch should *not* be merged.

You can use the Merge tool on Github to merge the branches. (This is the best alternative, but if you prefer, your changes may be merged from the command line as well.) To merge on Github, use the green "Merge Pull Request" button midway down the pull request page. 

![github merge](/img/github-merge.png)

Switch to **berks** and delete the working branch from your local system
------------------------------------------------

- `git checkout master`
- `git branch -d name-of-your-editing-branch`

---

Last Update: August 16, 2016

---

Notes
	
<a id="fn1"></a>
**From Statement**: 
When you initially create the views and write your queries, you may have assumed that all the components and the endpoints would be in the same directory. Material\_Girl keeps components and endpoints in separate folders in the repository. Material\_Girl has defined folder paths, but the specific folder that is used to maintain a specific name-space for the components needs to be specified in your endpoint query. For example, if you created your endpoint by selecting from a file named: `district_metrics.sql` your query's *from* statement might say 

`select (something) from district_metrics` 

but the `district_metrics` component file is in the `fy2016_districts` folder. In order to find the file, you'll need to prepend `fy2016_districts` in your *from* statement so it reads 

`select (something) from fy2016_districts.district_metrics` 

to give your endpoint the information it needs to find the query file. <a href="#fnref1"  class='footnoteBackLink'  title="Jump back to footnote 1 in the text.">&#x21A9;&#xFE0E;</a>

---

**Compare Branches**: 
When you create a Pull Request you are going to click on a control on the Github page that selects which existing branch to which you are going to compare your editing branch. This will allow you to see changes you've made to any files compared to previous versions of those files. (If the files are new, of course there won't be any code changes to compare.) If you are uploading changes/updates, other analysts and developers will review the code in your new or updated files by using the diff interface that displays those changes side-by-side with the previous version of the code. 
<a href="#fnref2"  class='footnoteBackLink'  title="Jump back to footnote 2 in the text.">&#x21A9;&#xFE0E;</a>


[1]: #fn1
[2]: #fn2


