---
layout: post
title: git as an svn client
category: work 
---
### Installation
+ [msysgit] (http://code.google.com/p/msysgit/)
+ [tortoisegit] (http://code.google.com/p/tortoisegit/)

### Git helps you think differently
I often find that svn trains me to commit at feature completion, thinking "I don't want to break the build". As a consequence, I keep changing files until the feature is complete.

> With git, you have local changes. Make a commit. Makes lots of commits!

When I have one commit to make but several approaches of solving the issue and I don't know which one is best, I have to just choose one way. Then if it doesn't work out, I have to undo everything and try the other approach. I hope I don't need those changes again. 

> With git, branch. You have local branches. Use them.

### Gitconfig 
Note that there are three config files, at the repo level, at the user/global level, and at the system level.
The repo level config is in the \.git folder (gitconfig) and the user level config is in your profile folder.

The first thing you'll need to do is set the editor, you can do so by typing in the shell:

> git config --global core.editor 'c:/progra~2/vim/vim73/gvim.exe'

Replace gvim.exe with anything you'd like (except notepad. No one should be using notepad.) 
After the editor is set the in the global/user level config you can run the following commands to access the various configs:

	git config -e             # where -e loads it in the specified editor
	git config --global -e    # where --global loads the user level config 

There are loads of tutorials and loads of config files that you can copy from the internet. So I won't specify every little bit. The important fact is that now you're able to edit the config as you see fit, consider adding these two aliases. 

	[alias]
	spull = !git-svn fetch && git-svn rebase
	spush = !git-svn dcommit

### The pull down

Now with git configured, you'll need to setup the local version of your svn repo. 
> 1. Assuming your bash shell or command prompt is at c:\source\
> 2. Run: git svn clone http://my.svn.repo localRepo
> 3. a new folder at c:\source\localRepo should exist
> 4. a new folder at c:\source\localRepo\.git should exist
Now you should have a folder at: c:\source\localRepo

It will take some time (and possibly retries - follow the steps outlined in the output). For example, it took a couple of days for me to clone my svn repo with over 14,000 commits. Part of the problem was the crappy infrastructure, so don't think that's normal.

> Do you have lots of files (over 100k? over 500k?)
>
> Do you have very large files?
>
> You may need to break up your one large svn repo to many local git repos

Do note that git is different and if you have lots of HUGE files or a huge number of files, maybe it's best to create several git repos to represent your one svn repo. Get a feel for why this is so by reading [an explanation from the guy that wrote git](http://osdir.com/ml/git/2009-05/msg00051.html) 




