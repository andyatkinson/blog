---
layout: post
title: "Building SMS and voice features for web applications"
date: 2015-02-12 20:00
comments: true
categories: [Programming, Ruby]
---

### Building SMS and voice features for web applications

At [OrderUp](http://orderup.com) we rely on voice calls and SMS messages to get information to customers and our rapidly growing team of delivery drivers. SMS messaging has some downsides but the big advantage over native push notifications is that we don't need to know the specific platform (iOS or Android) of the recipient device.

Twilio is a service that has a very rich API for sending SMS messages and making voice calls. We have been building features with Twilio for a while and it is working great. Each of the features described next were built with [Twilio](http://twilio.com/) and the [twilio-ruby](https://github.com/twilio/twilio-ruby) gem. API providers like [Tropo](http://tropo.com/) and [Nexmo](http://tropo.com/) also provide SMS and voice services.

##### SMS messages for new customers

Like many startups, we want to acquire new customers. To help out with that, we offer discounts for new customers, and try to ensure that a customer only receives the discount once.

Unfortunately fraudulent usage of this feature is a reality, so we have taken some steps to mitigate fraud. For one-time discounts, we have experimented with determining a unique, new customer, by having them respond to a SMS message with a unique code. This also helps ensure we have a phone number where we can contact the customer when they choose to receive messages.

Some of the basic steps to build the feature:

 1. Create a callback in the web application. For our Ruby on Rails application, this is a controller action. We have namespaced our webhooks controller actions. The controller action will receive a HTTP POST from Twilio and should take the params and do something with them.
 1. Create a twilio phone number and configure it with the callback URL. This can be done manually or progrmatically. There are separate callbacks for voice and SMS.
 1. In development, use [ngrok](https://ngrok.com/) or a similar tool to expose the local web server to the internet. During development it may be easier to use a separate phone number (they are priced as low as $1/month) to avoid forgetting to change the callback URL.

Now SMS messages can be sent to the customer, and replies will come in via the webhook.

##### Voice and SMS connecting drivers and customers with masking

 1. Create a callback in the web application.
 1. Create a twilio phone number and configure the callback.
 1. In development use ngrok or a similar tool to expose the local web development server to the internet.
 1. Using one of the Twilio numbers, for SMS messaging, when the driver sends a text to the Twilio number, look up the customer number and make a POST to twilio sending a message from the Twilio number to the customer. When the customer replies, do the same lookup but in reverse. In this case, using the from number (`params['From']`) from Twilio, determine the sender is the customer, and send a message to the driver. By building this in-house, we're also able to store records for all of this text communication, which is helpful for ensuring quality, both in the communication, and in the operation of the sytem.
 1. We implemented masking for voice calls differently. It will be covered in a future post.


##### Adding and releasing numbers via the Twilio API

* Writing either a script or some application code, query for Twilio numbers and for each one that matches the desired criteria, reserve it. We keep track of the Twilio number in our database so we can update it or release it later.
* To release a number, using the twilio-ruby gem, look up the `SID`, and send an HTTP DELETE request. Releasing the number removes it from the Twilio account. Because we can add and release numbers, we could do it very frequently if we wished to. For our particular implementation, we've taken advantage of this to dynamically increase the Twilio numbers we have based on usage by our driver team. We have idea for even more ways to dynamically adjust the numbers in use.
