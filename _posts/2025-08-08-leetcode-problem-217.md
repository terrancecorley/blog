---
layout: post
title: "LeetCode Problem #217: Contains Duplicate"
date: 2025-08-08
categories: leetcode
description: "Terrance Corley explores solving LeetCode #217: Contains Duplicate with JavaScript."
---

## Problem

You are given an integer array `nums`. Return `true` if any value appears more than once in the array, and return `false` if every element is distinct.

Here is a [link](https://leetcode.com/problems/contains-duplicate/description/){:target="\_blank"} to the problem on LeetCode.

#### Example 1

Input: `nums = [1, 1, 2, 3]`

Output: `true`

Explanation: The number 1 appears twice in the array.

#### Example 2

Input: `nums = [1, 2, 3, 4]`

Output: `false`

Explanation: All numbers are distinct in the array.

## Approach

### Approach One: Convert Input To Set, Compare Lengths

The goal is to determine if our input has any duplicate integer values. We could take advantage of the built in `Set` data structure in JavaScript
which only allows for distinct values. We can initialize out Set with the input array and then compare the lengths of the original input and our set. If the lengths
are different then we know there must be duplicate values and we can return a boolean based on that result. This solution would technically give us the same time
and space complexity as approach two, but there is something to consider with this approach. What about if the input was a million items long, but a duplicate value was
found at index two. That means we created a Set with a size of one million just to find the duplicate value at the second index. Approach two offers a better way
to determine duplicates without creating a Set based on the entire input and will also end execution early if a duplicate is found.

### Approach Two (Selected Approach): Create Empty Set, Iterate Through Input

We can still take advantage of a loop, but instead of feeding our input array into it initially, we can initialize it as empty. Then just loop through our input array with a
traditional `for loop`. If we haven't seen the value before, we add it to our Set and continue looping. If we have seen the value, end the loop and return `true`. If the entire
loop runs without returning true then we know we don't have duplicates and can return `false`.

## Solution

```js
function containsDuplicate(nums) {
    const numsSet = new Set();

    for (let i = 0; i < nums.length; ++i) {
        if (numsSet.has(nums[i])) {
            return true;
        }

        numsSet.add(nums[i]);
    }

    return false;
}
```

## Complexity & Closing Thoughts

#### Time Complexity

O(n), we looped through the `nums` array a single time resulting in linear time complexity.

#### Space Complexity

O(n), in the worst case scenario where the `nums` array contains all unique values, that means our loop would iterate through the entire array and add to out `Set`
at each iteration, resulting in a linear data structure based on the input length.
