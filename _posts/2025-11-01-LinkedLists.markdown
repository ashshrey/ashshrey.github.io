---
layout: post
title:  "Understanding LinkedLists"
date:   2025-11-01 18:46:52 -0400
categories: blog
---
**Note: These notes are based on course material and lectures provided by North Carolina State University.**
<br><br>
For traversing through list of ListNodes, do not try to access or use the reference that represents the list itself.<br>
DON'T do this:
~~`while (front != null)`~~ <br>

Instead do this:<br>
``` java
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
``` java
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
``` java
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

**Implementing indexOf(E element) for LinkedList**
``` java
private int indexOf(E element) {
    ListNode current = front;
    for (int i = 0; i < size; i++) {
        if (current.data != null && current.data.equals(element)) {
            return i;
        }
        current = current.next;
    }
    return -1;
}


```
**LinkedList Implementation**
``` java
public class LinkedList<E> {
    private ListNode front;
    private ListNode back;
    private int size;

    public LinkedList() {
        front = null;
        back = null;
        size = 0;
    }

    public void add(int index, E element) {
        ListNode node = new ListNode(element);
        if (size == 0) { //add to empty list
            front = node;
            back = front;
        }
        else if (index == 0) { //add to front
            node.next = front;
            front.prev = node;
            front = node;
        }
        else if (index == size) { //add to back
            back.next = node;
            node.prev = back;
            back = node;
        }
        else { //add to middle
            ListNode current = front;
            for (int i = 0; i < index - 1; i++) {
                current = current.next;
            }
            node.next = current.next;
            current.next.prev = node;
            current.next = node;
            node.prev = current;
        }
        size++;
    }

    public E remove(int index) {
        E removed = null;
        if (index == 0) { //remove from front
            removed = front.data;
            front = front.next;
            if (front != null) {
                front.prev = null;
            }
            else {
                back = null;
            }
        }
        else { //remove from middle or back
            ListNode current = front;
            for (int i = 0; i < index - 1; i++) {
                current = current.next;
            }
            removed = current.next.data;
            current.next = current.next.next;
            if (current.next != null) { 
                current.next.prev = current; 
            } 
            else { 
                back = current;
            }
        }
        size--;
        return removed;
    }

    public E set(int index, E element) {
        ListNode current = front;
        for (int i = 0; i < index; i++) {
            current = current.next;
        }
        E oldElement = current.data;
        current.data = element;
        return oldElement;
    }

    public E get(int index) {
        ListNode current = front;
        for (int i = 0; i < index; i++) {
            current = current.next;
        }
        return current.data;
    }

    private class ListNode {
        private E data;
        private ListNode next;
        private ListNode prev;

        public ListNode(E data) {
            this(data, null, null);
        }
        public ListNode(E data, ListNode next, ListNode prev) {
            this.data = data;
            this.next = next;
            this.prev = prev;
        }
    }
}

```

