---
title: "What are system design questions?"
date: 2023-08-20T16:10:56+02:00
type: docs
weight: 10
aliases: ["/classrooms/system-design/lesson/52"]
---
In this section we'll talk about the questions which require the interviewee to design a high-level architecture for some sort of a software system. This can be a web facing service, a RESTful API, a peer-to-peer desktop app, and so on. The exact type of question will most likely vary depending on the specifics of the company you interview at.

### Some examples

We can give a few examples of such questions:

* Design a URL shortening service like bit.ly.
* How would you implement a web search engine?
* Design a client-server application which allows people to play chess with one another.
* How would you store the relations in a social network like Facebook and implement a feature where one user receives notifications when their friends like the same things as they do?

Hopefully these example questions give you some idea of what we will be talking about. The web is full of many other examples. In addition to that the book “Cracking the Coding Interview” has a small section offering some more such questions.

### Don't panic

These questions may seem intimidating at first. After all, how does one design a web search engine in 20-30 minutes!? It has taken many smart people multiple years to do that properly. Don’t worry, no one really expects that from you.

The idea of these questions is to have a discussion about the problem at hand. What’s important for the interviewer is the process, which you use to tackle the problem. The typical outcome of such a discussion is a high-level architecture addressing the goals and constraints in the question. Perhaps the interviewer will choose one or more areas where they will want to discuss bottlenecks and other common problems.

Remember that there is no one right answer. A system can be built in different ways. The important thing is to be able to justify your ideas. This is somewhat different from the algorithm design questions, which are discussed in the [course on algorithmic interviews](/algorithms/).

Finally, keep in mind that the discussion about the same system design problem could go in different directions depending on the goals of the interviewer. They may be willing to see how you create a high-level architecture covering all aspects of the system. Or rather, they could be more interested in looking at a few specific areas and diving deeper into them. In any case, you should have a strategy for how to approach the different situations. We will look into such strategies in the next sections.

### Our approach

Similar to the algorithmic questions, we believe that system design questions require a combination of the right strategy and knowledge. By strategy we mean a way to approach the problem at an interview. We've seen good candidates fail not because they lack the knowledge but because they cannot focus on the right things while discussing a problem.

Because of that, in the next few sections, we will present our strategy for approaching system design questions at tech interviews. In addition to that, we've collected useful online resources, which will help you update your knowledge of software systems design.

### What’s next?

Now that you have an idea of what system design questions look like, let’s talk about some strategies for solving them at an interview. We will also look at an example problem, which will help us apply the strategies in this chapter.
