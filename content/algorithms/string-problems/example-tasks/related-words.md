---
title: "Related words"
type: docs
weight: 20
aliases: ["/classrooms/algorithm-design/lesson/29"]
---
### Task Statement

A company analysing news articles needs to identify relations between words in these articles. One simple idea that its engineers have is to look at pairs of words that are often seen close to each other.

You goal will be to help this company in its experiment. Write a program, which given a text T and a word W, finds the word, which is most often seen around word W.

We define “seen around word W” as a word, which is within the N words before and after an occurrence of the word W.

For example if we have the text *“It is a nice day today, the sun is shining.”* and our word W is “day” and N=3, then the words around W are “is”, “a”, “nice”, “today”, “the” and “sun”. These are the words that come immediately before or after “day” within the distance of 3.

The goal is for all occurrences of W in T to consider the words that are around these occurrences and to return the one that is most often seen. If there are more than one such words return the one that comes first lexicographically.

Don’t count the occurrences of the word W around other occurrences of it. Also, don’t count the same word more than once even if it’s around more than one occurrence of W.

If the text has no occurrences of the word W, return the string “N/A” (quotes are not part of the string).

The input is read from the standard input. The first line contains the text T. The second line contains the word W and the third line contains the number N.

The result must be printed to the standard output. It must contain one word as was described above.

The text T will contain words consisting of only lower-case and upper-case latin letters and numbers. When counting words you must ignore the casing. This means that “today” and “Today” is the same word. **When printing the result use lower-case.** The text T will also contain other symbols like ‘,’, ‘.’, ‘!’, ‘?’, but not only. You must strip out everything that is not a letter or a digit. Such symbols should not be counted as part of the words.

Here is an example:

**SAMPLE INPUT**

```
It is a nice day today, the sun is shining. However, the weather is expected to get worse the following few days. Nice day by day weather forecasts can be found literally everywhere on the “Internet”. So, it is quite easy to know what to expect tomorrow.
day
3
```

**SAMPLE OUTPUT**

```
nice
```

There are three occurrences of the word ‘day’ within the text. Note that we don’t count the word ‘days’ as an occurrence. Only exact word matches are considered.

Near the first occurrence are the words ‘is’, ‘a’, ‘nice’, ‘today’, ‘the’, ‘sun’.

Near the second occurrence are the words ‘few, ‘days’, ‘nice’, ‘by’, ‘day’, ‘weather’. However, we won’t consider the word ‘day’ because it’s the same as W in the example.

Near the third occurrence are the words ‘nice’, ‘day’, ‘by’, ‘weather’, ‘forecasts’, ‘can’. However, the first four words are already covered by the second occurrence of W, so we WILL NOT count the one more time.

In the end we have the following list of words that were found to be around occurrences of the word ‘day’: 'is', 'a', 'nice', 'today', 'the', 'sun', 'nice', 'few', 'days', 'by', 'weather', 'forecasts', 'can'.

In this list all words are seen only once except the word ‘nice’, which is seen twice. This is why this is the correct output for this sample input.

<hr/>

### Solution

To solve this task you basically need to implement the approach that is described in the task statement. It is also a task that would be likely to occur in you everyday job if you are analysing text, searching for relations between terms, improving a search engine's capabilities and so on.

Initially there are a few preprocessing steps that need to be taken to prepare the input text. You will need to downcase the string and then strip out all symbols that are not latin letters or numbers.

This is probably the simplest form of "cleaning" a text for analysis. In this task you don't need to do that but sometimes in such tasks you would need to stem the words, so that words like "train", "training", "trained", "trainer", etc, are matched to the same thing - the root "train". Also, the removal of stopwords is a desirable step, so that you don't take into consideration words that appear often in text but are not interesting for your purposes. In this task we're keeping things simple and don't require you to do that. You can find some articles about these techniques in the resources list below.

Back to our task. Once you've performed the preprocessing steps you will have a text containing words made of lower-case latin letters and digits. You can split the text by the spaces found in it to obtain a list of words. Many programming languages have functions for splitting strings by a given character in their standard libs. In case you need to implement this it will be a good practice for you though it's not a though problem.

Now that you have a list of words you can traverse it once, say from left to right, and count the words found around occurrences of `W`. Each time a word from the text `T` matches `W` you can traverse the words around this occurrence and take them into account. The task is a bit more complicates because you must not count the same word more than once so you would need to "remember" the right most word that has been inspected so far.

For counting the number of occurrences of each word seen an occurrence of the word `W` you could use a hash table. This technique was briefly covered in the overview lesson. Again, many programming languages will give you for free a data structure, which can have strings as keys.

In the end you just need to find the word with the largest number of occurrences in the hash. If there are many words getting the first lexicographically is rather easy.

Here is some source code in Ruby implementing a solution:

```ruby
# t - the input text
# w - the input search word
# n - the number of words around occurrences of `w` to search through

words = t.downcase.split.map { |word| word.gsub(/[^a-z0-9]/, '') }

hash = Hash.new(0)

last_covered = -1
words.each_with_index do |word, i|
  if word == w
    start = [last_covered+1, i-n, 0].max
    (start...i).each do |j|
      hash[words[j]] += 1 if words[j] != w
    end
    start = [last_covered+1, i+1].max
    stop = [i+n+1, words.count].min

    (start...stop).each do |j|
      hash[words[j]] += 1 if words[j] != w
    end

    last_covered = i+n
  end
end

ans = nil
ans_cnt = 0
hash.each do |k, v|
  if v > ans_cnt
    ans_cnt = v
    ans = k
  elsif v == ans_cnt && k < ans
    ans = k
  end
end

if ans
  puts ans
else
  puts 'N/A'
end
```

### Resources

- Wikipedia on <a href="https://en.wikipedia.org/wiki/Stemming" target="_blank" rel="noopener nofollow">stemming</a>
- A lesson on <a href="http://nlp.stanford.edu/IR-book/html/htmledition/stemming-and-lemmatization-1.html" target="_blank" rel="noopener nofollow">stemming and lemmatizaion</a>
- Wikipedia on <a href="https://en.wikipedia.org/wiki/Stop_words" target="_blank" rel="noopened nofollow">stop words</a>
- Another short lesson from Stanford on <a href="http://nlp.stanford.edu/IR-book/html/htmledition/dropping-common-terms-stop-words-1.html" target="_blank" rel="noopened nofollow">stop words</a>
