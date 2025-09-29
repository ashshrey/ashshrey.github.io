---
layout: post
title:  "Understanding Inheritance and Polymorphism"
date:   2025-09-28 18:46:52 -0400
categories: blog
---
Abstract class
`public abstract class AbstractClass { }`
Abstract class can have abstract methods for sub classes to implement. Abstract class doesn't implement an abstract method.
`public abstract void methodName(int x);`
`public abstract List<Integer> getList();`
When sub class implements getList(), the return type `List<Integer>` can be `ArrayList<Integer>` because List is an Interface.

Sub class. Abstract classes can also be a sub class and extend a super class.
`public class SubClass extends SuperClass { }`
`public abstract class SubClass extends SuperClass { }`

Implementing interface
`public class ClassName implements InterfaceName { }`

Sub class constructor MUST call super constructor
```
public SubClass() {
    super();
    this.var = 0;
}
```

`@Override` for methods of the SuperClass you want to overrride

Interfaces ONLY have constants and methods without implementations.
Methods are already public and static.
`public interface Interface { }`

equals() method
`(object instanceof Object) { }` Don't use because polymorphically the sub classes of Object (if Object is a super class) will be instances of Object
Object is SuperClass. object is SubClass.

`SuperClass object = new SubClass();`

CANNOT do this the other way around whether the class is concrete or abstract.
~~`SubClass object = new SuperClass();`~~

CANNOT instantiate SuperClass or Interface
Can't do this `= new SuperClass();`
Or this `= new Interface();`

So how to do equals() method given an inheritance heirarchy?
Don't compare `static` variables because they belong to the class NOT the instance.
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