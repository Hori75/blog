---
layout: post
title:  "Git Guide or Cheatsheet or Whatever"
author: hori75
date:   2022-02-27 22:45:00 +0700
background: '/images/GitGuideorCheatsheetorWhatever-image.png'
excerpt_separator: <!--more-->
---

Git is a common version control used on Software Engineering projects.
<!--more-->
You could see that every projects maintained online used git in majority.
Learning git is a necessity if you would like to work in a codebase maintained by a group or company.
This post currates a list of common knowledge and guide I found and followed.

### Overview of Git

A codebase is stored in a **repository** either local or on a remote server.
In the repository, there is a **"main" branch** that represents the current progress or release.
The repositories often have many branches of others.
You save your progress by creating a **commit** consists of your changes into a branch.
You could **branch** from other branch and **merge** a branch into other branch.

With git, you could work on a task alongside with others' work in the same codebase.
This is important as you need to store your own work and merge with the rest of others' work in a good way.

### Git Remote Server

There are sites that host remote repositories such as [github](https://github.com), [gitlab](https://gitlab.com), etc.
These sites have utility features such as continous integration/deployment (CI/CD) and merge request that can be reviewed by others.

### Commands of Git

This is a list of git commands I have used.

#### Initializing a Repository

{% highlight bash %}
git init
{% endhighlight %}

This command is used to initialize a local repository. The `.git` folder is initialized by this command. 

#### Cloning a Remote Repository

{% highlight bash %}
git clone <remote_url> <target_dir>
{% endhighlight %}

This clones a remote repository into a folder. An origin remote is set to able to pull and push to the remote repository.

#### Setting Remote Repository

{% highlight bash %}
git remote add <remote_name> <remote_url>
git remote set-url <remote_name> <remote_url>
git remote remove <remote_name>
{% endhighlight %}

This command is used to manage remote repositories it relates to. 

#### Stage Changes

{% highlight bash %}
git add <files>
{% endhighlight %}

This command stages files to be commit.

#### Commit Changes

{% highlight bash %}
git commit
git commit -m <commit_message>
git commit -a
{% endhighlight %}

This commits changes staged using `git add`. You also could modify previous commit using `-a`.

#### Pull Changes from Remote Repository

{% highlight bash %}
git pull
git pull <remote> <branch>
{% endhighlight %}

This command pull commits from remote repository.
If executed on different branch, it will create a merge commit to apply pulled commits.

#### Push Changes to Remote Repository

{% highlight bash %}
git push <remote> <branch>
{% endhighlight %}

This command pushes commits created locally to the remote repository. This creates new branch if it doesn't exist.
You could use `--force` to rewrite commit history with your local commit history.

#### Status

{% highlight bash %}
git status
{% endhighlight %}

This command outputs an overview of your local repository. This includes current branch and uncommited changes if any. 

#### Branch

{% highlight bash %}
git branch <new_branch_name>
{% endhighlight %}

This command creates a new branch for current branch. Keep in mind that you need to select the new branch using checkout.

#### Checkout

{% highlight bash %}
git checkout <branch_name>
git checkout -b <new_branch_name>
{% endhighlight %}

This command changes the current branch to specified branch.
You could use `-b` to create new branch and checkout to the new branch.

#### Log

{% highlight bash %}
git log
git reflog
{% endhighlight %}

`git log` is used to see the history of commits on current branch. 
You could see the code on that commit version using `git checkout <commit_sha>`.
`git reflog` is used to see the history of git command you used. 

#### Stash

{% highlight bash %}
git stash
{% endhighlight %}

This command stashes your uncomitted changes. Useful when you need to pull or change branch.
To unstash, use `git stash apply`.

#### Rebase

{% highlight bash %}
git rebase <branch_source>
{% endhighlight %}

This adds commits added from source branch before repeating your commits on current branch.

### Tips and Tricks

These are tips and tricks that could be used for convenience.

#### Updating Branch without Merge Commit

Before merging your work into the main remote branch, you often need to update your branch to the latest commit done in main branch.
You could just `git pull origin master` to update your branch, but this will create a merge commit which is often 
cumbersome. You could instead utilize `git rebase` for this matter. 
This is command I run when I need to update my branch before merge.

{% highlight bash %}
git checkout master
git pull origin master
git checkout <branch_name>
git rebase master
git push --force origin <branch_name>
{% endhighlight %}

`--force` is required here because the commit you create on the branch is repeated and hence creating new SHA for the commit.
This will cause history between local and remote become different and need to be rewritten.

#### Reverting Recent Unpushed Commit

When you accidentally commit your changes, you have two choices: Reset to remote state which wastes your current work, or use this command

{% highlight bash %}
git reset HEAD~1 --soft
{% endhighlight %}

This will undo the local commit, assuming your last action is committing.

#### Use `.gitkeep` for Empty Directories

You couldn't commit empty directories. But you could place `.gitkeep` to keep the empty directory.

### Conclusion

Git is a nice version control that has wide features and commands that you might not use.
But once you learn basic of committing, branching, and merging, you will get used to these commands and tricks.
