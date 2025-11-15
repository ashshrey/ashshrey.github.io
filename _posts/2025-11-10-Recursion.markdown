---
layout: post
title:  "Understanding Recursion"
date:   2025-11-10 18:46:52 -0400
categories: blog
---
**Note: These notes are based on course material and lectures provided by North Carolina State University.**
<br><br>

``` java
public int pow(int x, int y) {
    if (y == 0) {
        return 1;
    }
    else if (y % 2 == 0) {
        return pow(x * x, y / 2); 
    }
    else {
        return x * pow(x, y - 1);
    }
}

```

``` java
public String binary(int x) {
    String binary = "";
    if (n < 2) { // 0 or 1
        return "" + n;
    }
    else {
        return binary(x / 2) + binary(x % 2);
    }
}

```
`int x +=` `+=` means append while doing `int x = ... + x` means reverse.<br>

Contains method for LinkedList<br>
``` java
public boolean contains(int e) {
    return contains(front, e);
}

private boolean contains(ListNode current, int e) {
    if (current == null) {
        return false;
    }
    if (current.data == e) {
        return true;
    }
    return contains(current.next, e);
}
```

Adding to the end of the LinkedList<br>
``` java
public boolean add(int e) {
    if (front == null) {
        front = new ListNode(e);
        size++;
        return true;
    }
    return add(front, e);
}
private boolean add(ListNode current, int e) {
    if (current.next == null) {
        current.next = new ListNode(e);
        size++;
        return true;
    }
    else {
        return add(current.next, e);
    }
}

//Can do this as well
private class ListNode {
    public boolean add(int e) {
        if (next == null) {
            next = new ListNode(e);
            size++;
            return true;
        }
        else {
            next.add(e);
        }
    }

    public void add(int index, int e) {
        if (index < 0) { // NOT necessary
            throw new IndexOutOfBoundsException();
        }
        else if (index == 0) { 
            next = new ListNode(e, next);
        }
        else if (next == null) { // NOT necessary
            throw new IndexOutOfBoundsException();
        }
        else {
            next.add(index - 1, e);
        }
    }

    public int remove(int index) {
        int removed;
        if (index == 0) {
            removed = next.data;
            next = next.next;
        }
        else {
            removed = next.remove(index - 1);
        }
        return removed;
    }
}

public void add(int index, int e) {
    //Better way of throwing IndexOutOfBoundsException
    if (index < 0 || index > size) {
        throw new IndexOutOfBoundsException();
    }

    if (index == 0) {
        front = new ListNode(e, front);
    }
    else if (front == null) { // NOT necessary
        throw new IndexOutOfBoundsException();
    }
    else {
        //DECREMENT index 
        //add BEFORE the current element at the index
        front.add(index - 1, e);
    }
    size++;
}


public int remove(int index) {
    if (index < 0 || index > size - 1) {
        throw new IndexOutOfBoundsException();
    }
    int removed;
    if (index == 0) {
        removed = front.data;
        front = front.next;
    }
    else {
        removed = front.remove(index - 1);
    }
    size--;
    return removed;
}
```



