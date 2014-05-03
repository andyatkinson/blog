---
layout: post
title: JavaScript Zoom Effect for Small Photos
date: 2008-10-28
comments: true
categories: JavaScript
---

Many personal websites will display photos on the front page of the website, usually in a thumbnail size. Small photos provide context because they show several photos from a given photostream, however they can't provide much detail due to their small size.

To get more detail, a thumbnail may link to an information page where the photo lives, or link to a larger version of the same photo.  However these options encourage visitors to leave the site.  To retain site visitors, while giving them more detail, a popular effect is to provide a larger version of the photo when the photo is clicked, but keep the visitor on the site. This article compares a few ways of doing that if you want to add a similar effect to your site.

Lightbox
---
One popular approach is the [Lightbox JS](http://www.huddletogether.com/projects/lightbox/).  Lightboxes are modal windows, which means users cannot click outside the pop-up.  Lightboxes force the user to focus on the pop-up content by darkening the area that surrounds it.  Lightboxes generally let users navigate multiple items by keyboard, which makes them great for galleries or portfolio websites.  However Lightboxes have been criticized for slow load times.  

FancyZoom
----
Alternatives to Lightboxes take different approaches and have different tradeoffs. The next few libraries here animate the transition as the pop-up opens as well. This technique was pioneered by Cabel Sasser in his [FancyZoom](http://www.cabel.name/2008/02/fancyzoom-10.html) library. FancyZoom is a great alternative to Lightbox for some applications, though it has downsides addressed by the next library. Additionally, $39 is requested for FancyZoom when it is used on commercial websites.

FancyZoom in Prototype
-----------------
John Nunemaker made a [rewrite of FancyZoom using Prototype](http://orderedlist.com/articles/fancyzoom-meet-prototype). I already used Prototype and I find that the animation is snappier and more pleasing.  His version also has rounded corners and supports text and Flash movies embedded in pop-ups as well. Google hosts the Prototype and scriptaculous libraries which provides an additional speed improvement.  The [John Nunemaker FancyZoom rewrite](http://github.com/jnunemaker/fancy-zoom/tree/master) is open source and has a [demo site here](http://orderedlist.com/demos/fancy-zoom/).

A potential disadvantage of FancyZoom is that it requires all content to be loaded on the page.  Since there is no round trip to the server when photos are clicked, the pop-up animation is faster, but for sites with large images, it probably makes more sense to load images via ajax.

Highslide JS
----
The library I used before FancyZoom was [Highslide JS](http://highslide.com/). Highslide is loaded with features and supports basically everything I've mentioned so far and more, including the ability to move pop-ups around on the page, auto-play slideshows, and pause playback with the spacebar. The library is broken apart so users can remove pieces that are not needed, which helps reduce client download time. Highslide makes the best gallery in my opinion, since it supports loading large images via ajax, is keyboard navigable, easy to style, and returns the user to the original view after the last item is displayed.  

Check out the [Highslide examples](http://highslide.com/#examples) and [Barebones samples](http://highslide.com/index.htm). Highslide is free for non-commercial use.  Prices start at $29 for commercial websites.

Conclusion
-------
This article presented a few ways to display large images from thumbnails on the same site, and keep users on your site. Try out the alternatives to see which one works best for your project.
