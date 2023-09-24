---
title: "Low-level Issues"
type: docs
weight: 40
---
Let’s assume that we’ve shaped the main parts of our Twitter-like application. In a real-life interview situation this would have been more like a discussion with the interviewer where you talk and they interrupt you with questions and comments. It is ok to have to clarify things that did not become apparent to the interviewer. It is also normal to not get everything right from the first time. Be prepared to accept suggestions from the interviewer or to have your design challenged even if it is sound.

All of the above discussion related to the so-called high level design may seem like it would take a lot of time to describe and discuss. This may be true if done inefficiently. Remember that at the interview you are usually given a very limited amount of time. If you want to be able to fit within that time you will need to practice solving system design problems, talking about your solutions, computing things like expected load, storage needed, required network throughput and so on. With time you will get the hang of it and will become better at having this special kind of discussion that the interview requires.

It is very likely that your interviewer would be interested to hear more details about a particular part of your designed system. Let’s look at a couple such aspects.

-----------------------------

### Database schema

If you’ve picked to use a relational database one possible topic for a more detailed discussion would be the schema that you intend to use. So, your interviewer asks:

<blockquote>
“If you’re going to use a relational database for storing all the data could you draft the tables and the relations between them?”
</blockquote>

This is something that is very common and you should be prepared for such questions. Let’s look at what we could draw and explain in this case.

We have two main entities: users and tweets. There could be two tables for them. For the users we would create a table like that with some column names suggested in brackets:

<div class="list-panel">
<h4>Table <code>users</code></h4>
<ul>
<li>ID (<code>id</code>)</li>
<li>username (<code>username</code>)</li>
<li>full name (<code>first_name</code> & <code>last_name</code>)</li>
<li>password related fields like hash and salt (<code>password_hash</code> & <code>password_salt</code>)</li>
<li>date of creation and last update (<code>created_at</code> & <code>updated_at</code>)</li>
<li>description (<code>description</code>)</li>
<li>and maybe some other fields...</li>
</ul>
</div>

Tweets should be slightly simpler:

<div class="list-panel">
<h4>Table <code>tweets</code></h4>
<ul>
<li>ID (<code>id</code>)</li>
<li>content (<code>content</code>)</li>
<li>date of creation (<code>created_at</code>)</li>
<li>user ID of author (<code>user_id</code>)</li>
</ul>
</div>

Perhaps one can think of other values but this should be enough in our case.

These two entities have several types of relations between them:

1. users create tweets
2. users can follow users
3. users like tweets

The first relation is addressed by sticking the user ID to each tweet. This is possible because each tweet is created by exactly one user. It’s a bit more complicated when it comes to following users and liking tweets. The relationship there is many-to-many.

For following user we can have a table like that:

<div class="list-panel">
<h4>Table <code>connections</code></h4>
<ul>
<li>ID of user that follows (<code>follower_id</code>)</li>
<li>ID of user that is followed (<code>followee_id</code>)</li>
<li>date of creation (<code>created_at</code>)</li>
</ul>
</div>

Let’s also add a table, which represents likes. It could have the following fields:

<div class="list-panel">
<h4>Table <code>likes</code></h4>
<ul>
<li>ID of user that liked (<code>user_id</code>)</li>
<li>ID of liked tweet (<code>tweet_id</code>)</li>
<li>date of creation (<code>created_at</code>)</li>
</ul>
</div>

Now that we have this rough idea about the database tables we will need, our interviewer could ask us to think about what else is needed to serve the load of expected queries. We already discussed with some numbers the expected sizes of the data. There is also a pretty good idea about the types of pages that the application will need to serve. Knowing this we could think about the queries that will be sent to our database and to try to optimize things so that these queries are as fast as possible.

Starting with the basics there will be queries for retrieving the details of a given user. Our users’ table above has both `id` and `username` fields. We will want to enforce uniqueness on both because IDs are designed to be unique and will serve as a primary key on the table and usernames are also meant to be different for all registered users. Let’s assume that the queries to our data will be filtering users by their username. If that’s the case we will definitely want to build an index over this field to optimize the times for such queries.

The next popular query will fetch tweets for a given user. The query needed for doing that will filter tweets using `user_id`, which every tweet has. It makes a lot of sense to build an index over this field in the tweets table, so that such queries are performed quickly.

We will probably not want to fetch all tweets of a user at once. For example, if a given user has accumulated several thousand tweets over time, on their profile page we will start by showing the most recent 20 or something like that. This means that we could use a query, which not only filters by `user_id` but also orders by creation date (`created_at`) and limits the result. Based on that we may think about expanding our index to include the `user_id` column but to also include the `created_at` column. When we have an index over more than one column the order of the columns matters. If our index looks like that: &lt;`user_id`, `created_at`&gt;, making a query filtering by just `user_id` will take advantage of the index even though we are not filtering by the second column. So, such an index will allow us to filter either by just `user_id`, or by both columns. This will allow us to fetch all tweets authored by a given user or to isolate just the tweets created in a given time frame. Both will be useful queries for our application.

For each user we will want to show the users that they follow and the users that follow them. For this we will need the table connections. To get the users followed by someone we can simply filter the connections table by the column `follower_id`. To get the users following someone we can filter by `followee_id`. All this means that it will make a lot of sense to build two indexes in this table - one on `follower_id` and another one on `followee_id`. Voila, we are ready to show the connections that each user has in our application. Like for tweets you can figure out how to fetch the connections in a paginated manner.

What about liked tweets by a user? We will definitely want to see something like that. For this we will need to use the table `likes`. We will need to join `likes` with `tweets` and to filter by `user_id` for the user whose likes we want to fetch. The columns used for joining will be the `tweet_id` in `likes` and `id` in `tweets`.

The above means that it makes sense to add two indexes - one on the `user_id` column and one on the `tweet_id` column.

Having discussed these base use cases, our interviewer suggests that you think about one more possible situation:

<blockquote>
“Do you think you could support with our database design the ability to display a page for a given user with their latest tweets that were liked at least once?”
</blockquote>

Let’s think about that. We will need to use the table `likes` but instead of filtering by the `user_id` column we will have to get the `user_id` from the tweets table. This means that we will again join the two tables - `likes` and `tweets` - and this time will filter by the `user_id` column in tweets. It seems like we have the needed indexes in place already. One is in `likes` over `tweet_id`, which will help us join this table with tweets. In table tweets the `id` field is a primary key so it has an index on it. And we also have an index on `user_id` in tweets, so this will help us filter by user.

One could think of other such query patterns and see what needs to be done in the database schema to address them. For example, for your own pleasure, you can think about supporting a page, which shows for a given user a list of recent tweets that this user either authored or liked, ordered by date of creation.

Here is another very good candidate for a homework exercise: for a given user A build a page showing the recent tweets authored by users that A is following. What would the query be, which indexes will it use and does it need more indexes to be added?

It is also worth mentioning that after creating the indexes our write queries will become slightly slower but the benefits that we get for our read operations are so significant with the amounts of data we have that we have no other choice.

In general, it is a useful skill to be able to design relational database schemas, to optimize them and to have a discussion about all that. We could cover much more on this topic but it is better to use specialized books and online resources for that. Be prepared to defend your database schema designs during your interviews. As mentioned already, if circumstances allow, it is always helpful to draw something on paper or a whiteboard. We’ve added a very simple diagram of our database schema in the [Appendix section](https://train.hiredintech.com/classrooms/system-design/lesson/72).

That was all great but with the expected size of our data we may have a separate discussion with our interviewer about partitioning the database in some way as a further step. We will touch on this a bit later in the text.

-----------------------

### Building a RESTful API

We have a simple plan for what our schema will be like. Another thing that our interviewer could be interested in is how our front-end would “talk” to the back-end system. Probably the most popular answer nowadays would be by exposing a RESTful API on the back-end side, which has a few endpoints returning JSON objects as responses. Many web applications are built this way nowadays and it is a good idea to take a look at what RESTful APIs are about if you don’t feel confident about this area.

Let’s see what we can draft for our particular task. The API endpoints will likely be built around the data entities that we have and the needs of the user-facing part of the application.

We will definitely need to fetch the profile details for a given user. So we could define an endpoint that looks like that:

<pre class="centered_code">
GET /api/users/&lt;username&gt;
</pre>

It will return a JSON object containing the data fields of a given user if such was found and will return status code 404 if no user matched the supplied username value.

To get the tweets of a given user ordered by date, we can expose an endpoint like that:

<pre class="centered_code">
GET /api/users/&lt;username&gt;/tweets
</pre>

This could be modified by supplying some query parameters telling the back-end that we want paginated tweets. For example, the default behavior will return the most recent 20 tweets only. But we could decide to load the next 20, and the next 20 and so on. A query fetching a subsequent “page” with queries could look like that:

<pre class="centered_code">
GET /api/users/&lt;username&gt;/tweets?page=4
</pre>

This tells the back-end to fetch the 4th page with 20 tweets, instead of the default behavior - 1st page with 20 tweets.

Let’s continue! Our front-end will also be asking about the users following a given user and followed by that user. Here are two possible endpoints for that:

<pre class="centered_code">
GET /api/users/&lt;username&gt;/followers
GET /api/users/&lt;username&gt;/followees
</pre>

So far we defined a few GET requests. Let’s look at creating new data. For example we will need an endpoint for posting a new tweet:

<pre class="centered_code">
POST /api/users/&lt;username&gt;/tweets
</pre>

Or how about following a given user:

<pre class="centered_code">
POST /api/users/&lt;username&gt;/followers
</pre>

If we look at the tweets, we may need API endpoints that cover them, too. For example it will be useful to be able to see a list of all users that liked a tweet:

<pre class="centered_code">
GET /api/users/&lt;username&gt;/tweets/&lt;tweet_id&gt;/likes
</pre>

And liking a tweet can be done through:

<pre class="centered_code">
POST /api/users/&lt;username&gt;/tweets/&lt;tweet_id&gt;/likes
</pre>

As you can see, there will be a number of such endpoints that will be needed to make our application tick. Our endpoints are revolving around the main entities that we have. We highly recommend that you read more about building good RESTful APIs and perhaps think about more scenarios in which you will need to define additional endpoints.

Of course, we will need some sort of authentication to be put in place, so that we make sure that not everyone can query our exposed API.

Now, let’s continue with some possible scenarios that the interview could follow. Imagine that you have outlined your ideas and the interviewer seems happy with what you have offered.

They may want to test your ability to spot bottlenecks and to handle the need to scale your system. Probably one could think of many complications to add to the problem statement and to lead the discussion in various directions. We will cover a few things that seem quite normal to consider and likely to happen in a typical interview.
