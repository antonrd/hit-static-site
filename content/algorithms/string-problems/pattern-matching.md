---
title: "Pattern matching"
type: docs
weight: 30
aliases: ["/classrooms/algorithm-design/lesson/44"]
---
A very popular string problem is to find one, some or all occurrences of one string within another. Usually the string to search for is called a *pattern*. One example task would be given a text `T` (with length `Lt`) and a pattern `P` (with length `Lp`) to find all the starting positions of substrings in `T` that are equal to `P`. This could be useful in a number of text processing applications, like searching in text or mapping documents to keywords.

Once given such a task, probably the most straight forward solution would be to try matching the string `P` against all substrings in `T` with the length of `P`. For example, if given `T = mississippi` and `P = issi` you would first check against the first substring `miss` and this would produce a mismatch on the very first symbol. However, the next substring `issi` will match `P`. Then you continue with the next substring - `ssis` - a mismatch again. There will be one more match with `issi` starting at symbol number 5 and all the rest of the substrings will not match.

This approach is easy to implement but it's worst-case running time can be terrible - `O(Lt * Lp)`. Sometimes `Lt` and `Lp` could be quite big rendering this approach not suitable. Still, you need to evaluate the task at hand and the possible inputs. For random strings it may be the case that in most of the cases there is a mismatch between `P` and the substrings of `T` in the first 1 or 2 symbols. If the matches are very few, this would mean that your running time will be much better than the expected worst-case. However, if your solution needs to solve an input in which `P` is contained in `T` many times you may need to think of a better algorithm. A very extreme and simple example is one where `T` contains the same latin letter many times and `P` is constructed of this letter only. For example: `T = "tttt...tttt"` and `P="tt..tt"`.

In the next section we will look into smarter algorithm for this kind of problem and will provide you with more useful reading material on the topic.
