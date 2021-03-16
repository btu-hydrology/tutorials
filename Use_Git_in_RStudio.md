---
title: "Git and github in RStudio"
editor_options:
  markdown:
    wrap: sentence
id: "spegg-doku"
output: 
  html_document: 
    toc: yes
    css: custom.less
    fig_caption: yes
---

<!---------
<https://nceas.github.io/oss-lessons/version-control/4-getting-started-with-git-in-RStudio.html> <https://support.rstudio.com/hc/en-us/articles/200532077?version=1.4.1103&mode=server>

<https://r-pkgs.org/git.html>
--------->

## Terminology: Learn to speak version control

A **version control system** is a system that records changes in your code project.
It makes it possible retrace the progress of your development and walk back to earlier versions.
**Git** is a command line program that enables you to do version control on your computer.
You can find different graphical user interfaces for git and many code editors (like RStudio) have incorporated functionality to use git.
The whole collection of files belonging to a project including all previous versions of these files as recorded by the version control system is called a **repository**.
**github** (github.com) is a web page/web service that hosts repositories to share them with other users.
It also offers functionality for discussing and planning the development of the project.
You can copy a **remote repository** from github to a **local repository** on your computer, to start working on it.
You record changes in the code by doing a **commit**.
A commit is a snapshot of all your files in that specific version.
You can then **push** the commit (the code changes) back to github.
Others then are able to **pull** your commit into their own local repositories to incorporate your changes in their work.
A **merge conflict** means that someone has pushed code changes to github that conflict with changes you made in your local repository.
In this case you can't push to github unless you pulled down the new commits and incorporated the changes into your code.
Often times this can be done automatically by git.
Sometimes you have to do it more tediously by hand.

A git **branch** is used when you want to work on something without blocking other development.
You can imagine the commit history as a chain of code changes.
You can choose to branch some developments off that chain.
A branch can be created for example to implement and test a certain feature.
You can rejoin the feature branch with the main branch once you consider the side project finished.
Other developments can continue while you are working on the feature branch and you can switch back and forth between branches and choose on which to work next.
Branches can be opened only on your computer or synced to github to be shared with others.
You can also branch off a project that will take a completely different trajectory.
This is usually called a **fork**.

On github you can plan your development by defining **issues**.
Issues are tickets for specific work packages like "implement this feature", "fix that bug", "test that thing" or "work on this idea".
Every issue has a discussion page.
If the task is resolved, the issue/ticket can be closed.
You can reference the git commit that resolved the issue.
**Milestones** are goals you set in the progress of your development.
Issues can be associated with a milestone.
The resolution of all issues associated with a milestone (should) mean that the milestone is reached.

**Additional info:**

-   The biggest alternative to git is [Subversion](https://subversion.apache.org/)
-   Alternatives to github are for example [Bitbucket](https://bitbucket.org), and [GitLab](https://about.gitlab.com)

## Working with git in RStudio

You can do version control on your computer with git (the software) without ever using github (the web page/web service).

### Install git on your computer

In order to use git you have to install it on your computer first.
You can find instructions for Windows, Mac an Linux [here](https://happygitwithr.com/install-git.html).

### Initiate git versioning for a new or existing projects

In order to use git in RStudio you first have to create a project.
You can learn more about using projects [here](https://support.rstudio.com/hc/en-us/articles/200526207-Using-Projects).
Go to *File \> New Project...* and follow the instructions.
Make sure to tick the box "Create a git repository" in the window where you define the name of the project.

You can also activate git version control for an existing project in the project options.
You can find the project options in the menu "Tools" or by clicking the project button on the upper right of the RStudio window.
You can activate git in the "Git/SVN" section.

![RStudio project settings](images/RStudio%20project%20settings.png){width="400"}

Once you activated version control for the project a new tab called "Git" appears in the upper right panel of RStudio.
There you can see which files changed in your project folder.
You can display a "Diff" for every file.
This shows exactly what was added and what was deleted in this file.
You can review your changes and stage them to be included in a commit.
You can also view the commit history, create new branches and push and pull commits to and from github.

![The Git tab in RStudio](images/GIt%20tab%20in%20RStudio.png){width="100%"}

### Set your name and email address

Before you can make a commit (see explanation below) you have to tell git which name to record in the commit description.
You do this in the Terminal (the tab next to the Console in the lower left panel).
Type in these commands:

```{bash}
git config --global user.name 'Jane Doe'
git config --global user.email 'jane@example.com'
```

Of course you have to insert your name and e-mail address.

To check your settings you can use:

```{bash}
git config --global --list
```

You can also set a specific name or email for the current repository if you replace `--global` with `--local`.

### Review code changes

If you change a file in your project it will be shown in the git panel as "modified".
If you add new files to your project the will be shown as "untracked", because they are not tracked in the version system yet.
If you delete a file that was recorded in the version system before it will be shown as deleted.

Don't confuse the file listed under "Files" in the bottom right panel with the files listed in the git panel.
The "File" panel is your file browser.
It shows all files in your project.
The list in the "Git" panel shows just the files that changed.

If you want to check what changed in a file that is shown as modified, you can press "Diff".
In the new window you can click on the different files and see the code changes in the panel below.
Green lines are added code lines and red ones are deleted code lines.

### Make code snapshots (commits)

If you want to include files in a commit (a project snapshot), you have to tick the box in front of the file name in the git panel or in the diff view.
This moves the status of this file to "staged for commit".

In the diff view you can also select single code blocks or single lines to include in the commit (and leave out others).
Note that you can view the "staged" and the "unstaged" code blocks in the diff view.
Everything that is in "staged" will be included in the commit.
Everything that is "unstaged" will be left out.
You also can "unstage" some of the staged code blocks.

Finish the commit by inserting a commit message in the top right textbox in the diff view.
This message will be recorded in the commit together with your name and email address you told git with `git config` (see above).
Click on "Commit" to make the snapshot.

### View commit history

You can view the commit history by clicking on the clock icon in the git panel in the main RStudio Window or by clicking "History" in the diff view.
You see a list of commits with their commit message, date and author.
You can click on every commit and see what changes where introduced into the project with this commit.

## Use RStudio with github

By linking your local git with github you can share your code online.

### Link RStudio to github

In order push and pull code to and from github you have to upload a key from RStudio to github.
You have to do this only once.
You can read more about it [here](https://happygitwithr.com/ssh-keys.html).

1.  Generate public/private key pair in RStudio: Go to Tools \> global settings.
    Got to View "Git/SVN" and click "Create RSA Key".
    After that is finished (close the opening window), click on "View public key" and copy the key.

2.  Insert the key on github.com.
    Choose one of these two ways:
    
    1.  Grant access to your entire account (all the repositories you have access to):
    
        1.  Go to <https://github.com/settings/keys> (you have to login for that)
        2.  Click "New SSH key"
        3.  Insert the key you copied and give a title (the title is used to remind you what key this is, you can choose any).
        
    2.  Grant access only to a particular repository:
    
        1.  Go to `https://github.com/<organisation_or_account>/<repository-name>/settings/keys` (you have to insert the path to your repository).
        2.  Click on "Add deploy key"
        3.  Insert the key you copied and give a title (the title is used to remind you what key this is, you can choose any).

There is an alternative way to [link RStudio to github using http](https://happygitwithr.com/credential-caching.html), but I recommend to use the ssh key.

### Clone a repository from github into RStudio

Downloading an existing project from github is called cloning.
You can do this in RStudio like this:

1.  Copy your repository url:

    1.  go to your repository page on github
    2.  Click on the green button that says "Code"
    3.  Choose "SSH"
    4.  Copy the url that is displayed (it should start with `git@github.com:`)

2.  Download repository to RStudio:

    1.  In RStudio click *File \> New Project...* . In the opening dialog click "Version Control", then "Clone a project from a Git repository".
    2.  Insert the url you copied from github.
    3.  If you want you can choose a different name for the project (defaults to the name of the github repository).
    4.  Choose a folder to save the project.

More information is available [here](https://happygitwithr.com/rstudio-git-github.html).

### Push code changes to github

By pushing you upload your local code changes to github.
You upload only commited changes.

1.  Make a commit.

2.  Press the green upwards arrow in the git tab or the diff view.

### Cannot push

You cannot push code to github if there is new code available that you don't have in your local version.
This is the case when you try to push and get the following error message:

    hint: Updates were rejected because the remote contains work that you do
    hint: not have locally. This is usually caused by another repository pushing
    hint: to the same ref. You may want to first integrate the remote changes
    hint: (e.g., 'git pull ...') before pushing again.

In this case you have to pull code from github first.

You can read more about push rejection [here](https://happygitwithr.com/push-rejected.html).

### Pull code from github

By pulling you download new code from github and incorporate it into your local files.
You pull code from github by pressing the green downward arrow in the Git panel in the main window or in the diff window.

If you have no local commits, the downloaded commits are just appended to your local commit history.
All files in your project folder will be changed to the latest version.

If you have local commits that are not on github, git will try to automatically merge the local with the remote (github) commits.
If changes are in different files or at least in different lines in the same file, the automatic merge will work.

### Merge conflicts 

If changes you recorded locally and changes on github affect the same lines of code, you will have a merge conflict and RStudio will tell you so.
In this case your code will be changed in this fashion:

    <<<<<<<<< HEAD
    Line of code I wrote locally
    ==============
    Line of code I pulled from github
    >>>>>>>>>>>>>>

You will have to go through the the file and decide on every code block that is marked like this which version you want to keep.
Delete the code that you dont't want to include.
Don't forget to also delete the `<<<<<<<<<`, `=========` and `>>>>>>>>>` lines.
After this you can make a normal commit.
This resolves the merge conflict.
You can read more about this [here](https://docs.github.com/en/enterprise-server@2.20/github/collaborating-with-issues-and-pull-requests/resolving-a-merge-conflict-using-the-command-line).

### Cannot pull

There are several reasons why you can't pull code from github.
The most common is that you have uncommitted changes in your codebase that would be overwritten by the download from github.
Commit them first and then you should be able to pull.
You can read more about problems occurring while pulling [here](https://happygitwithr.com/pull-tricky.html#pull-tricky).
