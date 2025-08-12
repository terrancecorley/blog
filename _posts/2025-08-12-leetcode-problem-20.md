---
layout: post
title: "LeetCode Problem #20: Valid Parentheses"
date: 2025-08-12
categories: leetcode
description: "Terrance Corley explores solving LeetCode #20: Valid Parentheses with JavaScript."
---

## Problem

You are given a string `s` consisting of just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid. An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

A string is considered valid if it meets the above conditions.

Here is a [link](https://leetcode.com/problems/valid-parentheses/description/){:target="\_blank"} to the problem on LeetCode.

#### Example 1

Input: `s = "([{}])"`

Output: `true`

Explanation: The string is valid because the parentheses are correctly matched and nested.

#### Example 2

Input: `s = "(]"`

Output: `false`

Explanation: The string is invalid because the parentheses are not correctly matched.

## Approach

### Hash Map & Stack

To determine if the given string of brackets is valid, we'll use a `stack` and a `Map`.

The algorithm works by iterating through the input string one character at a time. When we encounter an opening bracket: `(`, `[`, or `{` we `push` it onto the stack. When we encounter a closing bracket: `)`, `]`, or `}` we check the top of the stack.

The Map is used to quickly determine the correct closing bracket for any given opening bracket. We pop the last item from the stack and use the Map to see if it corresponds to the current closing bracket. If the brackets match, we continue iterating. If they don't, or if the stack is empty when we find a closing bracket, we know the string is invalid.

Finally, after checking the entire string, a valid bracket sequence will result in an empty stack. If there are any opening brackets left in the stack, the string is also considered invalid. This ensures all brackets are correctly opened and closed. This approach provides an efficient solution with a time complexity of O(n) and a space complexity of O(n).

## Solution

```js
function isValidParentheses(s) {
    if (s.length < 2) {
        return false;
    }

    const bracketsMap = new Map([
        ["(", ")"],
        ["[", "]"],
        ["{", "}"],
    ]);

    const stack = [];

    for (let i = 0; i < s.length; ++i) {
        if (bracketsMap.has(s[i])) {
            stack.push(s[i]);
        } else {
            if (stack.length === 0) {
                return false;
            } else {
                const currentItem = stack.pop();

                if (bracketsMap.get(currentItem) !== s[i]) {
                    return false;
                }
            }
        }
    }

    if (stack.length > 0) {
        return false;
    }

    return true;
}
```

## Complexity & Closing Thoughts

#### Time Complexity

O(n), we iterate for the length of the input string.

#### Space Complexity

O(n), we are creating a stack that in the worst case would be based on the entire length of the input string.
