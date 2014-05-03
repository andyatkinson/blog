---
layout: post
title: "Pair programming with wemux"
date: 2013-12-05 23:19
comments: true
categories: [Tools, Productivity]
---

[Wemux](https://github.com/zolrath/wemux) is a way to do remote pairing (collaborative code development) with less bandwidth, compared with a full graphical interface shared desktop experience. 

Remote pairing with wemux was one of the main motivations for me to improve my skills with VIM and learn tmux. With tmux I can have windows and panes dedicated to code, log file output, consoles, and more, and share all of that with a collaborator. 

In my case I'm using OS X. We used the following steps to set up a remote user that could connect to my tmux session.

 * Install tmux and wemux.
 * add a "pair" user in OS X, using the control panel. I gave the user an easy password.
 * in the "sharing" control panel, enable remote access for user "pair". I disabled access when we were no longer pairing.

At this point I was able to share my external IP address with a co-worker who was able to connect to my tmux session.

Wemux has a lot of features I hope to try out. If you're interested in pairing on some open source code, let me know!
