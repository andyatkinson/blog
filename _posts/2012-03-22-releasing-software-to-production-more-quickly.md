---
layout: post
title: Releasing software to production more quickly
date: 2012-03-22
comments: true
categories: [Ruby, Rails, Productivity]
---

Releasing software to production can yield findings (A/B test results, feature usage, conversion on a metric the feature enables) more quickly, which can inform whether to invest further in a feature. Having a goal on a team that is shared of prioritizing shipping software (as opposed to planning, or a large suite of features instead of one or two simple ones) can help keep conversations productive. What follows are some ways to release code while reducing risk to revenue, a broken site, or a bad user experience.

Conditionally show the feature
-------------
 * Show a feature if a URL parameter is present. It could be `?show_feature=1` appended to the URL, just the presence of the flag could be checked, or the value could be checked if multiple values were going to be used.
 * Show feature to employees only. For logged-in users, check their email domain. If the email domain matches your company email domain, you can conclude the user is an employee and show them the feature. Additionally, you could check their role if you have a role-based authorization system in place. Releasing a feature just to the "engineer" or "product manager" role for example.
 * On a particular page, show the feature to users that meet certain criteria. In our case we can show a feature to users that subscribe to deals in a particular city, are viewing a specific deal or a specific category, have a home address in a particular city, or are browsing with a particular language selected. 
 * Add a cookie for some visitors and show a feature if the cookie is present. We might write a cookie that lasts for a week to avoid showing a feature to the same user (in the same browser) during the week the cookie is present. A cookie means there is less to evaluate on the server, and the cookie can be set to expire automatically by the browser.
 * Show a feature to a user that is part of a cohort of behavior you want to target: heavy subscribers, heavy purchasers, heavy sharers, heavy users of external social networks.

Reducing risk
------------- 
Risk for a particular feature can be reduced by releasing the feature to a small group initially, then gradually increasing the size of the group. However another type of risk is performance, which in the case of our application are most often in the form of database queries that run too slow. 

In this case one technique is to wrap certain code in conditional blocks that reference variables that can be kept external to the code, in a configuration file for example (this could also be environment variables). The values might be true or false to show or hide a feature, a numerical value for a time-to-live on a cache, or a datetime value that describes when a feature should be disabled or enabled.

With the external configuration file driving the values of these variables, the file can be modified locally by developers, and changed in production by deploying a new version of the file.

Show the feature to a portion of the traffic
--------------------------------------------

Another strategy is to reduce the percentage of users that are eligible to see feature. Start with a low number and verify things are working then increase it in steps (25% of visitors, 50% of visitors etc.). In Ruby, you could have a helper method that is modified from `rand(3) == 0` (25%) to `rand(2) == 0` etc as needed. A Ruby gem for conditionally releasing features that may be useful for your project is [rollout](https://github.com/jamesgolick/rollout).

I hope some of these tips are useful for your to help release your feature, get buy-in from your team, and get answers from your users more quickly.
