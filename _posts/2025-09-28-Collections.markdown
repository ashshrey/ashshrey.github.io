---
layout: post
title:  "Understanding Collections"
date:   2025-09-28 18:46:52 -0400
categories: blog
---
<br><br>
if double then `assertEquals(expected, actual, 0.001);`
<br>`assertEquals(46.0, ex.calculateAverage(list), 0.001);`

`ArrayList<Integer> list = new ArrayList<Integer>();`
<br>`list.get(index)` MUST return an object. ArrayList is an object that can only contain objects. 

infinite loop
```
public void infiniteLoop(ArrayList<Integer> list) {
		for (int i = 0; i < list.size(); i++) {
			list.add(i, 0);
		}
	}
```
to prevent infinte loop
```
int size = values.size();
		for (int i = 0; i < size; i++) {
			values.add(0);
		}
```

for ArrayLists we have to convert the primitive type to its wrapper class
<br>`Integer.valueOf(some integer);`
```
		assertEquals(Integer.valueOf(100), list.get(0));
		assertEquals(Integer.valueOf(50), list.get(1));
```

list.add(1 paramater) means it adds an element
```
list.add(index, element);
list.add(element);
```