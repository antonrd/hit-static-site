---
title: "Testing your code"
type: docs
weight: 70
aliases: ["/classrooms/algorithm-design/lesson/83", "/algorithm-design/testing"]
---
Once your code is written, you don’t just lift your pen, say “I’m ready” and leave. A great next step is to verify it with several small test cases. And what would be even better is if you could tell your interviewer how you would extensively unit test your code beyond these sample tests.

### Why writing tests?

Showing that you know and care about testing is a great advantage. It demonstrates that you fundamentally understand the important part testing plays in the software development process. It gives the interviewer confidence that once hired, you’re not going to start writing buggy code and ship it to production, and instead you’re going to write unit tests, review your code, work through example scenarios, etc.

### Sample tests vs Extensive tests

Before we go into what makes a good test case, we're going to make one clarification around testing at interviews. There are two kinds of testing you may be asked to do (or decide to do) at an interview.

We call the first kind **"sample"** tests: these are small examples that you can feed to your code, and run through it line by line to make sure it works. You may want to do this once your code is written, or your interviewer may ask you to do it. The keyword here is "small": not "simple" or "trivial".

Alternatively, your interviewer may ask you to do more **"extensive"** testing, where they ask you to come up with some good test cases for your solution. Typically, you will not be asked to run them step-by-step. It is more of a mental test design exercise to demonstrate whether you're skilled at unit testing your code.

Fundamentally, these are very different. We'll address each kind separately.

### Extensive testing

Let's start with the bigger topic: what makes for a good test case. If you were to compile an extensive set of tests for your solution, what should these be? Here is a good list to get you started.

- **Edge cases**: Remember that "Constraints" section that we filled in? It's going to come in very handy. Design cases that make sure the code works when the min and/or max values of the constraints are hit. This includes negative numbers, empty arrays, empty strings, etc.
- Cases where there's **no solution**: To make sure the code does the right thing (hopefully you know what it is)
- **Non-trivial functional tests**: these depend very much on the problem. They would test the internal logic of the solution to make sure the algorithm works correctly.
- **Randomized tests**: this makes sure your code works well in the "average" case, as opposed to only working well on human-generated tests (where there's inherent bias).
- **Load testing**: Test your code with as much data as allowed by the constraints. These test your code against being very slow, taking up too much memory or maybe causing a stack overflow.

A good "test set" is a well-balanced combination of the above types. It will include tests that cover most edge cases, a few non-trivial functional tests, and then a series of random tests. These will make sure the code is solid and functionally correct. Finally, some load tests make sure the algorithm works well on the largest and most resource-demanding tests.

### Sample tests

Sample tests are small tests that you run your code on at the interview to make sure it is solid. Now that we've covered the major kinds of tests you may design, which ones should you use as sample tests?

Typically, we stay away from randomized tests and load tests during interviews, for obvious reasons. Instead, we like choosing a small-scale version of a non-trivial functional test, to make sure the code does the right thing. Then, we look at how the code would react to several edge cases, and finally think about whether the code would work well if no solution can be found.

This combination (non-trivial functional + edge + no solution) tends to be the most effective. For the amount of time it takes to design the tests and to run them on your code on a sheet of paper, it gives you the highest certainty in your code.

### How to prepare

There are three good practice activities that will significantly improve your testing skills.

1. Number one is to make sure you understand the fundamental kinds of algorithm tests (mentioned above).
2. The second step is to pay attention to the sample test cases for the given problem. Algorithmic problems usually have a few "open" test cases (part of the problem statement). Pay attention to what cases they’re trying to cover. They are often not sufficient to cover all interesting cases, so you may need to come up with your own that cover more edges cases, for example.
3. The third step is to always fill in the "Test cases" section of the Algorithm Design Canvas. See what scenarios you can come up with.

No matter how you prepare, the key message here is to not ignore testing your solution. Reading your code once it’s written and trying it out with a well-chosen test case is going to do wonders in finding everything from silly typos to actual bugs. Choose the test cases carefully, so that this does not turn into a huge time sink. You will learn to do that with some practice.

Finally, if you propose some good test cases for your solution and check whether it works for them, this should make a very positive impression on the interviewer. One thing we've noticed in our interview experience is that too few candidates remember to test their solution even with one test. And even fewer suggest any unit tests, which they would write in a production setting. Doing this on top of solving the problem will most likely make you stand out.

### Example

<div class="row">
<div class="col-md-8 col-md-offset-2">
<div class="embed-responsive embed-responsive-16by9 text-center">
{{< youtube KKpbPOE3rEQ >}}
</div>
</div>
</div>

### Summary

In this section you learned:

- Why is testing at tech interviews important?
- What tests should you use?
- How can you learn to design the right tests for your solutions?

### What's next?

So far we've covered the important steps when solving algorithmic problems at tech interviews. By this time you have a framework for dealing with them from beginning to end. Now you need to boost your skills with some theory and practice we've prepared for you. First, let's look at the best ways to practice.
