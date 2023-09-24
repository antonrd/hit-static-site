---
title: "Step 1: Constraints and use cases"
type: docs
weight: 10
---
Just like algorithm design, system design questions will also most likely be weakly defined. Consider the question about the URL-shortening service ("Design a URL shortening service like bit.ly"). There are so many things that are unclear about it! Without knowing more, it will be impossible to design an appropriate solution. Actually, many candidates forget about this and start designing a solution immediately.

**Don’t make this mistake!**

The very first thing you should do with any system design question is to clarify the system's constraints and to identify what use cases the system needs to satisfy. Spend a few minutes questioning your interviewer and agreeing on the scope of the system. Many of the same rules we discussed while [talking about algorithm design](/algorithms/algorithm-design-canvas/task-constraints/) apply here as well.

Usually, part of what the interviewer wants to see is if you can gather the requirements about the problem at hand, and design a solution that covers them well. Never assume things that were not explicitly stated.

For example, the URL-shortening service could be meant to serve just a few thousand users, but each could be sharing millions of URLs. It could be meant to handle millions of clicks on the shortened URLs, or dozens. The service may have to provide extensive statistics about each shortened URL (which will increase your data size), or statistics may not be a requirement at all.

You will also have to think about the use cases that are expected to occur. Your system will be designed based on what it's expected to do. Don't forget to make sure you know all the requirements the interviewer didn't tell you about in the beginning.

### Example

Here's an example of how we'd approach defining the use cases and the constraints for the url shortening problem.

#### Use cases

<div class="row">
<div class="col-md-8 col-md-offset-2">
<div class="embed-responsive embed-responsive-16by9 text-center">
{{< youtube IV7ImQfjnTs >}}
</div>
</div>
</div>


#### Constraints

<div class="row">
<div class="col-md-8 col-md-offset-2">
<div class="embed-responsive embed-responsive-16by9 text-center">
{{< youtube 7hJ79RuKBM8 >}}
</div>
</div>
</div>

<br>

> **Note to video**: It has been pointed out to us that it is not very clear how the author gets to the 1 bln requests per month number around minute 6:00 of the video. Here is a short explanation. The author was considering the average time span of a URL (1-2 weeks, let's take the average ~ 10 days). Then he assumed 1 click per day, keeping in mind that the top 20% got much more traffic than the rest 80%. This makes 100 mln * 10 days * 1 click per day = 1 bln.
>
> The important thing here is that these calculations are based largely on many assumptions and gut feeling. They may be incorrect. The point is that at the interview, if you need to come up with such numbers it's good to have some background knowledge but also to be able to do reasonable conclusions about the numbers and to explain them to the interviewer.

> **Update**: Arnab Dutta sent us a great diagram with alternative ways to estimate the requests per month. You can find it <a href="https://github.com/antonrd/hiredintech_files/raw/master/system_design/digram_url_shortening.jpg" target="_blank" rel="noopener noreferrer">here</a>
