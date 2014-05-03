---
layout: post
title: "Node Frameworks: Geddy and Express"
date: 2010-08-15
comments: true
categories: JavaScript
---

In preparation for the [Node Knockout](http://nodeknockout.com/) competition, which I will be participating in, I decided to look at two frameworks built on top of Node that make building applications easier. I’m looking at [Geddy](http://geddyjs.org/) and [Express](http://expressjs.com/). 

Geddy
---
Geddy has components that will be familiar to users of the Ruby on Rails framework: code is organized into model, view, and controller folders, it has a router that maps URLs to controller actions, and built-in generators to create new applications, models or controllers within an application. Geddy also includes ActiveRecord-style model validations.

I tried out the [2-minute geddy app](http://wiki.github.com/mde/geddy/the-two-minute-geddy-app) (accessible through the wiki), which demonstrates CRUD on a resource. Overall it worked well. Geddy told me on startup that my Node version was too old, so I built a newer version of Node from source which worked fine. I used SQLite as the data store. After creating the database with the geddy command, the geddy server wouldn’t start. I forgot to add [node-sqlite](http://wiki.github.com/mde/geddy/install-sqlite-and-node-sqlite) which allowed the server to start. Geddy includes support for other SQL database systems like Postgres and also includes support for CouchDB.

From there I was able to add the model fields, and create records, cool! I did not care for the markup and templating Geddy is using. If I used this in a project I’d investigate [haml-js](http://github.com/creationix/haml-js) for markup and something like [mustache.js](http://github.com/janl/mustache.js/) for templating. 

Geddy even includes an `assert` framework for [unit testing your application JavaScript](http://wiki.github.com/mde/geddy/writing-tests).

Express
---
If Geddy is Rails on Node, then Express aims to be Sinatra on Node. In other words, a lighter-weight framework, with the associated pros and cons of less framework code. 

Creating an Express app is more like creating and launching a plain Node app, whereas Geddy is a higher level of abstraction.

To get started with Express I recommend copying the directories `lib` and `examples/hello-word` out of the framework code into a new project directory. Express will be required this way, and you can start working on your application code.

The "upload" sample app in the Express framework source demonstrates using Haml and Sass for markup and style.

The Express documentation website doesn’t have anything on persistent server-side storage options (like SQLite or PostgreSQL) as of this writing. Depending on the application, perhaps an in-memory server-side JavaScript store would be fine. Or perhaps the application doesn't even need server-side persistent storage. Modern browsers have facilities for storing data in a key-value fashion, or even structured data and SQL querying, completely on the client side. Express might be a good option for these applications.

Let’s store some `SnowDog` objects (from the Geddy sample app) with Express as well, and just store them in memory.  Using the "hello-world" example app from the Express source as a starting point, the following `app.js` demonstrates adding SnowDog objects to memory and serving them to the view layer through the Express `locals` object.

``` javascript
    require('./lib/express')
        
    configure(function(){
      set('root', __dirname)
    })
    
    var MemoryDB = {
      snowdogs: [],
      add: function(snowdog) {
        this.snowdogs.push(snowdog);
      },
      all: function() {
        return this.snowdogs;
      }
    }
    
    function SnowDog(name) {
      this.name = name;
    }
    
    get('/', function(){
      
      var s1 = new SnowDog("bob");
      var s2 = new SnowDog("jane");
      
      MemoryDB.add(s1);
      MemoryDB.add(s2);
      
      this.render('front.html.ejs', {
        locals: {
          title: 'Hello World',
          name: 'Friendly user',
          items: MemoryDB.all()
        }
      })
    })
    
    run()
```
    
    
I hope that helps clarify what Geddy and Express are, how they are similar and different. Let me know if this was useful!
