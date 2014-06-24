---
layout: post
title: "Sharing rake tasks defined in a gem"
date: 2014-06-23 23:00
comments: true
categories: [Ruby, Tips]
---

This tip describes how to write a rake task in a gem, then use it in another Ruby gem or Rails app.

#### Create a rake task in a gem

Create a `lib/tasks` directory in your gem. Create a rake task there, with the same syntax it would have in the Rakefile. The file should have the `.rake` extension.

Now include the rake task in the Rakefile for the gem by using `import`. For example: `import "./lib/tasks/downloader.rake"`.

#### Use the rake task in another gem

In the second gem, create a Rakefile for the project and load the rake file with "load". To load the "downloader" rake file from the "corenlp" gem for example, include this snippet:

``` ruby
spec = Gem::Specification.find_by_name 'corenlp'
load "#{spec.gem_dir}/lib/tasks/downloader.rake"
```

Verify the task shows up when running `rake -T` and can be invoked as expected.

#### Use the rake task in a Rails app

We used "load" in the Rakefile for a Rails app, in the same way the gem instructions define including it in a gem. Working with [Railtie](http://api.rubyonrails.org/classes/Rails/Railtie.html) could be another way to include the task.

#### Conclusion

Rake tasks are a nice way to automate some work. Sharing them between Ruby apps keeps your code DRY. If you found this helpful let me know!

