---
title: "Wrap-up"
type: docs
weight: 30
aliases: ["/classrooms/system-design/lesson/62", "/system-design/final-thoughts"]
---
Alright, at this point you already have solid theoretical and practical understanding of system design. In this section, we'll wrap things up and put them in the context of technical interviews.

### Everything is a tradeoff

This is one of the most fundamental concepts in system design.

Hopefully, at this point this is not a surprise to you. If you've looked at the real-life architectures, you saw that there rarely is one perfect way to do things. Each company ends up with a different architecture. Designing a scalable system is an optimization task: there are tons of constraints (time, budget, knowledge, complexity, technologies currently available, etc.), and you need to build the best thing that fits those constraints. Every technology, every pattern is great for some things, and not so great for others. Understanding these pros and cons, the advantages and disadvantages, is key.

**Remember: there is no one optimal system design.**

Sure, there are best practices you can use. But at the end of the day, it all boils down to balancing between time to market, system complexity, cost of development, cost of maintenance, availability, and many other things.

Being able to understand and discuss these trade-offs is what system design (and thus system design questions) is all about.

In your preparation, don’t try to find silver bullets. Instead, focus on what each scalability pattern is good for, what its shortcomings are, and why people prefer it over other patterns.

### Putting it all together & staying up to date

At this point, the most useful thing you could do is come up with a one or two pager that contains the scalability lessons you've learned.

Finally, you'd be well served throughout your professional career to stay up to date on how scalability evolves. For example, 10 years ago there were no Amazon Web Services and companies were forced to manage their infrastructure in house. Nowadays, using services like EC2, RDS, S3, Elastic MapReduce, etc. you can build a giant company. So while AWS didn’t change the fundamental scalability principles, it did change the landscape of technologies people need to be familiar with when scaling. Thus, staying up to date is quite important (or else you’d be reinventing the wheel).

### At the interview

So what should you do at your interview?

First of all, follow the System Design Process. You already know how to apply it, so we'll be brief. Don't skip steps, don't make assumptions, start broad and go deep when asked.

Second, keep in mind that system design questions serve as an idea exchange platform. Be prepared for **discussions** about tradeoffs, about pros and cons. Be prepared to give alternatives, to ask questions, to identify and solve bottlenecks, to go broad or deep depending on your interviewer's preferences.

Don't get defensive: whenever your interviewer challenges your architectural choices, acknowledge that rarely an idea is perfect, and outline the advantages and disadvantages of your choice. Be open to new constraints to pop up during the discussion and to adjust your architecture on the fly.

Most of all, have fun. Dreaming up architectures is a very stimulating mental process - enjoy it and stay positive. You're already equipped with the right knowledge, just apply it during your interview and you'll do well.

### Example

At this point, we're ready to close off the scalability part of our URL shortening problem.

<div style="text-align: center; margin: 20px;"><iframe allowfullscreen="" frameborder="0" height="400" mozallowfullscreen="" src="//player.vimeo.com/video/86413593" webkitallowfullscreen="" width="600"></iframe></div>

### Summary

You now know how to approach any system design question. You first build a high-level architecture by identifying the constraints and use cases, sketching up the major components and the relationships between them, and thinking about the system's bottlenecks. You then apply the right scalability patterns that will take care of these bottlenecks in the context of the system's constraints.

### What's next?

Congratulations! You should now feel very comfortable attacking any system design question. Having learned a repeatable approach for system design, as well as seen lots of real-life examples of scalable architectures, your chances of acing the tech interview are **very solid**.
