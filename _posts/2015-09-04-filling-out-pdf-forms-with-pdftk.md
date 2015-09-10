---
layout: post
title: "Filling out PDF forms with pdftk"
date: 2015-09-04 13:00
comments: true
categories: [Programming, Productivity, Ruby]
---

At work we collect W9 forms from our independent contractor partners each year. This year we wanted to automate that process to reduce the burden on the operations team, as we've scaled up the number of active drivers on the platform.

#### Problem description

We needed to have our driver partners complete a IRS W9 form inside the driver app that they are already using. The driver app is used on a variety of iOS and Android devices, and has limited real estate. It is a hybrid app with a native wrapper but mostly composed of HTML/CSS/JS.

We evaluated some third-party solutions like HelloSign for this process. These solutions allow you to put together templated documents and collect input and signatures on various fields.

#### Solution

Ultimately we decided to roll it ourselves in house, because we had more control over the UX, and could optimize the minimal mobile phone real estate for our purposes.

The solution involved a regular web form, a PDF with fillable fields with specific identifiers, `pdftk` and the `pdf-forms` [^gem] gem. *Pre-Filling PDF Form Templates in Ruby-on-Rails with PDFtk* [^article] has code samples for Ruby classes to make nicer interfaces to working with the command line tool.

In our case I made a class that described the fields in the W9 form to be filled in, and the data coming from our database to use to fill those fields in.

Code and project links for this are coming soon.

#### Storing and serving the document

We use Amazon S3 for a lot of file storage, and for these documents, it was a good fit. We're able to use the bucket encryption feature, which means the image is stored encrypted at rest. The app uses HTTPS so traffic is encrypted in flight. Sensitive attributes (PII) are encrypted in the database as well.

After calling `pdftk` to create the PDF form, we upload the document to S3. Using an authenticated request with the S3 credentials in the app, the PDF can be displayed in the app.

The overall experience is pretty smooth.

### OS X Install

  * Install pdftk server tools. You will get the `pdftk` executable when this is complete.
  * Add the `pdf-forms` gem to your Gemfile
  * I used LibreOffice (open source, free) to create the fillable fields and export a PDF

#### Useful tools

 * `pdftk` has a useful option `dump_data_fields` that shows the fillable fields and values. You can run this before and after editing the PDF, and confirm the values that are set.
 * In LibreOffice, on a fillable field, right-click the field and choose "Control" to view or customize the name for the field.

Thanks!

[^gem]: [pdf-forms gem](http://github.com/jkraemer/pdf-forms)

[^article]: [Pre-Filling PDF Form Templates in Ruby-on-Rails with PDFtk](http://adamalbrecht.com/2014/01/31/pre-filling-pdf-form-templates-in-ruby-on-rails-with-pdftk/)
