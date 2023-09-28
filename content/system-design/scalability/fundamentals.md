---
title: "Fundamentals"
type: docs
weight: 10
aliases: ["/classrooms/system-design/lesson/60", "/system-design/scalability-fundamentals"]
---
Now that you've designed a solid abstract architecture, the next step is to take it to scale. If you've never built a large-scale system, this task may seem a little daunting.

### Where do you start?

There is a common set of scalability principles that you need to know. Knowing what they are, understanding how they are used, and being able to discuss their pros and cons is what scalability at interviews is all about.

How do you build up that intuition?

The first thing we’d recommend you to do is watch this video:

<div class="row">
<div class="col-md-8 col-md-offset-2">
<div class="embed-responsive embed-responsive-16by9 text-center">
{{% youtube -W9F__D3oY4 %}}
<!-- <iframe class="embed-responsive-item" allowfullscreen="" frameborder="0" height="315" src="//www.youtube.com/embed/-W9F__D3oY4" width="560"></iframe> -->
</div>
</div>
</div>
<br>
In it, professor David Malan from Harvard is teaching a huge part of the intuition you will need to have when it comes to scalability. So start here, watch the video and make sure you understand it well.

After watching it, you should have a good fundamental understanding of the following concepts:

- Vertical scaling
- Horizontal scaling
- Caching
- Load balancing
- Database replication
- Database partitioning

Next, we recommend reading a great 4-post “Scalability for Dummies” tutorial, which is linked <a href="https://github.com/donnemartin/system-design-primer/blob/master/README.md#step-2-review-the-scalability-article" target="_blank" rel="noopener noreferrer"> here</a>. It reiterates on some of the topics mentioned above, but also introduces several important new concepts:

- Using NoSQL instead of scaling a relational database
- Being asynchronous

You would also know how to deal with the two major bottlenecks: handling a lot of users, and handling a lot of data.

Finally, you may want to read <a href="http://highscalability.com/blog/2009/8/6/an-unorthodox-approach-to-database-design-the-coming-of-the.html" target="_blank" rel="noopener noreferrer">this tutorial on Database sharding</a>. It's a very common and powerful way of database scaling (as you learned from prof. Malan's lecture).

### What's next?

Now you're ready to start looking at some real-life architectures to see how these principles are applied in practice.
