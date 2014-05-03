---
layout: post
title: Auto-linking Twitter tweets in Ruby and Javascript
date: 2009-04-20
comments: true
categories: [Ruby, JavaScript]
---

Ruby on Rails introduced me to a the concept of an `auto_link` helper method, which finds and hyperlinks URLs within text. When working with Ruby in a different framework like Sinatra, I miss not having a `auto_link` helper. 

Twitter hyperlinks both URLs and usernames on their site. When fetching tweets via the Twitter API, results are in plain text. 

How does the Ruby or Javascript developer auto-link URLs and twitter usernames for their application then? Regular expressions to the rescue.

Ruby
----
As already mentioned with Ruby on Rails, `ActionView::Helpers::TextHelper#auto_link` handles URLs, but usernames need to be linked by the application developer. Duplicating the twitter style involves putting the "@" symbol immediately before the anchor tag, and linking the username. A Rails helper to do this, might look like:

``` ruby
  def auto_link_username(username)
    auto_link username.gsub(/@(\w+)/, %Q{@<a href="http://twitter.com/\\1">\\1</a>})
  end
```   

To test the helper in versions of Rails that include `ActionView::TestCase`, use `assert_match` with a regular expression to validate the hyperlinked username.

``` ruby
  require File.dirname(__FILE__) + '/../../test_helper'
  class TwitterHelperTest < ActionView::TestCase
    def test_auto_link_username
      tweet = "thanks @twitter, this is awesome."
      assert_match /@<a href=\"http:\/\/twitter.com\/\S+\">\S+<\/a>/, auto_link_username tweet
    end
  end
```

If you aren't using Rails, the following regular expression will hyperlink URLs.

``` ruby
  tweet = "have you seen this awesome search engine? http://google.com"
  tweet.gsub /((https?:\/\/|www\.)([-\w\.]+)+(:\d+)?(\/([\w\/_\.]*(\?\S+)?)?)?)/, %Q{<a href="\\1">\\1</a>}
```

JavaScript
----------
The regular expression methods are different in JavaScript than Ruby. I used the search and replace methods to check for the presence of a pattern, then update the tweet if the pattern was found. The "/g" option handles multiple usernames in one tweet.

``` javascript
  tweet = "this search engine from @google is awesome: http://www.google.com";

  if(tweet.search(/(https?:\/\/[-\w\.]+:?\/[\w\/_\.]*(\?\S+)?)/) > -1) {
    tweet = tweet.replace(/(https?:\/\/[-\w\.]+:?\/[\w\/_\.]*(\?\S+)?)/, "<a href='$1'>$1</a>")
  }

  if(tweet.search(/@\w+/) > -1) {
    tweet = tweet.replace(/(@)(\w+)/g, "$1<a href='http://twitter.com/$2'>$2</a>");
  }
```

Some of this code is present in my jQuery plugin for fetching tweets with Ajax called jquery-tweets. I hope this article taught you a little about regular expressions and auto-linking content in Ruby and JavaScript.
