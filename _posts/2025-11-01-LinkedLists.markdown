---
layout: post
title:  "Understanding LinkedLists"
date:   2025-11-01 18:46:52 -0400
categories: blog
---
For traversing through list of ListNodes, do not try to access or use the reference that represents the list itself.<br>
DON'T do this:
~~`while (front != null)`~~ <br>

Instead do this:<br>
```
ListNode current = front;
while (current != null) {
    // do something
    current = current.next;
}
```
ListNodes are similar to Arrays but implemented differently. We can use ListNodes in LinkedLists. <br>

LinkedLists are composed of chained ListNodes. <br>
Inner classes like ListNode (ListNode is an inner class of LinkedList) can refer to the outer class as `LinkedList.this`<br>
If outer class declares a type parameter (like generic type E), the inner class doesn't need to redeclare it <br>
For example, <br>
```
public class LinkedList<E> {
    private class ListNode {

    }
}
```

Two types of assignment of reference for ListNodes:<br>
1.<br>
`ListNode current = front;` and `current = current.next` are just reasigning a variable. The list DOES NOT change. <br>
current creates a different reference pointing to the same object that front
<br>
2. <br>
`current.next = new ListNode(element, current.next);` and `current.next = current.next.next;`

**Implementing LinkedList.addSorted(element)**
```
public void addSorted(E element) {
    if (front == null || element.compareTo(front.data) < 0) {
        front = new ListNode(element, front);
    }
    else {
        ListNode current = front;
        while (current.next != null && current.next.data.compareTo(element) < 0) {
            current = current.next;
        }
        current.next = new ListNode(element, current.next);
    }
    size++;
}

```

**LinkedList Implementation**
```
public E remove(int idx) {
    E removed = null;
    if (idx == 0) { 
        removed = front.data;
        front = front.next;
    } 
    else {
        ListNode current = front;
        for (int i = 0; i < index - 1; i++) {
            current = current.next;
        }
        removed = current.next.data;
        current.next = current.next.next;
    }
    size--;
    return removed;
}



```

