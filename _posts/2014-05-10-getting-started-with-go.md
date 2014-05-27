---
layout: post
title: "Getting started with Go"
date: 2014-05-03 23:00
comments: true
categories: [Go, Programming]
---

I spent some time getting familiar with the Go programming language by working through some tutorials and building a small app. The first resource I recommend is [An Introduction To Programming in Go](http://www.golang-book.com/). The book has 14 chapters and covers data structures, HTTP, command line apps, concurrency, and more.

I typed out most of the go example code for practice and have [pushed my code here](https://github.com/andyatkinson/golang-book). Go has specific project layout requirements. The `GOPATH` environment variable for me points at `~/go` and project source code is in `src`. For more information refer to `go help gopath`.

To learn Go better, I slogged through making a small web app and deploying it to Heroku. This forced me to figure out how to handle form posts, make redirects, work with the MD5 library, and work with a database. The Heroku part started off easy [thanks to this guide](http://mmcgrana.github.io/2012/09/getting-started-with-go-on-heroku.html). However Heroku deploys failed for me with third-party dependencies like `pq` using [godep](https://github.com/tools/godep). I wasn't able to get godep working, but I did find the [gopack](https://github.com/d2fn/gopack) project, which serves a similar purpose, and have successfully deployed gournay to Heroku using gopack.

### Gournay

Gournay is a URL shrinker. The [source is on github](https://github.com/andyatkinson/gournay) and the app is deployed at [gournay.herokuapp.com](http://gournay.herokuapp.com/). Gournay depends on the `pq` package to connect to a postgres database, and `godep` to manage dependencies.

Gournay takes a long url like `http://www.npr.org/2014/05/17/313142425/a-worldwide-voyage-to-prove-stars-wind-and-waves-are-enough` and makes a short hash from it. The URL and hash are stored in a database table. If the hash is posted back at gournay, a HTTP redirect to the URL is issued. Pretty exciting stuff!

I am enjoying learning Go so far. If you have any other tips, or found this useful, please let me know.

### More resources

 * [Simple go webapp on Heroku](http://blog.joshsoftware.com/2014/02/28/a-simple-go-web-app-on-heroku-with-mongodb-on-mongohq/)
 * [gopack](https://github.com/d2fn/gopack) for dependencies
 * My [stack overflow godep issue](http://stackoverflow.com/questions/23745092/go-project-with-third-party-packages-on-heroku)
