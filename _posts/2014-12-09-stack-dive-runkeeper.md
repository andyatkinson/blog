---
layout: post
title: "Stack Dive with RunKeeper"
date: 2014-06-23 23:00
comments: true
categories: [Programming, Productivity]
---

Doug Williams and Joe Bondi from [RunKeeper](http://runkeeper.com/) gave a technical talk at the WeWork Boston South Station office in December 2014. The talk explored the technical stack that supports the app and web site, as well as tools and processes that have worked well for their team. RunKeeper has huge growth, currently at 38.5 million users, using their native mobile apps in the US and around the world.

One of the technical challenges they have faced with apps around the world is translating the app into many languages, and various levels of quality and accuracy for cellular service and position information.

Users in China has been a big part of their growth, since the app has been translated into Mandarin.

#### Techniques on the devices

One thing they discussed was that they needed to show users geo coordinates in the app. In order to keep the app performing well, they have implemented queues and workers on the device itself, in addition to the queues and workers on the back-end. Another interesting thing I thought was that moved away from storing geo coordinates in postgres, and replaced that solution with one that stores coordinates posted to the server, as rows in a log file (encoded as JSON). The log file is pushed to S3. This way consumers of that file can read log files from there, access can be controlled, and the files can even be served on the web. S3 has been reliable and very high-performance for them.

They also recommended using native push notifications on devices over SMS, and said there are a lot of inexpensive services now that provide that. In general their move has been from a traditional data center to more cloud services.

The talk was filled with recommendations for various services that have worked well.

Here are some of the services that have worked well for RunKeeper:

   * [SmokePing](http://oss.oetiker.ch/smokeping/)
   * [Vessel.io](https://www.vessel.io/) -- a/b testing
   * [Beta by Crashlytics](http://try.crashlytics.com/beta/) -- beta distributions for iOS and Android.
   * [Applause](http://www.applause.com/) -- QA, app testing, distributed external manual testing services. Very highly recommended.
   * [Smartling](http://www.smartling.com/) -- Translation services, highly recommended.
   * [GM Voices](http://www.gmvoices.com/) -- voice prompts, IVR.
