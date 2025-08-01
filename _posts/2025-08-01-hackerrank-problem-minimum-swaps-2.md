---
layout: post
title: "Hackerrank: Minimum Swaps 2"
date: 2025-08-01
categories: hackerrank
description: "Terrance Corley explores solving the Minimum Swaps 2 problem on Hackerrank."
---

## Problem

You are given an array of consecutive integers. The array is not sorted and contains no duplicates. You need to find the minimum number of swaps required to sort the array in ascending order.

Here is a [link](https://www.hackerrank.com/challenges/minimum-swaps-2/problem){:target="\_blank"} to the problem on Hackerrank.

#### Example 1

Input:

```
[7, 1, 3, 2, 4, 5, 6]
```

Output:

```
5
```

Explanation:
The array can be sorted in ascending order with the following swaps:

```
1. Swapped 7 and 6: [6, 1, 3, 2, 4, 5, 7]
2. Swapped 6 and 5: [5, 1, 3, 2, 4, 6, 7]
3. Swapped 5 and 4: [4, 1, 3, 2, 5, 6, 7]
4. Swapped 4 and 2: [2, 1, 3, 4, 5, 6, 7]
5. Swapped 2 and 1: [1, 2, 3, 4, 5, 6, 7]
```

## Approach

### Approach One - Loop & Conditional Swap

We can take advantage of the fact that arrays are index-based and our array contains consecutive non-duplicate values. If a value is at the correct position in the array, it's value would be index + 1.
If this is not the case for a given index value, we can find the index this value should be in and do a swap. We can iterate through the array to do this for every value
and have a variable to track the amount of times we need to swap. We also need to make sure to consider that when we swap values, the second value in the swap may not be at the correct index, so we will
need to check this index again after the swap has been done.

## Solution

```js
function minimumSwaps(arr) {
    let minSwaps = 0;

    for (let i = 0; i < arr.length; ++i) {
        if (arr[i] !== i + 1) {
            let correctPosition = arr[i] - 1;
            let temp = arr[i];

            arr[i] = arr[correctPosition];
            arr[correctPosition] = temp;

            minSwaps += 1;
            --i;
        }
    }

    return minSwaps;
}
```

## Complexity & Closing Thoughts

#### Time Complexity

O(n), we only iterate over the length of the array a single time.

#### Space Complexity

O(1), all variables are storing primitives.
