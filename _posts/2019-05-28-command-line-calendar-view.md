---
layout: post
title: "Command line calendar summary"
date: 2019-05-28 13:00
comments: true
categories: [Tips, cli]
---

I set up [iCalBuddy](https://hasseg.org/icalBuddy/) with my personal and work Google calendars (On OS X with Homebrew, run `brew install ical-buddy`), along with an alias `today`, to get a quick view of my calendar events for the day.

I've customized the output of certain data and formatting with this alias:

`alias today='icalBuddy -f -iep "title,datetime" -po "datetime,title" -df "%RD" eventsToday'`

Which produces this output:

```
$ today

• Car appointment (wife's personal calendar)
• 12:00 PM - 12:15 PM
    Frontend stand-up meeting (work calendar)
• 12:15 PM - 12:30 PM
    Backend stand-up meeting (work calendar)
```
