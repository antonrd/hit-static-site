---
title: "Additional Considerations"
type: docs
weight: 50
aliases: ["/classrooms/system-design/lesson/73"]
---
### Increased number of read requests

We have our implementation of the system and it handles everything perfectly. But what would happen if suddenly we got lucky and people started visiting our application 5 times more often generating 5 times more read requests caused by viewing posts and user profiles. What would be the first place that will most likely become a bottleneck?

One very natural answer is our database. It could become overwhelmed with all the read requests coming to it. One typical way to handle more read requests would be to use replication. This way we could increase the number of database instances that hold a copy of the data and allow the application to read this data. Of course, this will help if the write requests are not increased dramatically. An alternative approach could be to shard our database and spread the data across different machines. This will help us if we need to write more data than before and the database cannot handle it. Such an approach does not come for free and it involves other complications that we would need to take care of. Consider getting familiar with these popular techniques for scaling a relational database.

If we manage to stabilize our database, another point where we could expect problems is the web application itself. If we’ve been running it on a limited set of machines, which cannot handle all the load anymore this could lead to slow response times. One good thing about our high-level design is that it allows us to just add more machines running the application. If the database is ready to handle more incoming requests from additional application instances we can scale horizontally like that. We will just add more machines running our application and instruct our load balancer to send requests to these machines, too. Of course, this sounds simpler that it is in practice but that’s the general idea.

One of the reasons why using the services of a company like Amazon or Heroku could be beneficial is that they make it easy to add new machines to your environment. You just need to have the money to pay for them. Having mentioned this, it is also useful to become familiar with some of these products and services that are in the market nowadays. For example, Amazon has a very big stack of services that can work together to provide a reliable and scalable environment for an application like ours. It is good to have an idea about what’s out there if you need to deploy a web-facing application.

Finally, if all else is scaled and capable of handling the increased loads we may need to improve our load balancing solution. We mentioned in the high level design that it is a very good idea to use a load balancer, which would direct requests to different instances of our application. This way our load balancer could become a single point of failure and a bottleneck if the number of requests is really high. In such cases we could start thinking about doing additional load balancing using DNS and directing requests for our domain to different machines, which are acting as load balancers themselves.

### Scaling the database

We just touched on that aspect but let’s talk a bit more about it. Let’s say our application needs to be able to store even more data and the read/write requests per second are increased significantly. If we are using a relational database with the proper indexes running on a single machine it could very quickly become unable to handle the loads that our application experiences. One approach mentioned above is to add an in-memory cache solution in front of the database with the goal to not send repeated read requests to the database itself. We could use a key-value store like memcached to handle that.

This will also be really useful for handling situations in which a tweet becomes viral and people start accessing it or the same thing happens to a given user’s profile.

But this could be insufficient if our data grows too quickly. In such cases we may have to start thinking about partitioning this data and storing it on separate servers to increase availability and spread the load. Sharding our data could be a good and necessary approach in such cases. It must be planned and used with care because it will cause additional complications. But sometimes it is just required. It is highly recommended that you read more about this topic and all the implication it brings along. This will help you justify your decision to shard and to have a discussion about the possible downsides of doing it.

Below are links to resources from Instagram and Flickr with some insights about how they managed to shard their data living in Postgres and MySql databases:

<div class="list-panel">
<ul>
<li><a href="http://instagram-engineering.tumblr.com/post/10853187575/sharding-ids-at-instagram" target="_blank">Sharding and IDs at Instagram</a></li>
<li><a href="http://www.databasesoup.com/2012/04/sharding-postgres-with-instagram.html" target="_blank">Sharding Postgres at Instagram (video & slides)</a></li>
<li><a href="http://code.flickr.net/2010/02/08/ticket-servers-distributed-unique-primary-keys-on-the-cheap/" target="_blank">Generating unique primary keys at Flickr when sharding></a></li>
</ul>
</div>

### Unexpected traffic

Let’s look at one more possible issue. We already touched on this but it doesn’t hurt to go through it one more time. In the beginning the interviewer warned us that there will be outliers in the data. This means that some users will have many more followers than the average. Also, some tweets will attract a lot of attention during a short period of time. In most cases such outliers will generate peaks in the number of requests that our application receives.

As we mentioned earlier this could increase the load on our database. In such a situation using a caching solution could help a lot. The idea is that it will be able to answer the popular and repeating requests coming from the application and these requests will never touch the database, which will be busy replying to other queries.

We could also experience unusual peaks in the requests hitting our application servers. If they are not enough to respond quickly enough to all requests this could cause timeout to occur for some of the users. In such situations solutions that offer auto-scaling of the available computing nodes could save the day. Some companies offering such services are Amazon and Heroku and they were already mentioned in this example. You can take the time to investigate what is out there on the market, so that you can have a discussion about possible ways to handle peaks in traffic.
