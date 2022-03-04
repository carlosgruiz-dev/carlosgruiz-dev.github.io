---
title: "\"Hello World!\" Scala Restful Edition"
date: 2020-05-28T22:05:27-05:00
draft: true
---

Since I'm learning [Scala](https://www.scala-lang.org/) and a bit impatient, I want to step into a project to get used to the language's ecosystem. So my idea for this is to create a ["Hello, World!" program](https://en.wikipedia.org/wiki/%22Hello,_World!%22_program) but in a [RESTful](https://en.wikipedia.org/wiki/Representational_state_transfer) way. So, I'll try to find out how to create endpoints, use some HTTP verbs, use headers and URL parameters, and persist data. This, I think is a good starting point.

<!--more-->

## Some Frameworks

So, my first step is to look for some libraries and frameworks to do the job. A googled a lot about Scala for these days, and for web applications these are common answers:

- [Play Framework](https://www.playframework.com/): This is a big framework, it looks like an equivalent of [Django](https://www.djangoproject.com/) for Python or [Spring](https://spring.io/) for Java (maybe competitors here, but since I'm going to use Scala it's ok). It has good documentation, tutorials, and commercial support. I'll give it a try later on..
- [Scalatra](https://scalatra.org/): This micro framework it looks very neat, it has a Manning book in progress, good documentation, a Giter8 template, and some examples. Something I specially like from documentation is the deployment chapter, from the settings for standalone deployments, to Heroku and Google App Engine.
- [Finatra](https://twitter.github.io/finatra/)
- [Akka HTTP](https://github.com/akka/akka-http)
- [Cask](http://www.lihaoyi.com/cask/)
- [tAPIr](https://tapir.softwaremill.com/)
- [Lagom Framework](https://www.lagomframework.com/)

