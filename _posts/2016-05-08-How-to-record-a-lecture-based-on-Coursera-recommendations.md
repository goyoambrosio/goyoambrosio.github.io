---
title: " How to record a lecture based on Coursera recommendations"
categories:
  - HowTo
tags:
  - coursera
  - learning
  - lecture
  - recording
  - studio
---

![Lecture recording](/assets/images/2017/02/lecture-recording.jpg | width=100){: .align-left} As many of you know, [Coursera](http://www.coursera.org/) is an educational technology company that offers massive open online courses (MOOCs). Coursera works with [universities and other organizations](https://www.coursera.org/about/partners) to make some of their courses available online, offering courses in very different subjects.

After taking several courses, I have been curious about the technologies Coursera uses in its platform. After surfing the Internet I've discovered some info related to the Coursera´s stack and about the recording of lectures.

## The Coursera's stack

I'm not sure if this information is very up to date, but I've read from some sources that Coursera's platform uses a mix of [PHP](http://www.php.net/) and [Python](https://www.python.org/) running on [MySQL](https://www.mysql.com/).  The front-end website is built entirely on [Backbone.js](http://backbonejs.org/), with backend services provided by accessing an API layer written mostly in Python/[Django](https://www.djangoproject.com/) and backed by MySQL. There are also other back end services running in a variety of different languages. On the other hand they are moving away from the legacy PHP stack into [Scala](http://www.scala-lang.org/) for better modularization and scalability. You might also be interested in this article [Why we love Scala at Coursera](http://tech.coursera.org/blog/2014/02/18/why-we-love-scala-at-coursera/) written by Brennan Saeta, infrastructure engineer at Coursera.

In addition, Coursera's platform utilizes [Amazon AWS](https://aws.amazon.com/) services quite heavily, using S3, EC2, SES, SQS, CloudSearch, CloudFront and RDS, among others.
