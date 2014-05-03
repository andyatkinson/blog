---
layout: post
title: Rails 2.3 Features
date: 2009-07-29
comments: true
categories: [Ruby, Rails]
---

Some interesting feaures from Rails 2.3 that I wanted to highlight.

Templates
---------
Rails application templates are a way to put project configuration in a single file. Common setup chores like installing gems, plugins, JavaScript libraries, adding initializers, or writing custom rake tasks can be automated with Rails templates. 

Use `rails app -m mytemplate` at creation time or a template can even be applied to an existing project. Browsing templates on github is also a nice way to see which tools and techniques other developers are using.

Nested model forms
------------------
I have found creating and updating nested models to be problematic. My suspicion is that nested model forms will work better in the next major version of Rails. Using the feature now maximizes forward-compatibility.

Use seed data
-------------
Managing seed data in the conventional rails way makes it easier for new team members to figure out how to get development data to work with. 

`rake db:seed` and `rake db:setup` are new tasks to manage application data while the application code is being developed. Understand the difference between seed data and test fixture data.

I hope these tips help you out with Rails 2.3 and future versions!
