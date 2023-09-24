---
title: "High-level Design"
type: docs
weight: 30
---
It’s a good idea to start from the top and define the main parts of our application. Then, for the high-level design, we can discuss their subparts.

As it is often the case, we can divide our architecture in two logical parts: 1) the logic, which will handle all incoming requests to the application and 2) the data storage that we will use to store all the data that needs to be persisted. If you learn enough about popular software systems, especially the ones that are accessed through a web browser you will notice that such a breakdown is quite popular and natural.

Now we begin with the first part. What should it take care of? The answer will come straight from the problem statement and the clarifying comments that the interviewer has made. At this point it has become obvious that our application will need to handle requests for:

<div class="list-panel">
<ul>
<li>posting new tweets</li>
<li>following a user</li>
<li>liking a tweet</li>
<li>displaying data about users and tweets</li>
</ul>
</div>

The first three operations require things to be written somewhere in our database, while the last is more about reading data and returning it back to the user. The last operation will also be the most common one as can be inferred from the numbers discussed in the previous section.

Let’s make it more concrete how the user will interact with our application and design something that will support such interactions. We can describe to the interviewer how we imagine this to work. For example, there will be a profile page for each user, which will show us their latest tweets and will allow for older tweets to be shown. Each such page will have a button for following the user. There will also be a button at the top of the page, which will allow logged in users to open a dialog box and write a message in it. After they click a button the message will be stored and will appear on their profile page. Once we have confirmed this very rough description of the UI we can begin with the design of the back-end supporting everything.

This kind of brief description of how you imagine the application to look could be useful because you make sure that you and the interviewer are on the same page. A simple drawing is also very helpful. You can look at one example in the [Appendix section](/system-design/the-twitter-problem/appendix/).

---------------------

### Handling user requests

We know that the expected daily load is 100 million requests. This means that on average the app will receive around 1150 requests per second. Of course, this traffic is expected to be distributed unevenly throughout the day. Therefore our architecture should allow the app to handle at least a few thousand requests per second at times. Here comes the natural question about what is needed to handle this kind of load. As you may have guessed the answer depends on several things.

One aspect is the complexity of the requests that the application receives. For example, one request could require just one simple query to a database. It could also need a few heavier queries to be run and some CPU-intensive computations to be performed by the application.

Another aspect could be the technologies used to implement the application. Some solutions are better at concurrency and use less memory than others. In a situation like this one you should have some common knowledge about what kind of load can be handled by a single machine for sure and what is load that definitely needs more computing power. To build that it would help to spend some time reading about different real-life examples. Some people also compare the throughput they have achieved in different setups using different web frameworks, hosting services and so on. Any information like that could help you build better instincts about this matter. Finally, your personal work experience is always the best way to learn about these things.

When the expected load seems nontrivially high you can always consider scaling up or out. Scaling up would be an approach in which you decide to get a beefier and more expensive server, which is capable of handling the expected load. This approach has a natural limit for its scalability because after a given point the hardware of one machine just isn’t capable of handling all the requests. In some cases doing that makes sense.

Scaling out would involve designing your architecture in a way that spreads the computations over a number of machines and distributes the load across them. This approach is better at scaling if your load grows significantly. However, it involves some other complications.

One more advantage of using more than one server for your application is the resilience that you add to your whole system. If you only have one machine and it goes down your whole application is down. However, if there are 10 servers handling requests and one or two go down the others will be able to handle at least part of the load if not all of it.

In our particular problem we would definitely suggest using a load balancer, which handles initial traffic and sends requests to a set of servers running one or more instances of the application.

One argument is the resilience that we gain as mentioned above. Another one is that our application doesn’t seem to have any special requirements in terms of very high memory or CPU usage. All requests should be serviceable with code that runs on regular commodity machines. Using many such machines in parallel should give us the flexibility to scale out a lot.

How many servers we should have is something that can probably be determined experimentally with time. Also, if we set things up properly it should be fairly easy to add new servers if that is needed.

Under these links you can read more about load balancing and check out examples of load balancing solutions:

<div class="list-panel">
<ul>
<li><a href="http://en.wikipedia.org/wiki/Load_balancing_(computing)" target="_blank" rel="noopener noreferrer">Wikipedia’s explanation</a></li>
<li><a href="http://aws.amazon.com/elasticloadbalancing/" target="_blank" rel="noopener noreferrer">Amazon’s service for traffic load balancing</a></li>
<li><a href="http://nginx.org/en/docs/http/load_balancing.html" target="_blank" rel="noopener noreferrer">nginx - HTTP load balancer</a></li>
<li><a href="http://www.haproxy.org/" target="_blank" rel="noopener noreferrer">HAProxy - TCP/HTTP load balancer</a></li>
</ul>
</div>

We’ll say more about load balancing when we start analysing the bottlenecks in our architecture. For the moment, at this high level, we’ll just mention that this is a needed component. Behind the load balancer we will be running a set of servers that are running our application and are capable of handling the different requests that arrive.

The application logic itself will most likely be implemented using some web framework, which in general allows us to write apps handling HTTP requests, talking to a database and rendering the appropriate HTML pages requested by the user. The details of which technology will be used are most likely not going to be important for this type of interview question. Nevertheless, it’s strongly advised that you get a good understanding of the different types of modern web frameworks and how they work. This book does not cover such material but some things to look at are Node.js, Ruby on Rails, Angular.js, Ember.js. React.js, etc. This does not mean that you need to get down to learning these in detail but rather to take a look at the existing ecosystem of technologies, how they interact with each other and what are the pros and cons.

Now we have a load balancer and a set of application servers running behind it. The load balancer routes requests to the servers using some predefined logic and the application servers are able to understand the requests and return the proper data back to the user’s browser. There is one more major component for our high-level architecture to be complete - the storage.

---------------------------

### Storing the data

We need to store data about our users and their tweets to make the application complete. Let’s quickly look at what needs to be stored. First of all, users have profiles with some data fields attached to them. We’ll need to store that. Each user has a set of tweets that they have produced over time. Moreover, users can follow other users. We need to store these relationships in our database. Finally, users can mark tweets as liked. This is another kind of relationship between users and tweets. The first one was recording users as authors of tweets. The second one will record users who liked a tweet.

Obviously, there are some relations between our data objects - users and tweets. Let’s assess the approximate size of the data to be stored. We said that we expect around 10 million users. For each user we’ll have some profile data to store but overall that kind of data shouldn’t be an issue for us. Tweets will be generated at an average speed of 10 million per day. This makes about 115 per second. Also, for a single year there will be 3.65 billion tweets. So, let’s aim for a solution that can store efficiently at least 10 billion tweets for now and the incoming traffic mentioned above. We didn’t really ask how big a tweet can be. Maybe it’s safe to quickly ask that now and let’s assume our interviewer told us it’s the same as it is for the real Twitter - 140 characters. This means that for tweets we want to be able to store at least 140 * 10 bln = 1.4 trillion characters or around 2.8 terabytes if we assume 2 bytes per character and no compression of the data.

Finally, there are the connections between the users and the likes of tweets. As we mentioned above the connections should be around 2 billion and each connection will most likely just contain two IDs of users where the first follows the second. So very likely it would be enough to store two 4-byte integer fields, making 8 * 2 bln = 16 bln bytes or 16 gigabytes.

The likes are expected to grow at a rate of 20 mln per day. So, for a year there will be 7.3 bln such actions. Let’s say we want to be able to store at least 20 bln such objects. They can probably just point to one user and one tweet through their IDs. The IDs for the tweets will probably need to be 8 byte fields while for the users we could use 4 bytes only. This is because our tweets will grow a lot in number. So, our very rough calculation gives us 12 * 20 bln = 240 bln bytes or 240 gigabytes.

After this quick analysis it is obvious that the tweets will take up the majority of our storage’s space. In general, you don’t need to make very detailed calculations especially if you don’t have much time. However, it is important to build a rough idea about the size of the data that you will need to handle. If you don’t figure that out any design decision at the higher or lower level may be inappropriate.

Now back to the storage. Our data has a number of relations between its main objects. If we decide to use a relational database for storing users, tweets and the connections between them this could allow us to model these relations easily. We know that the expected size of the data to store is around 2.6 - 2.7 terabytes. Real-life examples show that famous companies like Twitter and Facebook manage to use relational databases for handling much bigger loads than that. Of course, in most cases a lot of tuning and modifications were required. Below are some useful links related to how big companies use relational databases for large amounts of data:

<div class="list-panel">
<ul>
<li><a href="http://highscalability.com/blog/2011/12/19/how-twitter-stores-250-million-tweets-a-day-using-mysql.html" target="_blank" rel="noopener noreferrer">How Twitter used to store 250 million tweets a day some years ago</a></li>
<li><a href="https://www.youtube.com/watch?v=NfS5ZLNPxS4" target="_blank" rel="noopener noreferrer">How Facebook made MySql scale</a></li>
<li><a href="http://webscalesql.org/" target="_blank" rel="noopener noreferrer">WebScaleSQL - an effort from a few big companies to make MySql more scalable</a></li>
</ul>
</div>

Let’s say we decide to use a relational database like MySql or Postgres for our design.

The data that will be stored and the rate of the queries it will receive are not going to be absurdly high but they are not going to be trivial either. In order to handle the incoming read requests we may need to use a caching solution, which stands in front of the database server. One such popular tool is memcached. It could save us a lot of reads directly from the database.

In an application like ours it is likely that a given tweet or a user’s profile becomes highly popular and causes many requests to be sent to our database server. The cache solution will alleviate such situations by storing the popular bits of data in memory and allowing for very quick access to them without the need to hit the database.

It is possible that at this moment the interviewer stops you and throws a question about what you were just talking about. For example, you just mentioned using a caching solution and imagine that the interviewer asks you:

> “Sounds good, but could you tell me more about why reading from the cache would be better than just reading from the database?”

It is perfectly fine and expected to receive such questions from your interviewer throughout your discussion. You need to be prepared with enough knowledge about the methods and technologies that you use, so that you can justify their usefulness and talk about how they work. It is also very important to be able to explain why one solution is better than its alternatives and this way motivate your design choices.

To answer the question asked, we could say that a database stores data on disk and it is much slower to read from disk than from memory. A solution like memcached stores data in memory, which provides way faster access. We would need to clarify further that databases usually have their own caching mechanisms but with memcached we have better control over what gets cached and how. For example, we could store more complex pieces of data like the results from popular queries.

It is vital to have a good understanding of the differences in read/write access to different types of storage mechanisms. For example, you need to know how hard drive speeds compare to RAM to CPU cache. And it is worth mentioning that nowadays people are using a lot of SSDs, which provide better parameters than the older spinning ones.

Going further, in order to make it possible to answer read queries fast we will definitely need to add the appropriate indexes. This will also be vital for executing quick queries joining tables. Considering the size of the data we may also think about partitioning the data in some way. This can improve the read and write speeds and also make administration tasks like backups faster.

If you intend to be interviewing at places where relational databases are used, make sure you get comfortable with the main aspects of using them. You should be familiar with the general organization of a database schema, the ways different real-life situations are represented through tables and how indexes come into play, so that the planned queries run fast enough with the expected data size. Throughout this example we will talk about some other interesting topics related to scaling a relational database.

At this point we have a pretty good high-level architecture, which is built considering the important dimensions and requirements of our application. Described like this it looks like something that could work. Most likely you will have drawn one or more simple diagrams for your interviewer to make things more understandable. Now may come the time when you need to start digging deeper into some of the moving parts of this design. Or the interviewer may decide to tighten some of the initial requirements to see how you can alter your system design to accommodate the changes. We will look at a few such issues in the next section, which focuses on various bottlenecks and scalability issues.

Finally, notice that we never dug too deep into any of the aspects of the high-level design. This is our goal - we want to draw the whole picture rather quickly within a few minutes and to make sure our interviewer agrees with the ideas that we presented. If they explicitly want you to focus on a specific aspect of the design, then go ahead and do what they ask for. Otherwise, our advice is to not get into the details of any specific part of the application until everything else is outlined at the higher level. Once we’ve built this bigger picture of the system design the interview could go into more details about specific parts of the system.
