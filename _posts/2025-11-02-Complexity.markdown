---
layout: post
title:  "Understanding Complexity"
date:   2025-11-02 18:46:52 -0400
categories: blog
---
<br><br>
Runtime Efficiency: a measure of the use of computing resources. <br>
The runtime of a loop takes N times the number of statments in the loop. <br>
If there is a nested loop, then it would be N^2 as the runtime. <br>

Growth rate is the change in runtime as N changes. <br>

For O(n) notation, we only consider the highest order term. <br>

**Complexity Classes** <br>
Categories of algorthim efficiency based on the input size N of the algorithm.<br>
O(1) is constant. <br>
O($\log_2(N)$) is logrithmic.<br>
O(N) is linear. <br>
O(N$\log_2(N)$) is log-linear.<br>
O(N^2) is quadratic. <br>
O(2^N) is exponential. <br>

<br>
Adding and removing to and from start of LinkedList is O(1) <br>
Adding and removing to and from end of ArrayList is O(1) <br>
