---
layout: post
title: "Command Line Calendar Summary"
tags: [Tips, CLI]
featured_image_thumbnail:
featured_image: /assets/images/pages/andy-atkinson-California-SF-Yosemite-June-2012.jpg
featured_image_caption: Yosemite National Park. &copy; 2012 <a href="/">Andy Atkinson</a>
date: 2019-05-28
comments: true
featured: true
hidden: true

---

I set up [icalBuddy](https://hasseg.org/icalBuddy/) with my personal and work Google calendars (On OS X with Homebrew, run `brew install ical-buddy`), along with an alias `today`, to get a quick view of my calendar events for the day.

I've customized the output of certain data and formatting with this alias:

```
alias today='icalBuddy -f -iep "title,datetime" -po "datetime,title" -df "%RD" eventsToday'`
```

```
$ today

• Car appointment (wife's personal calendar)
• 12:00 PM - 12:15 PM
    Frontend stand-up meeting (work calendar)
• 12:15 PM - 12:30 PM
    Backend stand-up meeting (work calendar)
```
