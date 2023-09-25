---
title: "Summary"
type: docs
weight: 50
aliases: ["/classrooms/system-design/lesson/105"]
---
Given a quite vague initial problem statement we managed to design a system that should work well in production under the expected constraints. The system will probably have some flaws in its current form but the important thing is that it already is quite robust and able to scale. At the same time we’ve described it in enough details.

At an interview you can always be asked to dig deeper into one or a few particular parts of the design. Maybe you would have to suggest concrete solutions for each part of the system. In our case you have to be familiar with one or a few message queue solutions and be able to suggest one that could be used in this case. Same goes for the database used and so on.

Each interview is unique and you will need to adapt to the situation. In this example problem we tried to produce a low-level design that covers most important aspects of a production system that can summarize text. To get to this point we went through a few steps:

* Tried to collect information about the constraints of the problem
* Drafted a very high-level design of the system. While doing that some additional questions popped up and by getting the answers to them we made the right decisions about the system. We also made sure that the interviewer is happy with the general direction that we are going before going into the details.
* After all that, we went into more details to address various issues that the system could have in production. This is probably the most time consuming part, which will also involve some more detailed discussions about different decisions that we make. You need to be prepared to talk about things more concretely using actual numbers, technology solutions and possible use cases.

Note that it’s fine to ask additional clarifying questions throughout the whole interview. Whenever you feel like it’s not possible to make a good design choice with the information that you have, it may be the case that you are missing important information that the interviewer could give you.

And sometimes the interviewer may not tell you all that you need. They may want to see if you are able to make trade-offs between possible solutions.

This is it for this example system design problem. We will be happy to hear your feedback about this problem and the site as a whole. Let us know if you find any issues or feel like the content can be improved.
