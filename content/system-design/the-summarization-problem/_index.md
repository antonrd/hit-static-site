---
title: "The Summarization Problem"
type: docs
weight: 60
no_list: true
aliases: ["/classrooms/system-design/lesson/101"]
---
Here is another example problem from a system design interview. Like with [The Twitter Problem](/system-design/the-twitter-problem/), we will start with a statement and then go through things like clarifying questions, designing the software architecture and resolve any issues that it may have.

### Statement

Imagine you are at a tech interview and you are asked the following:

<blockquote><p>"In our company we already have developed a great library that can be used to summarize text articles. Just feed it the whole text and it will return a decent summary that is just a few sentences long.</p>

<p>We need to put this in production and make it scalable. We expect that our customers will submit text articles from our mobile app and also from our website.</p>

<p>The library currently takes between 0.1 and 5 seconds to summarize an article. You need to design a system that uses our existing library and allows users to submit text articles through the mobile app and through the website.</p>

<p>We anticipate that this service will be used around 1 million times a month. Our desire is to not respond in more than 10 seconds to each request."</p></blockquote>

Let’s see what system design we can build here...
