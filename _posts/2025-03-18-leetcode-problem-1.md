---
layout: post
title: "LeetCode #1: Solving Two Sum"
date: 2025-03-18
categories: leetcode
description: "Terrance Corley explores solving LeetCode #1: Two Sum with a TypeScript solution."
---

## Problem

You are given an array of integers `nums` and a target integer `target`. Return the indices of the two integers in `nums` that sum up to `target`.
You can assume there are **exactly two integers** that add up to `target`. You may not use the same index twice. Return the two indices in an array.
Can you come up with a solution that is less than O(n<sup>2</sup>) time complexity?

Here is a [link](https://leetcode.com/problems/two-sum/description/) to the problem on LeetCode.

#### Example 1

Input: nums = [4, 3, 5, 8], target = 9  
Output: [0, 2]  
Explanation: 4 + 5 = 9, therefore we return the respective indices

## Approaches

### Approach One - Sort & Two Pointer

We need to find the two indices in the array that add up to target and ideally in a time complexity less than O(n<sup>2</sup>). My first idea is maybe we can sort the array first in ascending order. Then try a two pointer solution. One pointer `left` starting at the
beginning of the array and the other pointer `right` can start at the end of the array. We will check to see if the sum of those two numbers equals our target. If not, check if the sum is greater than target. If it is, decrement the right pointer by 1 because we know the sum is too big. If the sum is less than
target, increment the left pointer as we know the sum is too small. We can run this loop until the value we are summing equals the target since the instructions guarantee there is at least one solution. Once the target sum is found, we can simply return an array with [`left`, `right`]. Or so I thought, it turns out this
approach will not work since when we sorted the array we lost the **original indices** that we were meant to return because after sorting, the integers in the array will now most likely be at different indices. This caveat means we will have to take another approach.

### Approach Two - Hash Map, Sort, & Two Pointer

My second thought was to do everything from approach one, but before doing that logic, I would loop over the existing nums array and create a hash map. This way I can save the correct original indices and when we meet are target sum condition, we can return the index reference from the hash map as opposed to the
indices in the sorted array. The problem with this approach I realized, is what happens if the same number appears twice in the nums array? We overwrite the existing index value, losing the first index of that number forever. So that won't work either.

### Approach Three - Hash Map & Using Maths

I ended up having to look at the solution. We were so close. We still needed the hash map, but instead of sorting or doing a two pointer search, we could instead leverage some math. Since we know there is exactly **one solution** to the problem, that means
there are definitely two, and only two numbers that add up to `target`. We can use this info to our advantage. The first step now is to create an empty hash map. We then can simply loop over the nums array. For each iteration, if the target minus the current
element exists in our map, we have our answer and we can return the appropriate indices. Otherwise, we can just add the current element and it's respective index to our map. Let's look at this in code.

## Solution

```ts
function twoSum(nums: number[], target: number): number[] {
  const numsMap = new Map();

  for (let [index, value] of nums.entries()) {
    if (numsMap.has(target - value)) {
      return [index, numsMap.get(target - value)];
    } else {
      numsMap.set(value, index);
    }
  }
}
```

## Complexity & Closing Thoughts

#### Time Complexity

The time complexity for the above solution would be O(n), linear time complexity. This is because we may have to search the entire nums array to find the two numbers that add up to target.

#### Space Complexity

The space complexity for this would also be O(n). That is because if we have to search the entire array, then we are creating _n_ amount of key value pairs in our map.
