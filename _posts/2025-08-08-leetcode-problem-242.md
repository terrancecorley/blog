---
layout: post
title: "LeetCode Problem #242: Valid Anagram"
date: 2025-08-08
categories: leetcode
description: "Terrance Corley explores solving LeetCode #242: Valid Anagram with JavaScript."
---

## Problem

You are given two strings, `s` and `t`. Write a function to determine if `t` is an anagram of `s`. Return `true` if it is an anagram, and `false` otherwise.

Here is a [link](https://leetcode.com/problems/valid-anagram/description/){:target="\_blank"} to the problem on LeetCode.

#### Example 1

Input: `s = "caret", t = "trace"`

Output: `true`

Explanation: Both strings contain the same characters and character amounts in different orders.

#### Example 2

Input: `s = "hello", t = "world"`

Output: `false`

Explanation: The strings do not contain the same characters or character amounts.

## Approach

### Counting With Maps

An anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once. The first
thing that sticks out to me is that if the strings are of different lengths, they cannot be anagrams, so we can exit and return `false` in that case. Otherwise, the bulk
of our algorithm will be creating a frequency counter `Map` for each string, these will contain the characters as keys and the character occurrences as values. Then we can
loop through one of our Maps. If a given `key` does not exist in the other Map or the `value` does not match the value in the other Map, we have failed the anagram condition and can return false.
We can have a default return `true` statement that runs after our loop is done.

## Solution

```js
function isAnagram(s, t) {
    if (s.length !== t.length) {
        return false;
    }

    const frequencyCounterS = new Map();
    const frequencyCounterT = new Map();

    for (let char of s) {
        frequencyCounterS.set(char, (frequencyCounterS.get(char) || 0) + 1);
    }

    for (let char of t) {
        frequencyCounterT.set(char, (frequencyCounterT.get(char) || 0) + 1);
    }

    for (let [key, value] of frequencyCounterS) {
        if (
            !frequencyCounterT.has(key) ||
            value !== frequencyCounterT.get(key)
        ) {
            return false;
        }
    }

    return true;
}
```

## Complexity & Closing Thoughts

#### Time Complexity

O(n) + O(m), because we are creating Maps based on our inputs. The `for loop` here is also a O(n) operation.

#### Space Complexity

O(n) + O(m), because we are creating Maps based on our inputs.
