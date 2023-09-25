---
title: "Examples"
type: docs
weight: 20
aliases: ["/classrooms/system-design/lesson/61"]
---
The awesome thing about scalability is that it's all around us. If you want to work on an exciting and successful product or service, by definition it's going to have to operate at scale.

Many of the web's largest websites have been very open about how they scale. It's extremely interesting to look "under the hood" of Instagram, Salesforce.com, TripAdvisor, Twitter, Google, and many, many others. That's exactly what we'll be doing in this section.

The goal is to show you how the theoretical principles from the previous section are applied in practice, as well as to introduce you to some of the real-life technologies many companies use nowadays.

### Let's get going!

The <a href="http://highscalability.com/" target="_blank" rel="nofollow noopener noreferrer">HighScalability blog</a> is our favorite resource for reading about scalability. Here are some real-life architectures we'd recommend you read, analyze and understand:

- <a href="http://highscalability.com/blog/2017/10/23/one-model-at-a-time-integrating-and-running-deep-learning-mo.html" target="_blank" rel="nofollow noopener noreferrer">Deep Learning in production</a>: Great story about how EyeEm built their production system running multiple deep learning models on huge amounts of images
- <a href="http://highscalability.com/blog/2016/10/12/lessons-learned-from-scaling-uber-to-2000-engineers-1000-ser.html" target="_blank" rel="nofollow noopener noreferrer">Uber</a>: A nice article about how Uber had to scale fast, about breaking your service into many micro services spread across many repos
- <a href="http://highscalability.com/blog/2016/6/27/how-facebook-live-streams-to-800000-simultaneous-viewers.html" target="_blank" rel="nofollow noopener noreferrer">Facebook</a>: How Facebook handles 800,000 simultaneous viewers on a live stream
- <a href="http://highscalability.com/blog/2016/6/15/the-image-optimization-technology-that-serves-millions-of-re.html" target="_blank" rel="nofollow noopener noreferrer">Kraken.io</a>: How to scale image optimisation at a large scale, this article will look in more detail at some specific hardware solutions used, as well as deployment, monitoring and other important aspects
- <a href="http://highscalability.com/blog/2016/4/20/how-twitter-handles-3000-images-per-second.html" target="_blank" rel="nofollow noopener noreferrer">Twitter</a>: How Twitter handles 3,000 image uploads per second and why the old ways it used would not work nowadays
- <a href="http://highscalability.com/plentyoffish-architecture" target="_blank" rel="nofollow noopener noreferrer">PlentyOfFish</a>: A great example of what a single engineer can achieve in terms of scalability
- <a href="http://highscalability.com/blog/2013/9/23/salesforce-architecture-how-they-handle-13-billion-transacti.html" target="_blank" rel="nofollow noopener noreferrer">Salesforce</a>: A relatively short example from Salesforce.
- <a href="http://highscalability.com/blog/2013/11/4/espns-architecture-at-scale-operating-at-100000-duh-nuh-nuhs.html" target="_blank" rel="nofollow noopener noreferrer">ESPN</a>: Another awesome and thorough example, this time from the digital media industry.
- Finally, some good example of Twitter subcomponents: Storing data (<a href="http://www.youtube.com/watch?v=5cKTP36HVgI" target="_blank" rel="nofollow noopener noreferrer">video</a>&nbsp;|&nbsp;<a href="http://highscalability.com/blog/2011/12/19/how-twitter-stores-250-million-tweets-a-day-using-mysql.html" target="_blank" rel="nofollow noopener noreferrer">text</a>), and Timeline (<a href="http://www.infoq.com/presentations/Twitter-Timeline-Scalability" target="_blank" rel="nofollow noopener noreferrer">video</a>&nbsp;|&nbsp;<a href="http://highscalability.com/blog/2013/7/8/the-architecture-twitter-uses-to-deal-with-150m-active-users.html" target="_blank" rel="nofollow noopener noreferrer">text</a>).
- For more advanced examples, check out these posts on <a href="http://highscalability.com/google-architecture" target="_blank" rel="nofollow noopener noreferrer">Google</a>, Youtube (<a href="http://www.youtube.com/watch?v=w5WVu624fY8" target="_blank" rel="nofollow noopener noreferrer">video</a> | <a href="http://highscalability.com/youtube-architecture" target="_blank" rel="nofollow noopener noreferrer">text</a>), <a href="http://highscalability.com/blog/2012/2/13/tumblr-architecture-15-billion-page-views-a-month-and-harder.html" target="_blank">Tumblr</a>, <a href="http://highscalability.com/blog/2009/8/5/stack-overflow-architecture.html" target="_blank" rel="nofollow noopener noreferrer">StackOverflow</a>, and <a href="http://highscalability.com/blog/2011/11/29/datasift-architecture-realtime-datamining-at-120000-tweets-p.html" target="_blank" rel="nofollow noopener noreferrer">Datashift</a>.

Don't worry if you don’t understand everything. Many of the posts contain lots of nitty-gritty details which, while priceless to know on your job, are not requirements at interviews. Try to focus on the shared principles used, and keep track of the lessons learned by these folks.

As you read the posts, you'll start noticing common technologies and patterns appear. As you do, make sure you do some research on each frequently seen technology. Try to write down <strong>what problem it solves</strong>, what its alternatives are, and what some common pros and cons may be.

One good way to research the alternatives to a technology is to type its name in Google followed by the text " vs ", and see what shows up in the Google Suggest box. For example, if you typed "rabbitmq vs" you'd get entires like "rabbitmq vs activemq", "rabbitmq vs redis", "rabbitmq vs msmq", "rabbitmq vs kafka" - which is a pretty good list to get you started.&nbsp;

The goal of all this reading (other than having tons of fun) is to develop practical knowledge about what works and what doesn’t work in “the real world”. After reviewing a bunch of these architectures and seeing where they agree or disagree, you’d be very well positioned to move on to the next step.

### Summary

When it comes to system design, it's incredibly useful to review real-life architectures. As you do this, make sure you:

- Pay attention to what technologies are used. Go ahead and research each new technology and see what problem it solves, what its alternatives are, where it excels, and where it fails.
- Take note of the common patterns you see, and how they relate to the scalability theory you learned in the previous section.
- Read through the lessons learned - they are a very quick way to learn from other people's battle scars.

Congratulations! Now that you've reviewed half a dozen to a dozen of these architectures, you're ahead of 95% to 99% of interview candidates. Not bad at all.

### What's next?

Now that you have both solid theory and solid practice under your belt, let's see how all of that knowledge comes together, particularly in the field of technical interviews. In the next section we'll wrap things up.
