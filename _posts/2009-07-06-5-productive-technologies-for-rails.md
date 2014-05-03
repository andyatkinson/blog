---
layout: post
title: 5 Productive Technologies for Rails
date: 2009-07-06
comments: true
categories: [Ruby, Rails]
---

This article attempts to recommend some extra good stuff in Rails to help you be even more productive.

1. For scaffold and layout code, I prefer [nifty generators](http://github.com/ryanb/nifty-generators) (from Ryan Bates) over the built-in generator. Nifty generators produce more attractive and usable markup and CSS and provide convenient view helpers. Nifty generators can generate Haml views initially, saving the developer from manually converting Erb views to Haml.

2. Use [shoulda](http://thoughtbot.com/projects/shoulda/) for model and controller testing instead of Test::Unit. Tests are easier to read and macros like `should_validate_presence_of :name` are time savers. Contexts provide a natural grouping mechanism.

3. Use [make resourceful](http://mr.hamptoncatlin.com/) on controllers when possible. Generated RESTful controllers with low customization are prime targets. 7 generated methods can be replaced with one make resourceful method call. Make sure to thoroughly understand the method code that is being replaced.

4. Use [semantic form builder](http://github.com/rubypond/semantic_form_builder) instead of presentational markup to style forms in views. For a slight loss in flexibility, the application gains consistency and sheds view code weight. Stop wrapping form elements in `<p>` and `<span>` tags across all the views and do it in a single spot instead.

5. Use [Haml](http://haml.hamptoncatlin.com/) and [Sass](http://sass-lang.com/). I prefer Haml and Sass to Erb and CSS because terse view code is easier to maintain. The upfront cost is solving lots of indentation problems while learning Haml, and getting all team members on board with both Haml and Sass.

Update 2013: I no longer use or recommend any of these technologies.
