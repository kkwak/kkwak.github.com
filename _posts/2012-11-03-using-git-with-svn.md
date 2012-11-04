---
layout: post
title: using git with svn 
category: work
---
### Assumptions ###
That the config file has these two aliases:
>	[alias]
>	ci = commit
>	co = checkout
>	spull = !git-svn fetch && git-svn rebase
>	spush = !git-svn dcommit

That the repo exists (having cloned it from the existing svn repo):
> git svn clone http://my.svn.repo localRepo

That the original svn repo has a standard layout:
>	/trunk
>	/branches
>	/tags
If you do not have a standard layout please read the doc on: [git svn clone](http://git-scm.com/docs/git-svn)

### Typical Workflow ###
0. **git co master** - Move to the branch named master
1. **git ci -a** - commit (adding changed files)
2. **git spull** - pull down commits from svn
3. **git spush** - push changes to svn (it will pull down changes if there are changes in svn)

When working with svn, you should keep your commits as linear as possible. Merges are not recommended, instead rebase everything.
Rebasing changes history, so you should not rebase anything that is in svn already or a commit that is on another repo. 
> git merge --squash --no-commit branchWithYourCommits

### Branches/Tags ###
Create a new folder under the /tags folder named "rev-1.5" with the commit message of "Tag this release"
Create a new folder under the /branches folder named "unicorns"
>	git svn tag -m "Tag this release" rev-1.5
>
>	git svn branch -m "Branch for unicorns" unicorns

Commits can be found if they have not been deleted. Remember that when you rebase, each commit becomes a new commit.
>	gitk --all $(git fsck --no-reflog | awk '/dangling commit/{print $3}')

Revert all local changes on the existing local branch and match with what is in svn
>	git reset --hard remotes/git-svn
>

