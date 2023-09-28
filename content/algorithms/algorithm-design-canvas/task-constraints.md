---
title: "Task Constraints"
type: docs
weight: 30
aliases: ["/classrooms/algorithm-design/lesson/79", "/algorithm-design/constraints"]
---
You never want to solve a problem that’s ill-defined. That’s why the very first thing you should turn your head to when it comes to algorithm design problems is the problem’s constraints.

### The importance of constraints

Developing an algorithm that sorts 50 numbers is going to be fundamentally different from developing an algorithm that sorts 5 billion strings, each one 1 million characters long. So if I told you “design an algorithm that sorts an array”, you’d better not start coding a solution right away. Among other things, you need to understand things like what’s in the array, and how large the array can get.

You're probably aware that interview problems have a bunch of constraints, which tell you how efficient your solution should be. What is less obvious is that interviewers don't always give you all the information needed. They expect you to be asking clarifying questions. Don't be alarmed if not everything is clear in a problem statement, this is your chance to make it so.

### How do you figure out the right questions?

Generally speaking, think about all the things that matter to your solution. For example, make sure you know the minimum and maximum possible values for any key value in the statement. These may affect the performance of your solution directly. If there are arrays of values you need to know the range of these values, too. They can be numbers, chars, geometric figures, etc. Some of these should come naturally to you once you hear the statement. If it says that there are N numbers and nothing else is mentioned about N, ask how big it can be. Others could come when you start designing your solution. If a given value is important for the complexity of your solution, don't hesitate to ask about it. Never assume things on your own.

The Algorithm Design Canvas helps you collect the needed information at an interview. It has a section where you need to fill in all the important constraints in a problem. If you use it while practicing you will get into the habit of making sure you know everything that you need to design an efficient solution.

Filling in the Constraints box is nothing more than asking the interviewer the right questions. Every problem’s different, but to get you started we’ve compiled a pretty extensive list of common things you should keep an eye on. All of them are included in the Common Constraints Handout. Feel free to download it and print it out: It will come in handy!

**Get the [Common Constraints Handout (PDF)](/files/the-common-constraints-handout.pdf)**

The handout above will help you get a good idea of what is important in most interview problems. In addition to that, you will have to practice with real problems to gain experience. For this you will be able to use the problems we recommend further in the course.

### Examples

And here is how we apply all this to our sample [ZigZag problem](https://community.topcoder.com/stat?c=problem_statement&pm=1259&rd=4493&rm=&cr=107835).

***NOTE***: In this video, around 4:40, the author types in the canvas that 2-element subsequences are all ZigZag sequences. This is not always correct. The 4th constraint should be "1-element subsequences are ZigZag".

<!-- <div style="text-align: center; margin: 20px">
<iframe allowfullscreen="" frameborder="0" height="400px" id="zigzag" mozallowfullscreen="" src="//player.vimeo.com/video/86507332?api=1&amp;player_id=zigzag" webkitallowfullscreen="" width="600px"></iframe>
</div> -->

<div class="row">
<div class="col-md-8 col-md-offset-2">
<div class="embed-responsive embed-responsive-16by9 text-center">
{{< youtube frGSrTLZa8M >}}
</div>
</div>
</div>

### What's next?

Once we know all we need about the problem, let's look at some strategies for designing a solution.
