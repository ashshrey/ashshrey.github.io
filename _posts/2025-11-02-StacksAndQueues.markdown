---
layout: post
title:  "Understanding Stacks and Queues"
date:   2025-11-02 18:46:52 -0400
categories: blog
---
<br><br>
Stacks store items as last in, first out. Queues store items as first in, first out. <br>
For Stacks, objects are removed in reverse order from how they are added. For Queues, objects are removed in the same order as how they are added. <br>
Stacks are like a stack of books. Queues are like a line of people. <br>

**Stacks and Queues are Abstract Data Types**
Abstract Data Types are specification of a collection and what operations can be performed on that data. It isn't how a collection is implemented. They are a conceptual model. <br>
Lists are Linear Data Structures. <br>
In Java, Stack is a class and Queue is an Interface.<br>
LinkedList implements Queue in Java<br>

Stacks have methods: push(element), pop(), peek()<br>
Queues have methods: add(element), remove(), element(). offer(element), poll(), peek() don't throw exceptions. <br>

Stacks are more efficient with push() and pop() when using a LinkedList.
**Top of Stack at index = 0, LinkedList is better.** This means adding/removing to and from the front of LinkedList<br>
**Top of Stack at size, ArrayList is better.** This means adding/remoing to and from the back of ArrayList<br> 

Loop through a Stack <br>
```
while (!stack.isEmpty) {
    // do something
    s.pop();
}
```

For Queues if front is 0 and back is size, and there is LinkedList with a front and back instance variables of ListNodes, then both adding and removing from the Queue would be O(1). <br>
This is not the case for a Queue implementation with LinkedList when front is size and back is 0. <br>

Can do this with Stacks as well. If you want to go through elements in Queue and inspect elements once and then you must remove, then you must have:<br>
``` java
int size = queue.size();
for (int i = 0; i < size; i++) {
    int removed = queue.remove();
    // do something with removed
}

```