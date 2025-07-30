---
layout: post
title: "LeetCode #713: Subarray Product Less Than K"
date: 2025-07-30
categories: leetcode
description: "Terrance Corley explores solving LeetCode #713: Subarray Product Less Than K with a TypeScript solution."
---

## Problem

You are given an array of integers `nums` and an integer `k`. Your task is to find the number of contiguous subarrays where the product of all the elements in the subarray is less than `k`.

Here is a [link](https://leetcode.com/problems/subarray-product-less-than-k/description/){:target="\_blank"} to the problem on LeetCode.

#### Example 1

Input: nums = [2, 3, 4, 5], k = 12

Output: 5

Explanation: The subarrays that satisfy the condition are:

- [2]
- [3]
- [4]
- [5]
- [2, 3]

## Approach

### Approach One - Two Pointer Sliding Window

You could solve this problem with a double for loop, but that would yield a O(n)² time complexity. We can utilize the sliding window technique to get the time complexity down to O(n).
To use this technique we can initialize a left pointer, the right pointer will be defined in our single for loop. We will also need to initialize a variable to contain our result, as well
as a variable to contain the current product as we iterate through our array. Inside our for loop we will have a while loop if our current product is greater or equal to k, which will shrink our window size.
At the end of the for loop, we can return the result.

## Solution

```ts
function numSubarrayProductLessThanK(nums: number[], k: number): number {
    if (nums.length === 0 || !Array.isArray(nums)) {
        return 0;
    }

    let left = 0;
    let result = 0;
    let product = 1;

    for (let right = 0; right < nums.length; right++) {
        product = product * nums[right];

        while (left <= right && product >= k) {
            product = product / nums[left];
            left++;
        }

        result += right - left + 1;
    }

    return result;
}
```

## Complexity & Closing Thoughts

#### Time Complexity

O(n), we loop through the `nums` array a single time resulting in the optimal solution.

#### Space Complexity

O(1), all variables created are primitives resulting in constant space memory allocation.
