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
    if (x < 2) { // 0 or 1
        return "" + x;
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
            return next.add(e);
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

**Recursion in LinkedList**
``` java 
public class LinkedList<E> {
    private ListNode front;
    private int size;
    private class ListNode {
        private E data;
        private ListNode next;
        public ListNode(E data, ListNode next) {
            this.data = data;
            this.next = next;
        }
        public ListNode(E data) {
            this(data, null);
        }

        private boolean contains(E element) {
            if (data.equals(element)) {
                return true;
            }
            else if (next == null) {
                return false;
            }
            else {
                return next.contains(element);
            }
        }
        private boolean add(E element) {
            if (next == null) {
                next = new ListNode(element);
                size++;
                return true;
            }
            else {
                return next.add(element);
            }
        }
        private void add(int index, E element) {
            if (index == 0) {
                next = new ListNode(element, next);
            }
            else {
                next.add(index - 1, element);
            }
        }
        private E get(int index) {
            if (index == 0) {
                return next.data;
            }
            else {
                return next.get(index - 1);
            }
        }
        private boolean remove(E element) {
            if (next == null) {
                return false;
            }
            else if (next.data.equals(element)) {
                next = next.next;
                size--;
                return true;
            }
            else {
                return next.remove(element);
            }
        }
        private E remove(int index) {
            E removed;
            if (index == 0) {
                removed = next.data;
                next = next.next;
            }
            else {
                removed = next.remove(index - 1);
            }
            return removed;
        }
        private E set(int index, E element) {
            E oldElement;
            if (index == 0) {
                oldElement = next.data;
                next.data = element;
            }
            else {
                oldElement = next.set(index - 1, element);
            }
            return oldElement;
        }
    }

    public boolean contains(E element) {
        if (front == null) {
            return false;
        }
        else if (front.data.equals(element)) {
            return true;
        }
        else {
            return front.contains(element);
        }
    }
    public boolean add(E element) {
        if (front == null) {
            front = new ListNode(element);
            size++;
            return true;
        }
        else {
            return front.add(element);
        }
    }
    public void add(int index, E element) {
        if (index == 0) {
            front = new ListNode(element, front);
        }
        else {
            front.add(index - 1, element);
        }
        size++;
    }
    public E get(int index) {
        if (index == 0) {
            return front.data;
        }
        else {
            return front.get(index - 1);
        }
    }
    public boolean remove(E element) {
        if (front == null) {
            return false;
        }
        else if (front.data.equals(element)) {
            front = front.next;
            size--;
            return true;
        }
        else {
            return front.remove(element);
        }
    } 
    public E remove(int index) {
        E removed;
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
    public E set(int index, E element) {
        E oldElement;
        if (index == 0) {
            oldElement = front.data;
            front.data = element;
        }
        else {
            oldElement = front.set(index - 1, element);
        }
        return oldElement;
    }
}

```