---
layout: post
title:  "Understanding Searching and Sorting"
date:   2025-12-03 18:46:52 -0400
categories: blog
---
**Note: These notes are based on course material and lectures provided by North Carolina State University.**
<br><br>

**Searching**
<br>
Find elements out of a collection of data.
The collection can be sorted or unsorted. <br>

**Sequential Search**: locates the element being searched for in the list by checking every element from the start to the end of the list. <br>
The complexity is **O(n)**
<br>

**Binary Search**: locates the element being searched for in **SORTED** list by halfing the list each time when checking an element. <br>
The complexity is **O(log(n))** <br>
If element not found after Binary Search: `return -(min + 1);` <br>

**Binary Search Tree** <br>

**Tree**: A directed and acyclic structure of linked nodes
<br>

**directed**: Edges have a direction (one way) <br>
**acyclic**: No Cycles <br>

**Binary Tree**: Tree where each node has at most 2 children <br>
Can be defined as empty (null) <br>
Can be defined as a `root` node that contains: `data`, `left` subtree (can be null), `right` subtree (can be null) <br>

**Terminology**

**Node**: an Object containing `data`, `left` and `right` children Nodes <br>
**Root**: top Node of Tree <br>
**Leaf**: Node with no children <br>
**Branch**: Node that is not the Root nor Leaf <br>

**Parent**: Node that is `this` <br>
**Child**: Node that `this` refers to <br>
**Sibling**: Node with common Parent <br>

**Subtree**: Tree of Nodes reachable to the left/right from the current Node <br>
**Height**: lenght of longest path from Root to a Node <br>
**Level/Depth**: lenght of path from Root to a given Node <br>
**Full Tree**: Tree where every branch has 2 children <br>

**Traversal for Tree**

**Pre-order**: process Root node, then left then right subtrees (FROM START) <br>
**In-order**: **ALWAYS SORTED** process left subtree (FROM END), then Root node, then right subtree (FROM END) <br>
**Post-order**: process left then right subtrees (FROM END), then Root node <br>

**Binary Search Tree**: Binary Tree that is either `null` or <br>
`Root` node that has <br>
`left` subtree with ALL elements with data less than Root's data and <br>
`right` subtree with ALL elements with data greater than Root's data <br>
`left` and `right` subtrees are also Binary Search Trees <br>

**Balanced Tree**: Tree whose subtrees differ in height by at most 1 and the subtrees are also balanced <br>

**Removing** Node with both children: replace node with **min node from right** child/subtree <br>
<br>

**Sorting**

**Selection sort O(n^2)**: look for the smallest element in the list and move it to the front <br>
**Bubble sort O(n^2)**: swap adjacent pairs that are out of order <br>
**Insertion sort O(n^2)**: build an increasingly large sorted front portion <br>
**Merge sort O(nlog(n))**: recursively half the array and sort it and then combine the sorted halves into a sorted array <br>
**Quick sort O(nlog(n))**: recursively partition array based on a middle value <br>
