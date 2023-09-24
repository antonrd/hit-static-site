---
title: "Writing the code"
type: docs
weight: 60
---
At this point, you’ve already nailed the constraints of a problem, iterated on a few ideas, evaluated their complexities and eventually picked the one you’re going to implement. This is a great place to be!

We see many people who jump straight into coding, ignoring all previous steps. This is bad in real life, and it’s bad when done at your interview. Never, ever jump straight into coding before having thought about and discussed constraints, ideas and complexities with your interviewer.

Now that we took that out of our system, let’s focus on how you code at the interview.

The one thing about coding (other than rushing into it too quickly) that many people struggle with is that coding in your IDE is not the same as coding on a whiteboard / a shared document / using some online system (in short: “outside your IDE”). As engineers, we’ve become so accustomed to relying on our IDEs (which is not bad), that when presented with a blank sheet of paper, we are lost. While this may have been OK at your day job, at an interview it simply doesn’t work.

This is why you need special preparation for “interview coding”. Say hello to the big “Code” section of the Canvas, waiting to be filled with source code. At first it may be a bit tedious to write your code on paper, but very quickly you get used to it and you become more efficient. And the great news is that being able to code on a sheet of paper will not only boost your interviewing skills - it will also make you a better engineer overall.

Some of the key things to keep in mind when coding outside your IDE:

- **Think before you code.** Especially if you’re coding on a sheet of paper (where there’s no “undo”), if you’re not careful everything could become very messy very quickly
- Coding outside of an IDE does not give you permission to stop abiding by good code style. **Make sure you name your variables properly**, indent nicely, write clean code, etc. etc.
- It’s even more important to **decompose your code** into small logical pieces and **NOT copy-paste**
- **Read your code** multiple times before you claim it’s ready. You don’t have the luxury to compile, see if it compiles, run, see if it runs, and then debug for 4 hours. Your code needs to work off the bat.

> Nowadays it seems like more and more of the tech interviews are conducted online, even the so-called "onsite" ones. This usually means coding in a shared editor of some sort, but not necessarily a full-fledged IDE. This is probably easier than writing on a whiteboard or paper, but many of the points in this lesson apply in these cases. Solving problems in websites like LeetCode provides a similar experience where there is no auto-completion by default for example, but there are helpers like syntax highlighting and automatic identation. Generally, it is a good idea to check beforehand in what way will the code during your interviews be written. Once you know that, try to find a way to simulate this kind of environment and write your solutions in it. If it is not clear exactly how the coding part of the interviews will be conducted, then your best bet probably is to practice on paper, whiteboard or in a simple editor, just to be prepared for all possibilities.

That’s it. Now say goodbye to your IDE for a while, and off to practicing!

### Example

Let's apply what we have learned to our ZigZag problem. Remember - do not use your IDE.

<div class="row">
<div class="col-md-8 col-md-offset-2">
<div class="embed-responsive embed-responsive-16by9 text-center">
{{< youtube OmsHMhdx-yk >}}
</div>
</div>
</div>

<br>
Below is the source code that was written in the video:

```cpp
int longestZigZagSequence(int N, std::vector<int> a) {
  std::vector<int> up;
  std::vector<int> down;
  int bestLength = 1;

  up.push_back(1);
  down.push_back(1);

  for (int i = 1; i < N; i++) {
    up.push_back(1);
    down.push_back(1);

    for (int j = 0; j < i; j++) {
      if (a[i] > a[j]) {
        up[i] = max(down[j] + 1, up[i]);
      }
      if (a[i] < a[j]) {
        down[i] = max(up[j] + 1, down[i]);
      }
    }
    bestLength = max(bestLength, max(up[i], down[i]));
  }

  return bestLength;
}
```

### Summary

In this section you learned:

- When should you start coding at the interview?
- Coding for an interview is not like coding in your IDE. How can you prepare for that best?
- Look at important tips for how to write the code. We also write the code for an example problem.


### What's next?

Let's wrap up the essential steps of a tech interview with a very important one - testing. You can never be 100% sure that your solution is correct unless you run it through some tests. Doing that has multiple positive effects at an interview. See how to test your solutions.
