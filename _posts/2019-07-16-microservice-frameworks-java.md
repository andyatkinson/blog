---
layout: post
title: "Microservice Frameworks for Java"
tags: [Tips, Java]
date: 2019-07-16
comments: true
---

A quick look at two Microservice Frameworks for Java.

## Dropwizard

[Dropwizard](https://www.dropwizard.io) is a lightweight (for Java) [^1] framework to build microservice back-ends with Java.

> Dropwizard is a Java framework for developing ops-friendly, high-performance, RESTful web services. <cite>dropwizard.io</cite>

I became aware of Dropwizard as an engineer at Groupon, where it is used as the basis of the official way to develop Java microservices, and is in heavy use. I know has been in use at Hubspot in the past as well, and perhaps other startups that may have started with a Rails monolithic app, that was broken up into microservices over time.

There seems to be a Ruby-to-Java history as well [^2] with the Coda Hale/Yammer background. This slide [^3] shows roughly equivalent Rails and Dropwizard functionality.

I made a [Hello World Dropwizard App](https://github.com/andyatkinson/dropwizard-hello-world) to get a sense for developing with it, and [deployed it to Heroku](https://hello-world-dropwizard.herokuapp.com/hello-world?name=andy). I found Dropwizard to be ok to use, maybe not the "Joy" of Sinatra and Ruby, but relatively lightweight for Java, and with very fast performance.


## Javalin

[Javalin](https://javalin.io/) is described as:

> A simple web framework for Java and Kotlin

I made a [Hello World App with Javalin](https://github.com/andyatkinson/javalin-hello-world) and [deployed it on Heroku](https://javalin-hello-world-andy.herokuapp.com/), as a comparison with Dropwizard, in search of the lightest weight Java web framework.

I found it easy to use, and having even less code and setup compared with Dropwizard. For a very small API, if I was using Java, I'd consider implementing it with Javalin. If I was starting from scratch, I'd probably choose Kotlin over Java as well!

#### Wrapping Up

There are loads more Java microservice frameworks out there. What is your favorite one and why?


[^1]: Ruby frameworks like Sinatra are much lighter/less lines of code to get going
[^2]: [Dropping Rails for Dropwizard](https://speakerdeck.com/bmorton/dropping-rails-for-dropwizard-from-abril-pro-ruby-2014?slide=2)
[^3]: [Slide title: What does an application look like?](https://speakerdeck.com/bmorton/dropping-rails-for-dropwizard-from-abril-pro-ruby-2014?slide=22)
