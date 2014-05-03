---
layout: post
title: Rails CMS choices
date: 2009-10-01
comments: true
categories: [Ruby, Rails]
---

Fewer CMS choices exist in the Ruby world compared with PHP. The choices that do exist vary in quality of UI, code, and their gems/plugins selections. Our evaluation of Rails CMS choices did not produce a clear winner. We downloaded each from github, installed the app and required gems. We considered code quality, documentation and support, usage of modern gems and plugins, how easy it was to add static and dynamic pages or code to the core, and how easy the UI was to understand (subjective). 

My colleague and myself have experience with Radiant, so we were primarily comparing the others against Radiant. Maintainers of the CMS will be 2 Rails developers. We have 1 designer, and several non-technical content authors. Content entry needs to be easy for our team. A workflow system would not be utilized.

Evaluated these
----

[Radiant CMS](http://radiantcms.org/)
---
 - Clean administrative UI
 - Active development (September 2009)
 - A volunteer group I was part of built [americas.org](http://americas.org) with Radiant. Building HTML/CSS templates outside of Radiant first is highly recommended. We noticed varying levels of Radiant plugin quality/maintenance. Radiant seems to be flexible enough and has a usable UI, though it could be fairly heavyweight for a small project or team. It is under active development.
  

[Adva CMS](http://adva-cms.org/)
---
 - Seems promising, documentation lacking (August 2009)
 - The Rails engines approach is interesting. UI is nice.


[Browser CMS](http://www.browsercms.com/)
---
 - Workflow features, would be overly complicated for our team.
 - Has the most impressive way of editing content visually.
  

[Refinery Content Manager](http://refinerycms.com/)
---
 - Simple UI
 - Refinery code is within a Rails app as a plugin

[RubyFlow](http://github.com/Sutto/rubyflow)
---
 - The source code behind RubyFlow and other sites by Peter Cooper, could be useful for a news site but probably not a CMS contender.


Interesting, but was not able to evaluate these
----

[Zena](http://zenadmin.org/)
---
 - Multilingual may be useful for you. Originally developed in Rails 1.2 timeframe.

[Seed](http://github.com/desaperados/seed) CMS
---
 - Good out of the box styling
 

Other possible solutions
-----
These choices are perhaps older or less supported, but may be worth considering. 

 - [Railfrog CMS](http://www.railfrog.com/)
 - [Comatose](http://comatose.rubyforge.org/)

If very minimal editing is necessary, [Static](http://github.com/trevorturk/static) may work. Made for easy deployment on Heroku, which does not offer local file storage (outside of `/tmp`), so configuration of an Amazon S3 account is necessary to store uploads. Simple code, zero UI, a starter app.

If editing on the web is not necessary at all, [Marley](http://github.com/karmi/marley) may be an option for your team or company.

[Nesta](http://effectif.com/nesta) is built on the Sinatra Ruby framework.

Finally, if your website isn't going to change frequently, and technical people can change it (check it out, make code/copy changes, deploy it), you might consider a static site generator. [Staticmatic](http://staticmatic.rubyforge.org/) lets you build a site with Rails view concepts using Haml and Sass.

I hope this list is useful as a starting point on picking a Rails-based CMS for your needs.

Update: 4/10/2010 [Rojo CMS](http://github.com/onomojo/rojo)
