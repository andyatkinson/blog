---
layout: post
title: "Getting started with Go"
date: 2014-05-03 23:00
comments: true
categories: [Go, Programming]
---

I spent some time recently getting familiar with the Go language and building a small app. The first resource I recommend is the online book [An Introduction To Programming in Go](http://www.golang-book.com/). The book has 14 chapters, covers a variety of topics, and is really well done!

I typed out most of the go example code from the book for practice, and have [pushed my code here](https://github.com/andyatkinson/golang-book). One note &mdash; normally I keep source code in `~/Projects`, though it worked out easier to keep go source code in `~/go/src`.

The most useful way to learn a new programming language for me is to build a small program. I decided to make a URL shrinker like bitly, to learn how to make forms, post data, and interact with the MD5 package.

### Gournay

Gournay is a URL shrinker, the [source is on github](https://github.com/andyatkinson/gournay), and the app is deployed at [gournay.herokuapp.com](http://gournay.herokuapp.com/).

Deploying the app to Heroku was surprisingly simple, using the Go buildpack.

Go is a general purpose language, and the Introduction book has examples of building command line applications, and covers the concurrency features Go offers, which I'm planning to look at in more detail.
