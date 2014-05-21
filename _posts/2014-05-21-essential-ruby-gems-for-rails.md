---
layout: post
title: "Essential Ruby gems for Rails"
date: 2014-05-21 23:00
comments: true
categories: [Ruby, Rails, Tips, Programming]
---

This is my recommend list of Ruby gems for all Rails web apps.

### Debugging

[pry](https://github.com/pry/pry) works really well for debugging. Add a `require 'pry'; binding.pry` where you want execution to stop. When the breakpoint is hit, a full Rails console is available. Pry can also be used as a traditional stepping debugger.

### Background processing

Code that blocks the user or takes more than 250ms to execute should be run from a background job. We used Resque in production at LivingSocial extensively. We also used [Sidekiq](https://github.com/mperham/sidekiq) in production on another project. For new projects, Sidekiq seems like a better choice because of the support options and active code development. Sidekiq uses less memory as well.

### Exception notification

The [exception_notification](https://github.com/rails/exception_notification) gem is an easy way to notify the whole engineering team when an application exception is raised. We try to write, test, and deploy a quick fix for production exceptions as soon as we find out about them.

### Factory objects for automated tests

Rails' built-in fixtures are fine for objects that don't change. Fixtures are loaded once at test boot time, which will be useful for some types of tests. For objects that require specific configuration, we have found the factory approach to work well. [factory_girl](https://github.com/thoughtbot/factory_girl) makes it easy to set up re-usable factory objects. Instead of mocking our own code, we prefer to have a factory object set up in the configuration the code under test expects. Another advantage of this approach is that the factory object serves as documentation of a specific configuration of objects the app uses.

### Authentication

If the authentication needs for the app are conventional or not specified, [devise](https://github.com/plataformatec/devise) works well as a drop-in solution. Among many nice features, Devise provides templates and issues emails to users for various lifecycle events (registration, forgot password, etc.).

### File uploads

[paperclip](https://github.com/thoughtbot/paperclip) has been under development for many years and has worked well in many Rails web applications. Typically we configure paperclip to store file uploads in S3. File uploads could be profile avatars or any file-based artifact associated to a user in the database.

### Periodic jobs

For periodic jobs, cron is the UNIX tool of choice. The only issue is that the crontab file syntax isn't very intuitive. While not strictly necessary, we have found the [whenever](https://github.com/javan/whenever) gem to be worthwhile, because it allows us to express the job details in a more English-like syntax. Whenever also provides a pattern for specifying cronjobs in an app, as opposed to a unique solution app-to-app. Whenever provides a command to generate the crontab output, as well as capistrano hooks and code to update the production crontab file on deploy.

What are your essential Ruby gems for Rails apps? Please leave a comment or get in touch by email. Thanks for reading this post!
