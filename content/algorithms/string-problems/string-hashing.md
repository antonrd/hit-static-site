---
title: "String hashing"
type: docs
weight: 20
aliases: ["/classrooms/algorithm-design/lesson/43"]
---
This is a technique often used when you need to use strings as keys pointing to a set of corresponding values. For example, if you are writing code, which analyses text and needs to record some data for each word found in the text. A good approach would be to compute a hash value for each found word. This hash value would be a number. Numbers make it easier to index parts of memory or disk. If you can quickly refer to a storage location given a string, you can quickly extract the data in this location. For example, when analysing text, when a new word is processed its hash can be used to find the already computed values for it, if such already exist. In many programming languages there are already implemented data structures giving you this functionality by using a hash table of some sort.

A good hashing function usually is one, which computes a polynomial from the symbols of the input string modulo a prime number. For example, if you have a string with symbols `S = S1 S2 ... Sn`, the hash function would compute `H(S) = (S1 * A^(n-1) + S2 * A^(n-2) + ... + Sn-1 * A + Sn) mod P`. Some presentation of the symbols as numbers needs to be used and a value for `A` is to be chosen. The prime number `P` gives you the size of the resulting set of values.

It's important to keep in mind that collisions are possible. Each time when there is a match of hash values you need to check if the string hashed really is the one that we are using as input.

One very useful property of this kind of hash function is that if you compute it for some string `S = S1 S2 ... Sn` you can compute in constant time the hash function value for a string `S' = S2 S3 ... Sn Sn+1`. This is the case because `H(S') = (H(S) - S1 * A^(n-1)) * A + Sn+1` if we ignore the fact that there is also a modulo operation. However, this is easily handled. We will leave you to figure this out as a small homework assignment.

It turns out that this "sliding window" property of the hash function can be used in some pattern matching algorithms. We will look into this topic next.
