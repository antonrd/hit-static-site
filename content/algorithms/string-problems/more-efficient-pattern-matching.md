---
title: "More efficient pattern matching"
type: docs
weight: 40
aliases: ["/classrooms/algorithm-design/lesson/45"]
---
It was mentioned in a previous lesson that a hashing function could be used in string pattern matching due to its "sliding window" property. This is the idea of the *Rabin-Karp algorithm*. In the resources below we've included links to Wikipedia and TopCoder articles about it. It is relatively easy to implement and offers an improvement over the previous algorithm but it's worst-case running time is still `O(Lt * Lp)`.

That is why it's worth considering some more advanced algorithms. A very nice algorithm worth learning and implementing is the *Knuth-Morris-Pratt* algorithm. The algorithm first constructs a table with some data based on the pattern with time complexity `O(Lp)`. Then for the search of the pattern within the text it uses the data from the table and this takes `O(Lt)`. These are worst-case running times. We encourage you to learn this algorithm and you will also have the chance to apply it in one of the practice problems in this section. The links about it from Wikipedia and Topcoder, found below, can be useful.

Some other techniques worth mentioning are the *Aho–Corasick algorithm*, *suffix trees* and *suffix arrays*.

### Resources

- TopCoder on <a href="https://www.topcoder.com/thrive/articles/Introduction%20to%20String%20Searching%20Algorithms" target="_blank" rel="noopener noreferrer">Rabin-Karp and Knuth-Morris-Pratt Algorithms</a>
- Wikipedia on <a href="https://en.wikipedia.org/wiki/Rabin%E2%80%93Karp_algorithm" target="_blank" rel="noopener noreferrer">Rabin-Karp</a>
- Wikipedia on <a href="https://en.wikipedia.org/wiki/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm" target="_blank" rel="noopener noreferrer">Knuth-Morris-Pratt</a>
- Wikipedia on <a href="https://en.wikipedia.org/wiki/Aho%E2%80%93Corasick_algorithm" target="_blank" rel="noopener noreferrer">Aho–Corasick algorithm</a>
- Wikipedia on <a href="https://en.wikipedia.org/wiki/Suffix_array" target="_blank" rel="noopener noreferrer">suffix arrays</a>
- Wikipedia on <a href="https://en.wikipedia.org/wiki/Suffix_tree" target="_blank" rel="noopener noreferrer">suffix trees</a>
