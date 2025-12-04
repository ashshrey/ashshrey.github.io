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
        if ((element == null && current.data == null) || (current.data != null && current.data.equals(element))) {
            return i;
        }
        current = current.next;
    }
    return -1;
}

```

**Implementing moveElementToBack()**
``` java
public void moveElementToBack(int index) {
    int move;
    if (index == 0) {
        move = front.data;
        front = front.next;
    }
    else {
        ListNode current = front;
        for (int i = 0; i < index - 1; i++) {
            current = current.next;
        }
        move = current.next.data;
        current.next = current.next.next;
    }
    back.next = new ListNode(move);
    back = back.next;
}

```

If it is a singly linked list, you must do this for adding and removing: `for (int i = 0; i < index - 1; i++) {`
REMEMBER: EMPTY list, add/remove FRONT, add/remove BACK, ONE element in list.
``` java
size == 0
size == 1
index == 0
index == size - 1 //REMOVE
index == size //ADD
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
        if (size == 1) { //only element
            removed = front.data;
            front = null;
            back = front;
        }
        else if (index == 0) { //remove from front
            removed = front.data;
            front = front.next;
            front.prev = null;
        }
        else if (index == size - 1) { //remove from back
            removed = back.data;
            back = back.prev;
            back.next = null;
        }
        else { //remove from middle
            ListNode current = front;
            for (int i = 0; i < index - 1; i++) {
                current = current.next;
            }
            removed = current.next.data;
            current.next = current.next.next;
            current.next.prev = current; 
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


**Implementing LinkedListIterator**

``` java

// Has SENTINEL NODES (both a front and a back sentinel)
public LinkedList() {
    front = new ListNode(null);
    back = new ListNode(null);
    front.next = back;
    back.prev = front;
    size = 0;
}

private class LinkedListIterator implements ListIterator<E> {

    private ListNode previous;
    private ListNode next;
    private int previousIndex;
    private int nextIndex;
    private ListNode lastRetrieved;

    public LinkedListIterator(int index) {
        if (index < 0 || index > size) {
            throw new IndexOutOfBoundsException();
        }
        previous = front; // equals sentinel node
        next = front.next;
        for (int i = 0; i < index; i++) {
            previous = next;
            next = next.next;
        }
        previousIndex = index - 1;
        nextIndex = index;
        lastRetrieved = null;
    }
    public boolean hasNext() {
		return next != back;
	}
    public boolean hasPrevious() {
        return previous != front;
    }
    public E next() {
        if (!hasNext()) {
            throw new NoSuchElementException();
        }
        lastRetrieved = next;
        next = lastRetrieved.next;
        previous = lastRetrieved;
        nextIndex++;
        previousIndex++; 
        return lastRetrieved.data;
    }
    public E previous() {
        if (!hasPrevious()) {
            throw new NoSuchElementException();
        }
        lastRetrieved = previous;
        next = lastRetrieved;
        previous = lastRetrieved.prev;
        nextIndex--;
        previousIndex--; 
        return lastRetrieved.data;
    }
    public void set(E e) {
        if (lastRetrieved == null) {
            throw new IllegalStateException();
        }
        if (e == null) {
            throw new NullPointerException();
        }
        lastRetrieved.data = e;
    }

    public void remove() {
        if (lastRetrieved == null) {
            throw new IllegalStateException();
        }
        lastRetrieved.prev.next = lastRetrieved.next;
        lastRetrieved.next.prev = lastRetrieved.prev;
        if (lastRetrieved == previous) { // next() was called
            previous = lastRetrieved.prev;
            previousIndex--;
            nextIndex--;
        }
        else { // previous() was called
            // removes node so should decrement indices but previous() already decrements indices
            next = lastRetrieved.next; 
        }
        size--;
        lastRetrieved = null;
    }
    public void add(E e) {
        if (e == null) {
            throw new NullPointerException();
        }
        ListNode node = new ListNode(e);
        node.prev = previous;
        node.next = next;
        previous.next = node;
        next.prev = node;
        previous = node; // next would not change
        previousIndex++;
        nextIndex++;
        size++;
        lastRetrieved = null;
    }
}

```

