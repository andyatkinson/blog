---
layout: post
title: "How to code review a repository with github"
date: 2013-10-16 11:58
comments: true
categories: [Tools, Git]
---

Github line and pull request commenting features with markdown formatting are great for code reviews. Recently I was asked to do a code review on a whole repository as opposed to a specific commit or pull request, which meant the github commenting features were not available.

It is possible to use the commenting features with a little bit of preparation. The steps I took to prepare the repository so that I could use the commenting features are below. There are probably other ways to accomplish this as well, please let me know if you have suggestions.

Fork the repository
---------
First I forked the repository so that I didn't introduce any commits on the main repo. The repository was private and I have a paid github account, so forking the repo created a private repository. I am not sure whether a private repository is created when forking without a paid account.

Create a code review branch
----------
I created a `code_review` branch (`git branch -d code_review`) off master. This branch was pushed to my fork (`git push andy code_review`).

Remove all the files on master
----------
On `master` I removed all the files git knows about with `git rm -rf *`. Next I pushed `master` to my fork with `git push andy master`.

Create a pull request
-----------
Using the github interface, I created a pull request comparing `andy/master` with `andy/code_review`. This makes it look like all the files are being added. Now using the pull request, line comments and pull request comments can be made, discussion can happen with the original author via the pull request link. If any additional commits are pushed to the fork, the original author can cherry pick the commits with `git cherry-pick sha`. When the original author is happy with the code review, the fork can be deleted. 
