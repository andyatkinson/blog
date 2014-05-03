---
layout: post
title: "5 Great Vim Plugins"
date: 2013-12-31 23:32
comments: true
categories: [Tools, Productivity]
---

 * [vim-vinegar](https://github.com/tpope/vim-vinegar) is a quick way (with `-`) to open the directory for the current file, using the built-in netrw.

 * [goyo](https://github.com/junegunn/goyo.vim) changes the way text is displayed, making it nicer for writing documentation and blog posts. I have `leader-z` toggle the goyo display.

 * [vim-airplane](https://github.com/bling/vim-airline) is a nice status bar.

 * [ctrlp-funky](https://github.com/tacahiroy/ctrlp-funky) is a plugin for CtrlP, which is a fuzzy finding plugin. I switched from Command-T to CtrlP and think it works better. `leader-p` brings up CtrlP, and `leader-b` brings up a MRU buffer list, which also supports fuzzy finding. A feature from Textmate I was missing was a list of function names, that I could fuzzy find on. The ctrlp-funky extension adds that functionality to CtrlP, which is great! I find it faster to type `leader-f cr` and `def create` to jump to the line where the "create" function starts.

 * [vim-sparkup](https://github.com/tristen/vim-sparkup) is nice for writing HTML snippets and expanding them. `C-e` expands `div.container` to `<div class="container"></div>`, puts the cursor in between the tag, and enters insert mode.
