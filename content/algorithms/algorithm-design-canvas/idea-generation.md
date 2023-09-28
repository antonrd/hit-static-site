---
title: "Idea generation"
type: docs
weight: 40
aliases: ["/classrooms/algorithm-design/lesson/80", "/algorithm-design/idea-generation"]
---
One of the goals of this course is to teach you how to solve new problems. This will be the topic of the current section. We believe that it is much better to learn how to design solutions instead of trying to cover all interview questions that exist. There are a few reasons for that.

First of all, new interview questions get created all the time. It is virtually impossible to know all of them by heart. Second, even if you know the solutions to many problems you need to be able to analyze these solutions, have a discussion about them and be able to tweak them in case the interviewer decides to modify the question in some way.

One final reason is that employers are looking for people who can think of solutions on the spot. This is why it is very useful to learn how to be such a person.

So, how can you achieve that? In this section we will discuss several strategies for solving algorithmic problems. They will give you a small framework for approaching a problem and coming up with a good solution.

Remember that practicing solving problems is the only way to really get in good shape. These strategies are one tool that you can use but you will become good with it only if you devote enough time applying it. Actually, with time you will notice various patterns in the problems and it will become much easier for you to crack them.

The following strategies are popular among people participating in programming contests. Since the algorithmic interview questions are very similar to these, we believe that they are very relevant here, too.

### Simplify the task

Let’s look at the following question:

“A map of streets is given, which has the shape of a rectangular grid with N columns and M rows. At the intersections of these streets there are people. They all want to meet at one single intersection. The goal is to choose such an intersection, which minimizes the total walking distance of all people. Remember that they can only walk along the streets (the so called "Manhattan distance").”

So, how can we approach this problem?

Imagine that we only have one street and people are at various positions on that street. They will be looking for an optimal place to meet on this street. Can you solve this problem? It turns out to be much easier than the 2D version. You just have to find the median value of all people’s positions on the street and this is an optimal answer. We’ll leave it to you to prove it.

Now, if we go back to the original problem we can notice that finding the X and Y coordinates of the meeting point are two independent tasks. This is because of the way people move - Manhattan distance. This leads us to the final conclusion that we have to solve two 1D problems and this will give us the final answer. As we already know how to solve the 1D case, we are done.

This strategy allows you to start thinking about a simpler version of the problem and to draw some conclusions about how to solve the original problem.

### Try a few examples

We’ve noticed that candidates rarely test with examples other than the one given by the interviewer. Sometimes, however, this helps a lot. You may start noticing patterns if you try to solve a few sample inputs that you create. It is ok to tell the interviewer that you would like to try writing down a few examples in order to try to find some pattern. Then do it quickly and see where it leads you.

Here is a sample problem:

“There are N+1 parking spots, numbered from 0 to N. There are N cars numbered from 1 to N parked in various parking spots with one left empty. Reorder the cars so that car #1 is in spot #1, car #2 is in spot #2 and so on. Spot #0 will remain empty. The only allowed operation is to take a car and move it to the free spot.”

This problem is not hard but at first seems intimidating. Write down 5 different examples and try to order the cars on a sheet of paper. See if you can notice a pattern in how it happens.

### Think of suitable data structures

For some problems it is more or less apparent that some sort of data structure will do the job. If you start to get this feeling think about the data structures you know about and try to apply them and see if they fit. For example you can consider the data structures we cover in the algorithmic topics section.

Here is an example question:

“Design a data structure, which supports several operations: insert a number with O(logN), return the median element with O(1), delete the median element with O(logN), where N is the number of elements in the data structure.”

Here it is pretty obvious that a data structure is involved. What could we use to solve the problem? Which data structure has similar characteristics? Things like arrays, stacks and vectors are far from these requirements. Perhaps some sort of a binary tree could do as they usually support logarithmic insert and remove operations.

Heaps do that but they either return the minimum or maximum element, not the median. Hm, but this is very close, if only we could get the median. What if we use two heaps, one stores the one half smallest numbers and the other is for the other half biggest numbers. Then some number in the middle is the median. As mentioned above one of the heaps could hold the maximum and the other the minimum element. This should be enough to return the median in constant time. We will leave the details to you to figure out.

In summary, if you get a feeling that a data structure could be the solution to a problem you are given, think a bit about the ones you know. You may have to combine two or more to get to the correct solution.

### Think about related problems that you know.

This is a simple idea and could help if nothing else helps. Since you’ve been practicing hard for your interviews you surely came across many different problems. If you see a problem and cannot think of a solution, try to remember another problem, which looks like it. If there is such, think if its solution can somehow be adjusted to work for the problem at hand. This can sometimes mislead you but many problems are related, so it could also get you out of the situation.

Read carefully these strategies and try to apply them to the problems you face. In this course there are many recommended problems and you can do that with all of them. The [Algorithm Design Canvas](/files/the-algorithm-design-canvas.pdf) will help you write down the ideas that come to you.

TopCoder tutorials also provide a useful resource on this topic, which you may find worth reading: <a href="https://www.topcoder.com/community/data-science/data-science-tutorials/how-to-find-a-solution/" target="_blank" rel="noopener noreferrer">How to Find a Solution</a>.

If you have other strategies for solving interview problems we will be more than happy to hear about them.

### Examples

Let's apply all this to the ZigZag problem.

<div class="row">
<div class="col-md-8 col-md-offset-2">
<div class="embed-responsive embed-responsive-16by9 text-center">
{{< youtube XPdmSshFmO0 >}}
</div>
</div>
</div>

**Note**: There is actually an even faster solution to this problem with time complexity O(N). Here is <a href="https://community.topcoder.com/stat?c=problem_solution&cr=107835&rd=4493&pm=1259" target="_blank" rel="noopener noreferrer">some source code in TopCoder's website</a> implementing it.

### Summary

In this section you learned:

- It is important to learn to solve any problem instead of knowing all of them by heart.
- There is a set of well-known strategies for approaching interview problems. We look at them and use some of them for an example problem.

### What's next?

Designing solutions to a problem inevitably leads us to talking about time and space complexity. This is a very important topic. The next section will teach you more about it. So, let's dive into some complexity!
