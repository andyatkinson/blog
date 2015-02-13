---
layout: post
title: "Building SMS and voice features for web applications"
date: 2015-02-12 20:00
comments: true
categories: [Programming, Ruby]
---

At [OrderUp](http://orderup.com) we rely on voice calls and SMS messages to get information to our customers and our team of delivery drivers. SMS messaging has some downsides but has a big upside over native push notifications in that we don't need to know the specific platform or capabilities (iOS or Android) of the recipient device. It Just Works &#0153; (most of the time).

[Twilio](https://www.twilio.com/) (and the [twilio-ruby gem](https://github.com/twilio/twilio-ruby)) are great tools. Twilio has a rich API and tons of documentation to build SMS and voice services for a variety of use cases. [Tropo](http://tropo.com/) and [Nexmo](http://nexmo.com/) offer similar services to Twilio.

##### SMS messages for new customers

Like many startups, we want to acquire new customers. To help out with that, we offer a discount for new customers, and try to ensure a customer receives the discount only once.

For fraud mitigation of sign-up discounts, we have experimented with using a verified phone number as a unique identifier. This also helps ensure we have a number we can SMS to, which some customers may prefer over email as a way to be notified.

Some of the basic steps to build the feature:

 1. Create a callback in the web application. For our Ruby on Rails application, this is a controller action. We have namespaced our webhooks controller actions. The controller action receives a HTTP POST from Twilio and uses the params to determine what to do next.
 1. Create a Twilio phone number and configure it with the callback URL. This can be done manually or via the API. Separate callbacks can be configured for voice and SMS.
 1. In development, use [ngrok](https://ngrok.com/) or a similar tool to expose the local web server to the Internet. It may be easier to use a separate phone number (they are priced as low as $1/month) to avoid forgetting to change the callback URL.

Now SMS messages can be sent to the customer, and replies will come in via the webhook. Twilio offers logs of inbound and outbound message activity for a number.

##### Voice and SMS connecting drivers and customers with masking

 1. Create a callback in the web application.
 1. Create a Twilio phone number and configure the callback.
 1. In development use ngrok or a similar tool to expose the local web development server to the Internet.
 1. Using one of the Twilio numbers, for SMS messaging, when the driver sends a text to the Twilio number, look up the customer number and make a POST to Twilio sending a message to the customer. When the customer replies, do the same lookup but in reverse. In this case, using the from number (`params['From']`) from Twilio, determine the sender is the customer, and send a message to the driver. Another benefit of the messaging passing through the web application is that it can be stored for use later.

We implemented masking for voice calls differently. It will be covered in a future post.

##### Adding and releasing numbers via the Twilio API

* Writing either a script or some application code, query for Twilio numbers and for each one that matches the search criteria, reserve it. We keep track of the Twilio number in our database so we can update it or release it later. We're also able to register local numbers for each of our markets due to the large number of phone numbers available through Twilio.
* To release a number, look up the `SID`, and send an HTTP DELETE request via the API. We have taken advantage of easily adding and releasing numbers to dynamically increase the Twilio numbers we are using based on demand in our app.

Due to the real-time nature of the food ordering business, it is critical to be able to quickly and effectively communicate with customers and team members. If your project has needs like this, consider building-in support for SMS and voice services.

Thanks!
