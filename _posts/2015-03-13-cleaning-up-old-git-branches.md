---
layout: post
title: "Cleaning up old git branches"
date: 2015-03-13 13:00
comments: true
categories: [Programming, Productivity]
---

With some git commands and bash scripting we can clean up old branches quickly.

The final solution looks like this:

``` bash
g old | head -n5 | xargs bash -c 'git branch -D $@; git push origin :$@;' bash
```

##### Breaking it down

1. Using a git alias we can list branches by the date they were committed to, with the oldest at the top.
1. The output is limited with `head` and `-n`, for example 5 items is `head -n5`.
1. `xargs` provides each branch as `$@` which is substituted in each of the next commands.
1. We execute the normal command to delete the branch locally and from a remote named `origin`.

##### Listing old git branches

Add the following alias to your `~/.gitconfig`.

```
[alias]
  old = for-each-ref --sort=committerdate --format='%(refname:short)' refs/heads/
```

##### Deleting a single branch

When I know I don't want a branch locally or on the remote server anymore, I use this function to delete it in both places:

```
function gdel { git branch -D $1; git push origin :$1; }
```
