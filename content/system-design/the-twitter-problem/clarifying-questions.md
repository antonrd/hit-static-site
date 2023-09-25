---
title: "Clarifying Questions"
type: docs
weight: 20
aliases: ["/classrooms/system-design/lesson/68"]
---
The way it is given, this problem is very unclear. At first, it may seem that you don’t need more than this one sentence. After all, it describes what the system should be doing. But think about it - being the architect and developer you need to know much more in order to make the proper decisions. Let's start thinking about them and get some answers from our imaginary interviewer.

First of all, how many users do we expect this system to handle? Our interviewer says:

<blockquote>
“well… to make things interesting, let’s aim for 10 million users generating around 100 million requests per day”
</blockquote>

That’s great but let’s continue. Since we have the notion of following someone, how connected will these users be? After all, they will form a graph with the users being the nodes and the edges will represent who follows whom. Our imaginary interviewer has an answer for this too:

<blockquote>
“we expect that each user will be following 200 other users on average, but expect some extraordinary users with tens of thousands of followers”
</blockquote>

Now, our graph is starting to look like something more concrete and we could start thinking of a design, which would accommodate its size.

We have another dimension in the application: tweets. Producing new tweets and liking them should be the most common write operations in the application. But how many requests will that generate? Our interviewer says:

“Hm, that’s hard to say… we expect that there will be a maximum of 10 million tweets per day and each tweet will probably be liked twice on average but again, expect some big outliers.”

Let’s make a few very simple calculations with the information we just received. We will have around 10 million users. Average number of followed other users is 200. This means that the network of users will have about 200 * 10 million edges. This makes 2 billion edges. If the average number of tweets per day is 10 million the number of likes will then be 20 million.

So far so good, we’ve got some numbers instead of nothing. In real life we can never have the exact numbers but it is always nice to have some predictions so that we know what kind of system we want to design. Imagine that the interviewer had in mind some very skewed version of Twitter in which there were only 30,000 users who produced thousands of tweets a day each and were all very strongly connected. This would probably throw us in a different direction for some of the design decisions. Each such problem could have many different interesting versions and it is amusing to think about each of them separately. In this case we will focus on the description given above.

Ok, so what else prevents us from getting our hands dirty and starting work on some high level design? In addition to the expected size of different things, for a system like that it will be important to know what availability is expected and what response times are tolerable. Naturally, our interviewer wants to have a system, which loads pretty quickly. None of the operations described above should take more than a few hundred milliseconds. The system should be online all of the time. It is not good to design into this application any downtimes.

That took a while to describe. There are many other questions that one could ask and we will get to some more in the next sections just to illustrate that sometimes questions pop up when you start thinking about the solution. However, interview time is very limited and you need to find the balance. This session where you ask questions and get answers should probably not last more than just a few minutes assuming your interview lasts 40-45 minutes and especially if this is not the only problem you get in it. Keep that in mind and practice will let you find your sweet spot.

Remember that not all system design questions will contain one or two sentences. In some cases the interviewer may give you a detailed specification, which includes more numbers, information about the UI and other important requirements. Even in such cases it’s part of your task to extract what is useful for you and figure out if something important is missing.

<div class="list-panel">
<h4>To summarize, here are some more things we now know:</h4>

<ul>
<li>10 million users</li>
<li>10 million tweets per day</li>
<li>20 million tweet likes per day</li>
<li>100 million HTTP requests to the site</li>
<li>2 billion “follow” relations</li>
<li>Some users and tweets could generate an extraordinary amount of traffic</li>
</ul>
</div>

Now, we continue to our high-level system design!
