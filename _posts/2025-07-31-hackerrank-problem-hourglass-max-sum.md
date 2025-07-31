---
layout: post
title: "Hackerrank: Hourglass Max Sum"
date: 2025-07-31
categories: hackerrank
description: "Terrance Corley explores solving the Hourglass Max Sum problem on Hackerrank."
---

## Problem

The Hourglass Max Sum problem on Hackerrank requires you to find the maximum sum of an hourglass shape in a 6x6 2D array. An hourglass is defined as a subset of values with the following pattern:

```
a b c
  d
e f g
```

Here is a [link](https://www.hackerrank.com/challenges/2d-array/problem){:target="\_blank"} to the problem on Hackerrank.

#### Example 1

Input:

```
[
    [1 1 1 0 0 0]
    [0 1 0 0 0 0]
    [1 1 1 0 0 0]
    [0 0 2 4 4 0]
    [0 0 1 2 4 0]
    [0 0 1 2 4 0]
]
```

Output: 19

Explanation: The hourglass with the maximum sum is:

```
2 4 4
  1
1 2 4
```

## Approach

### Approach One - Double For Loop With Running Sum

The first thing I noticed with this problem are the variables I'll need and my method of traversal. At a high level I know I need to traverse the rows and columns
in this 2D array and find the maximum sum of values within the given bounds of an hourglass shape. That means I'll need to track the maximum hourglass sum, the current
hourglass sum, and I'll need some logic on when and how to build up the sum for a given hourglass. With this approach in mind, we can initialize a maximum sum var, use a double for loop to
traverse the rows and columns of the grid, then have conditional logic that checks if we are at the "start" (top left) of an hourglass shape within the defined bounds, and if we are we can build our current sum.
When we are done building our sum for a given hourglass, we can update our maximum sum appropriately. We return that value at the end of our double for loop. You will see I created a separate function for
handling the updating of current sum, not completely necessary but in the moment I decided to break that logic out.

## Solution

```js
function hourglassSum(arr) {
    let maxSum = -Infinity;

    function handleCurrentSumAdd(currentSum, row, col) {
        return currentSum + arr[row][col];
    }

    for (let row = 0; row < arr.length; ++row) {
        for (let col = 0; col < arr[row].length; ++col) {
            if (row <= 3 && col <= 3) {
                let currentSum = arr[row][col];
                currentSum = handleCurrentSumAdd(currentSum, row, col + 1);
                currentSum = handleCurrentSumAdd(currentSum, row, col + 2);
                currentSum = handleCurrentSumAdd(currentSum, row + 1, col + 1);
                currentSum = handleCurrentSumAdd(currentSum, row + 2, col);
                currentSum = handleCurrentSumAdd(currentSum, row + 2, col + 1);
                currentSum = handleCurrentSumAdd(currentSum, row + 2, col + 2);
                maxSum = Math.max(currentSum, maxSum);
            }
        }
    }

    return maxSum;
}
```

## Complexity & Closing Thoughts

#### Time Complexity

O(1), usually a double for loop would give us O(n)² but since our `arr` parameter is always expected to be 6x6, that would qualify as a constant giving us constant time complexity.

#### Space Complexity

O(1), we only created variables containing primitives and a helper function, both require constant space.
