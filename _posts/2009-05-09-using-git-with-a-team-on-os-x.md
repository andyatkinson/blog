---
layout: post
title: Using Git with a team on OS X
date: 2009-05-09
comments: true
categories: [Git, Productivity, Tools]
---

This is an introductory or intermediate level article on using git with a team.

1.  Install git. I used Macports and bash on OS X. `port install git-core +bash_completion`. Follow the instructions to update your bash profile. Search available git variants with `port git-core variants`. If you already have git-core installed without bash completion, deactivate it and reinstall it to add it. Now you have git installed and can tab-complete branch names.

2.  Learn git. Use the man page and search for lots of great documentation including this [everyday git](http://www.kernel.org/pub/software/scm/git/docs/everyday.html) page. I prefer documentation from the cheat gem to man [read more about cheat here](http://errtheblog.com/posts/21-cheat). Run `cheat git` and [update the wiki with tips](http://cheat.errtheblog.com/s/git).

    I also recommend the `git_remote_branch` gem, which provides a `grb` executable that makes branch administration friendlier. Run `grb explain commandname` to preview git commands.

       `gem install cheat git_remote_branch`

3.  Review team commits. I do this with graphical tools and the command line. The graphical tools I recommend are [GitNub](http://wiki.github.com/Caged/gitnub) and [GitX](http://gitx.frim.nl/), which optionally install `nub` and `gitx` executables (respectively) in your path. Both tools display gravatars for commit authors. GitX has a nice "Commit" view (Command+2), showing staged and unstaged changes.

4.  Develop a workflow for your team. Here is a sample workflow. Deploy changes only from the `master` branch. Develop features or fix bugs on branches. When the branch is ready for others to work with, use `grb publish newbranch`. Use `git branch -a -v` to view local and remote branches. Use `grb track branch-name` to track a new branch not yet available in a local git repository. Use `git mergetool` to fix merge conflicts when pulling new code. Use FileMerge on OS X, or merge the file with a text editor. Merges with FileMerge are automatically staged, use `git add filename` to stage changes from a manual merge. Use `git checkout .` to reset your current working directory.

    When changes on a branch or new branches are ready to go live, pull them with `git pull origin newbranch` When a feature or bug fix branch has been integrated into master, use `grb delete branch-name` to delete both the remote copy and your local copy.

    Use `git stash` to store uncommitted files temporarily. Use `git stash apply` when the files can be applied to a branch. More than one stash can be maintained.
    
Environment customization
---
I recommended adding aliases and color to git output. You can do accomplish this by using the `~/.gitconfig` file. Changes here are effective for all git repositories on a machine. Here is a sample `~/.gitconfig` file.

``` bash
        [user]
      	  name = Andy Atkinson
        [apply]
      	  whitespace = nowarn
        [color]
          ui = auto
        [color "branch"]
          current = yellow reverse
          local = yellow
          remote = green
        [color "diff"]
          meta = yellow bold
          frag = magenta bold
          old = red bold
          new = green bold
        [color "status"]
          added = yellow
          changed = green
          untracked = cyan
        [alias]
          st = status
          ci = commit
          br = branch
          co = checkout
          df = diff
          lg = log -p
``` 

More resources
---
The best resource for me was using git with experienced team members who helped me learn. I did purchase and recommend the [Git Peepcode screencast](http://peepcode.com/products/git). [GitCasts](http://www.gitcasts.com/) is a free screencast resource. I recommend [github](http://github.com/) for repository hosting. [Unfuddle](http://unfuddle.com/), [Gitorious](http://gitorious.org/), and [codebase](http://www.codebasehq.com/) are others.


Update 2013: I do not recommend a git gem and recommend built-in git commands instead.
