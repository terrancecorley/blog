---
layout: post
title: "LeetCode Problem #104: Maximum Depth of Binary Tree"
date: 2025-09-09
categories: leetcode
description: "Terrance Corley explores solving LeetCode #104: Maximum Depth of Binary Tree with JavaScript."
---

## Problem

You are given the `root` of a binary tree, return its maximum depth. The maximum depth of a binary tree is the number of nodes along the longest path from the root node down to the farthest leaf node.

Here is a [link](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/){:target="\_blank"} to the problem on LeetCode.

#### Example 1

Input: `root = [3,9,20,null,null,15,7]`

Output: `3`

Explanation: The maximum depth is 3 because the longest path from the root to a leaf node is 3 nodes long (3 -> 20 -> 15 or 3 -> 20 -> 7).

#### Example 2

Input: `root = [1,null,2]`

Output: `2`

Explanation: The maximum depth is 2 because the longest path from the root to a leaf node is 2 nodes long (1 -> 2).

## Approach

### Post-Order Traversal (DFS)

The problem title gives us a hint as to which strategy we might use, we want the maximum depth so it makes sense to use a depth-first search algorithm, specifically a post-order one.
We can do our algorithm recursively, our base case will be an empty node in which case we return zero. Otherwise, we will return `Math.max(left, right) + 1` to account for how many levels the subsequent subtrees are, the `+ 1` here
represents the current node's level.

## Solution

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
const maxDepth = function (root) {
    if (!root) {
        return 0;
    }

    let left = maxDepth(root.left);
    let right = maxDepth(root.right);

    return Math.max(left, right) + 1;
};
```

## Complexity & Closing Thoughts

#### Time Complexity

O(n), we must visit every node in the tree exactly once.

#### Space Complexity

O(h)/O(n), we are building a stack in memory for each level in the tree.
