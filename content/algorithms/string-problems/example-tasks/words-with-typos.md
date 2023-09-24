---
title: "Words with types"
type: docs
weight: 30
---
### Task Statement

You are given a text `T` consisting of words in which there may be typos. Your task is to count how many times a given word `W` is used in this text. However, you need to include in this count the cases in which this word was written with a typo.

It's hard to say if a word contains a typo or not, especially if you don't have a good dictionary. For this task, a word `W'` in `T` is considered to be an instance of `W` if:

- it's exactly the same as `W`
- it has the same length as `W` and up to 2 letters are different
- `W'` can be obtained from `W` by removing or adding 1 letter

For example if `W = banana` the following words are instances of it with typos:

- bamama (2 letters are changed)
- bananas (one added letter)
- banna (one letter was missed out)

The length of `W` will be in the range `[5, 20]`. The input text `T` will be no longer than `10,000` symbols. It will contain only lower case latin letters and spaces used to separate the words.

Input is read from the standard input. On the first line will be the word `W`. On the second line will be the text to search.

The result is written to the standard output. It must consist of one integer - the number of occurrences of `W` in the text including the typos as defined above.

**SAMPLE INPUT**

```
banana
there are three bananas on the tree and one banano on the ground
```

**SAMPLE OUTPUT**

```
2
```

<hr/>

### Solution

This task is mainly about implementing the rules for recognising words with typos as they are defined in the statement.

A good solution will split the text into words and will compare each word from the text with the word `W` given in the input. There are three types of comparisons to be done. The first is trivial - check if the two words are identical.

The second is about counting the mistyped letters. The first main observation is that the words must have the same length because no letters are expected to have been removed or added. If they do have the same length a simple iteration over the two words can be performed and the differences in letters can be counted. If these differences go over 2, then these two words are not the same instance. Here is a sample Ruby method doing that:

```ruby
def matching_with_mistypes?(word1, word2)
  return false if word1.length != word2.length

  diffs = 0
  word1.length.times do |index|
    if word1[index] != word2[index]
      diffs += 1
      return false if diffs > 2
    end
  end

  true
end
```

The third case to check for is when a letter has been removed or added to the original word `W`. In these cases the lengths of the two words must differ by exactly 1. If that's the case we can perform just one iteration over the words and allow for just one difference. We could have two counters for the current position in each of the words. If there is a difference we only increment the counter for the longer word. Eventually if there are more than 1 differences these two words are not the same instance. This is a sample Ruby method implementing this logic:

```ruby
def matching_with_added_letter?(word1, word2)
  return false if (word1.length - word2.length).abs != 1

  small_word = word1.length < word2.length ? word1 : word2
  big_word = word1.length < word2.length ? word2 : word1

  small_word_index = 0
  big_word_index = 0
  misses = 0
  while small_word_index < small_word.length
    if small_word[small_word_index] != big_word[big_word_index]
      misses += 1
      return false if misses > 1
    else
      small_word_index += 1
    end
    big_word_index += 1
  end

  true
end
```

The time complexity of this solution is linear in terms of the length of the input text `T`. Since its maximum length is `10,000` this solution should be fast enough.
