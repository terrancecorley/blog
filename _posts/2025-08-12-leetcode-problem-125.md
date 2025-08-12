---
layout: post
title: "LeetCode Problem #125: Valid Palindrome"
date: 2025-08-12
categories: leetcode
description: "Terrance Corley explores solving LeetCode #125: Valid Palindrome with JavaScript."
---

## Problem

You are given a string `s`. Write a function to determine if `s` is a valid palindrome, considering only alphanumeric characters and ignoring cases. Return `true` if it is a valid palindrome, and `false` otherwise.
A string is a valid palindrome if it reads the same backward as forward after removing all non-alphanumeric characters and ignoring case.

Here is a [link](https://leetcode.com/problems/valid-palindrome/description/){:target="\_blank"} to the problem on LeetCode.

#### Example 1

Input: `s = 'Race car'`

Output: `true`

Explanation: The string reads the same backward as forward.

#### Example 2

Input: `s = dog`

Output: `false`

Explanation: The string does not read the same backward as forward.

## Approach

### Two Pointer Pattern Check

The biggest hint I get from this problem statement is the fact that a palindrome needs to read the same forwards as it does backwards. This immediately made me think of a two pointer approach.
To start, I will trim the leading and trailing whitespace on a given string and lowercase it. I will initialize a left and right pointer for the string. For the last variable we'll need, I'll create a regex pattern
that makes sure a given character is alphanumberic and lowercase. While the left pointer and right pointer have yet to meet, I will have inner while loops that increment left and decrement right
should we be on an invalid character we don't want to consider for our palindrome comparison. Otherwise, we can use the `charCodeAt` method to see if the characters are the same. If any comparison
returns a `false` result, we can return false. Otherwise, increment left and decrement right to continue our loop. If no invalid comparisions are found after looping the entire string, we can return `true`.

## Solution

```js
function validPalindrome(s) {
    let sModified = s.trim().toLowerCase();
    let left = 0;
    let right = sModified.length - 1;
    let validCharacterPattern = /[a-z0-9]/;

    while (left < right) {
        while (
            validCharacterPattern.test(sModified[left]) === false &&
            left < right
        ) {
            left++;
        }

        while (
            validCharacterPattern.test(sModified[right]) === false &&
            right > left
        ) {
            right--;
        }

        if (sModified.charCodeAt(left) !== sModified.charCodeAt(right)) {
            return false;
        }

        left++;
        right--;
    }

    return true;
}
```

## Complexity & Closing Thoughts

#### Time Complexity

O(n), we are iterating once through the entire string and also creating a new string from the given one.

#### Space Complexity

O(n), we created a new string from the given one.
