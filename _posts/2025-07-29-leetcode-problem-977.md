---
layout: post
title: "LeetCode #977: Squares of a Sorted Array"
date: 2025-07-29
categories: leetcode
description: "Terrance Corley explores solving LeetCode #977: Squares of a Sorted Array with a TypeScript solution."
---

## Problem

You are given an integer array `nums` sorted in increasing order. Your task is to return an array of the squares of each number in `nums`, also sorted in increasing order.

Bonus points: Can you find an O(n) time complexity solution?

Here is a [link](https://leetcode.com/problems/squares-of-a-sorted-array/description/){:target="\_blank"} to the problem on LeetCode.

#### Example 1

Input: nums = [-4, 0, 3, 5]
Output: [0, 9, 16, 25]  
Explanation: After squaring, the array becomes [16, 0, 9, 25].
After sorting, it becomes [0, 9, 16, 25].

## Approach

### Approach One - Two Pointer & Pre-Defined Array

Going straight for the bonus points, let's see how we can do this in O(n) time. We can take advantage of the fact that the input array is already sorted in increasing order.
We will use a two pointer solution here in combination with a new array that we will fill with default values (0 to keep things simple), then in our while loop we will assign new values to these array items, starting at the end of the array. To make this O(n) time, we can initialize our return array
with `nums.length-1` number of items and `fill` them in as 0. This way when we assign the actual return values, that will be done in constant time.

The alternative would be initializing an empty array and shifting items
onto the front at each iteration, but that would cause an O(n) time complexity because at each iteration the array would need to re-index. We will already have O(n) time complexity from needing the two pointer approach in a while loop, so this added O(n)
operation at each each iteration would give us a complete time complexity of O(n)², resulting in no bonus points. Instead, we will update values in the initialized array starting at the end of the array for the duration of the while loop.
At each iteration we will check which pointer value is greater in order to know which value will be used when updating our array, we should use `Math.abs()` for the comparison since our input could involve negative integers. We should increment our left pointer or decrement our right pointer depending on which one we used for value assignment.
We will also decrement the variable that should point to the index we are updating in our array (see solution for clarity). After the loop runs, we can return that now modified array which
holds our result.

## Solution

```ts
function sortedSquares(nums: number[]): number[] {
    const result_array = new Array(nums.length).fill(0);
    let left_pointer = 0;
    let right_pointer = nums.length - 1;
    let result_array_idx = result_array.length - 1;

    while (left_pointer <= right_pointer) {
        if (Math.abs(nums[left_pointer]) > Math.abs(nums[right_pointer])) {
            result_array[result_array_idx] =
                nums[left_pointer] * nums[left_pointer];
            left_pointer++;
        } else {
            result_array[result_array_idx] =
                nums[right_pointer] * nums[right_pointer];
            right_pointer--;
        }

        result_array_idx--;
    }

    return result_array;
}
```

## Complexity & Closing Thoughts

#### Time Complexity

We are creating a new array based on the length of the input as well as looping for the length of that array by doing our while loop, giving us an overall time complexity of O(n).

#### Space Complexity

Creating the array gives us a space complexity of O(n), creating the variables is O(1), overall space complexity is O(n).
