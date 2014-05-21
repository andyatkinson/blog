---
layout: post
title: "Essential Ruby gems for Rails"
date: 2014-05-21 23:00
comments: true
categories: [Ruby, Rails, Tips, Programming]
---

This is my recommend list of Ruby gems for all Rails web apps.

### Debugging

[pry](https://github.com/pry/pry) works really well for debugging. Add a `require 'pry'; binding.pry` where you want execution to stop and get a full IRB/Rails console session at that point. Pry can also be used as a traditional stepping debugger.

### Background processing

Code that blocks the user, takes more than 250ms to execute, or takes up a lot of resources, should be run from a background job. We have used Resque in production extensively, though we have also used [Sidekiq](https://github.com/mperham/sidekiq) in production and it seems better supported. Sidekiq uses less memory as well.

### Exception notification

The [exception_notification](https://github.com/rails/exception_notification) gem is an easy way to notify the whole engineering team when an application exception is raised. We specify the email as a distribution list so everyone has a chance to be notified as soon as possible after the exception occurs. We try to write, test, and deploy a quick fix for production issues.

### Factory objects for automated tests

Rails' built-in fixtures are fine for objects that don't change. Fixtures are loaded once at test boot time, which will be useful for some types of tests. For objects that require specific configuration, we have found the factory approach to work well. [factory_girl](https://github.com/thoughtbot/factory_girl) makes it easy to set up re-usable factory objects. Both Fixtures and Factories need to be kept up to date with schema changes. Instead of mocking our own code, we prefer to have a factory object set up in the configuration the code under test expects.

### Authentication

If the authentication needs for the app are conventional or not specified, [devise](https://github.com/plataformatec/devise) works well as a drop-in authentication solution. Among many nice features, Devise provides templates and issues emails to users for various lifecycle events (registration, forgot password, etc.).

### File uploads

[paperclip](https://github.com/thoughtbot/paperclip) has been under development for many years and has worked well in many Rails web applications. Typically we configure paperclip to store file uploads in S3. File uploads could be profile avatars or any file-based artifact associated to a user in the database.

### Periodic jobs

For periodic jobs, cron is the UNIX tool of choice. The only issue is that the crontab file syntax isn't very intuitive. While not strictly necessary, we have found the [whenever](https://github.com/javan/whenever) gem to be helpful, because it allows us to express the job details in a more English-like syntax, as well as a conventional way to add cronjobs to an app. Whenever provides a command to generate the crontab output, as well as capistrano hooks and code to update the production crontab file on deploy.

What are your essential Ruby gems for Rails apps? Please leave a comment or get in touch by email. Thanks for reading!
