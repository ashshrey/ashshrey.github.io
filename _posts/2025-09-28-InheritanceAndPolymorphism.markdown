---
layout: post
title:  "Understanding Inheritance and Polymorphism"
date:   2025-09-28 18:46:52 -0400
categories: blog
---
**Note: These notes are based on course material and lectures provides by North Carolina State University.**
<br><br>
Abstract class<br>
`public abstract class AbstractClass { }`<br>
Abstract class can have abstract methods for sub classes to implement. Abstract class doesn't implement an abstract method.<br>
Abstract methods CANNOT be static. Static belongs to the class itself. 
`public abstract void methodName(int x);`<br>
`public abstract List<Integer> getList();`<br>
When sub class implements getList(), the return type `List<Integer>` can be `ArrayList<Integer>` because List is an Interface.
<br><br>
Sub class - Abstract classes can also be a sub class and extend a super class.
`public class SubClass extends SuperClass { }`<br>
`public abstract class SubClass extends SuperClass { }`
<br><br>
Implementing interface<br>
`public class ClassName implements InterfaceName { }`
<br> Interface methods are automatically `public abstract`
<br> For example `void print();` is treated as `public abstract void print();`<br>
**Interfaces can only have constants and not implemented methods.** <br>
**Note:** Since Java 8, Interfaces can implement methods using the `default` keyword. These methods are inherited by sub classes and can be overrided.
Interfaces can also have `static` methods.
<br>
<br>
Sub class constructor MUST call super constructor
```
public SubClass() {
    super();
    this.var = 0;
}
```

`@Override` for methods of the SuperClass you want to overrride
<br>
Interfaces ONLY have constants and methods without implementations.<br>
Methods are already public and static.<br>
`public interface Interface { }`

equals() method<br>
`(object instanceof Object) { }` Don't use because polymorphically the sub classes of Object (if Object is a super class) will be instances of Object
<br>Object is SuperClass. object is SubClass.

`SuperClass object = new SubClass();`

CANNOT do this the other way around whether the class is concrete or abstract.<br>
~~`SubClass object = new SuperClass();`~~

CANNOT instantiate SuperClass or Interface<br>
Can't do this `= new SuperClass();`<br>
Or this `= new Interface();`<br>
<br>
So how to do equals() method given an inheritance heirarchy?<br>
Don't compare `static` variables because they belong to the class NOT the instance.<br>

MUST always first extend the superclass and then the interface if extending a super class (which can be an Abstract class) and implementing an Interface <br>
CANNOT extend more than one super class in Java <br>

MUST do this <br>
`public class SubClass extends SuperClass implements Interface`

This is SubClass.equals() { }
```
public boolean equals(Object o) {
    if (this == o) {
		return true; 
    }
    // replace with (o == null) if this is SuperClass or not a SubClass (will be sub class of Object)
	if (!super.equals(o)) {
		return false;
    }
	if (getClass() != o.getClass()) {
        return false;
    }
    SubClass other = (SubClass) o;

    // some instance varible called var
    // if-else is checking if either variable is null or doesn't equal to each other
    if (this.var == null) {
        if (other.var != null) {
            return false;
        }
    } 
    else if (!this.var.equals(other.var)) {
        return false;
    }

    return true;
}
```

Explaining hashCode() method?