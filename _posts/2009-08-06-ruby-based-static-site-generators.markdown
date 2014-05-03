---
layout: post
title: 5 Ruby-based static site generators
date: 2009-08-06 16:06
comments: true
categories: [Ruby, Tools]
---

Developing dynamic database-driven web applications with Ruby on Rails is great, however the flexibility and overhead of the framework is not always needed for small static websites.

Pros
----
Static sites have some nice advantages. Pages are served from memory or disk by the web server, no other processes are involved. No deployment infrastructure (database, queue, background processing, etc.) is required. Before converting a site to a CMS like Radiant with proprietary concepts like "page parts" and "snippets", a static site is typically developed anyway. Converting that site into the format the CMS requires represents work that could be saved, and skipped, with a lightweight static site framework that more or less uses the static HTML pages from initial the front-end development. 

Dynamic parts of a site like commenting or search can often be replaced with third party services and included with JavaScript. 

Cons
----
On the negative side, static site generators require command line interaction and editing content in text editors, which may or may not work for a project or team.

Ruby-based static site generators will feel familiar to Rails developers. Some adopt naming conventions from Rails, have Rake and `yml` files for configuration, and may use Haml. Most of these come with generators to create new pages. The best part is that your pages stay DRY because all of these tools use things like layouts and partials to reuse common design elements.

Here is a brief overview of some Ruby-based static site generators.

[Webgen](http://webgen.rubyforge.org/)
----

 - Has a rake task to continually rebuild HTML files from source, but does not offer a built-in web server
 - Erb, Markdown, Textile and Haml

Does not come with much CSS so pages look poor initially. Tried this first and most of the following options seemed better.

[Nanoc](http://nanoc.stoneship.org/)
----

 - Has a web server that can rebuild HTML pages
 - Development happens in a Mercurial repository
  
Metadata is maintained in a separate file. After using Jekyll, storing file metadata in a separate file seems unnecessary and confusing to me. Has had a couple major releases. Liked this better than webgen.

[Staticmatic](http://staticmatic.rubyforge.org/)
----

 - *Only* supports Haml
 - Has a built-in server to generate HTML and serve files
 - Uses some of the same HTML helper names as Rails, for example `link_to`
  
Staticmatic is opinionated. I liked this better than either webgen or nanoc. If you don't use Haml, you will have to look elsewhere, I suggest Webby. I was up and running in the least time with staticmatic.
  
[Webby](http://webby.rubyforge.org/)
----

 - Erb and Textile by default, Haml and Markdown are optional
 - Comes with Rake tasks for deployment
 - Source code highlighting
 - Blueprint CSS framework support
  
Mike Clark has written a lengthy overview of [Webby](http://clarkware.com/cgi/blosxom/2008/08/06#Webby). Webby supports other features like TeX and graphing tools, which may be of interest.
  
[Jekyll](http://github.com/mojombo/jekyll)
----

 - Supports migrating from other platforms like Movable Type and Typo
 - Jekyll used daily in the real world by powering Github Pages
 - Source code highlighting


Summary
---
Staticmatic, Webby, and Jekyll are the best options based on my criteria. Webby has more features and has been around longer. Jekyll works locally or can be used through Github pages.

After spending a few minutes and doing basic testing with each, I prefer Staticmatic for static webpage development where I'm building out a site in Haml quickly. As a blogging tool (adding new pages of text copy), or if composing text in Markdown or Textile is important, Webby or Jekyll are better options.

I hope this summary is useful to you. Try out the different tools and figure out which one works best for you.
