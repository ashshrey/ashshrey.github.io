---
layout: post
title:  "Understanding ArrayLists"
date:   2025-11-01 18:46:52 -0400
categories: blog
---
**Note: These notes are based on course material and lectures provided by North Carolina State University.**
<br><br>
ArrayLists are collections. They are data structures that store elements and have methods for abstracting the behavior to clients who use ArrayList. There are methods such as add, remove, contains, size, get. <br>
ArrayLists extend AbstractList and implement List.<br>
Constructing ArrayList <br>`ArrayList<Integer> list = new ArrayList<Integer>();`<br>

How to implement your own custom ArrayList?<br>
Must use generic types! <br>
Could have a `ArrayList<Object>` but then must cast to get the type you want. <br> 
`ArrayList<E>` is better. E is the generic object name. The generic object can be named anything (as long as it compiles) <br>
<br>
CANNOT construct a Generic Type Object<br>
~~`E item = new E();`~~<br>
You MUST do this (Remember SuppressWarnings):<br>
``` java
@SuppressWarnings("unchecked")
public ArrayList() {
    list = (E[]) new Object[10];
    size = 0;
}
```
When you remove an element at an index, memory and garbage collection is important. <br>
Make sure to (after removing element and shifting left) dereference the index at which an object is no longer being used. <br>
`list[size - 1] = null` <br>

**Sorting in Lists and Comparable Interface**
For the object that is the type of element that the list contains, the class must implement the Comparable interface.<br>
`public class MyClass implements Comparable<MyClass>`<br>
The list must also have a header that guarantees that the element can use the compareTo() method.<br>
`public class MyList<E extends Comparable<E>> extends AbstractList<E>`<br>

Generic Wildcard: Represented as `?`<br>
Generic Type is specific (can only be 1 type). Generic Wildcard refers to any Object (can be multiple types).<br>
<br>

**ArrayList Implementation**
``` java
public class ArrayList<E> {
    private E[] list;
    private int size;

    @SuppressWarnings("unchecked")
    public ArrayList() {
        // new Object[INITIAL_SIZE]
        list = (E[]) new Object[10];
        size = 0;
    }
    public boolean add(E element) {
        add(size, element);
        return true;
    }
    public void add(int index, E element) {

        //IMPORTANT
        // REMEMBER to growArray()
        if (list.length == size) {
            growArray();
        }

        // you are DECREMENTING
        // i > index
        for (int i = size; i > index; i--) {
            list[i] = list[i - 1];
        }
        list[index] = element;
        // INCREMENT size
        size++;
    }

    private void growArray() {
        E[] array = (E[]) new Object[list.length * 2];
        for (int i = 0; i < size; i++) {
            array[i] = list[i];
        }
        list = array;
    }

    public E remove(int index) {
        // get REMOVED
        E removed = list[index];
        // START at INDEX
        for (int i = index; i < size - 1; i++) {
            list[i] = list[i + 1];
        }
        // DEREFRENCE last element
        list[size - 1] = null;
        // DECREMENT size
        size--;
        return removed; 
    }

    public E set(int index, E element) {
        E oldElement = list[index];
        list[index] = element;
        return oldElement;
    }

    public E get(int index) {
        return list[index];
    }

    public int size() {
        return size;
    }


} 

```

