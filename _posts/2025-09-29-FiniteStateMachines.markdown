---
layout: post
title:  "Understanding Finite State Machines"
date:   2025-09-29 18:46:52 -0400
categories: blog
---
`final int START = 0;` 
`int state = START;`
`int i = 0;`

``` java
// while-switch logic
// can have ERROR state and (state != ERROR) for while loop
while (i < string.length()) {
    // can also do i++ here but don't if checking i in states
    c = string.charAt(i);
    // switching states
    switch (state) {
        case START:
        // if-else statements
        break;
        case STATE_1:
        // if-else statements
        break;
        default:
        System.out.println("Invalid state: " + state);
    }
    i++;
}
```
how to convert to int from char
`char c = '10';`
`x = c - '0';`
`x = 10;`

Horner's Rule
For integer `x = 10.0 * x + (c - '0');`
For after decimal values 

``` java
double power = 0.1;
x += power * (ch - '0');
power /= 10.0;
```

**[State Pattern] (https://en.wikipedia.org/wiki/State_pattern#/media/File:State_Design_Pattern_UML_Class_Diagram.svg)** 
**for FSMs**
``` java
// instance fields. NOT constants
private final State start = new Start();
private final State state1 = new State1();
private final State state2 = new State2();

//starts at initial state
private State state = start; 

// variables that we use in logic
private int variable1 = 1;
private int variable2 = 2;

private char c;

// implmenting like the while-switch logic
// BUT there is no switch statement
// switch statment is replaced by classes of the states
// methods of the states are the transitions
public int methodFSM(String s) {
    // reset variables 
    state = start;
    variable1 = 1;
    variable2 = 2;
    int i = 0;
    // while loop and if statements
    // state.method are transitions and logic
    while (i < s.length()) {
        c = s.charAt(i++);
        // examples of transitions
        if (Character.isWhitespace(c)) {
            state.onWhitespace();
        }
        else if (Character.isDigit) {
            state.onDigit();
        }
        else {
            state.onOther();
        }
    }
    return variable1 * variable2;
}

// Abstract class for State -- State can also be an Interface
// The super class must implement the transitions
// @Override for overriding methods
private abstract class State {
    public void onWhitespace() {
        // do something
        state = start;
    }
    public abstract void onDigit();
    public void onOther() {
        throw new IllegalArgumentException();
    }
}
// sub class of State
private class Start extends State {
    @Override
    public void onDigit() {
        // do something
        state = state1;
    }
}
// sub class of State
private class State1 extends State {
    @Override
    public void onDigit() {
        // do something
        state = state2;
    }
}
// sub class of State
private class State2 extends State {
    @Override
    public void onDigit() {
        // do something
    }
}
```

State Pattern for FSM using Interfaces is a little different.
However, you can also do State Pattern using Interfaces like the State Pattern for abstract class but change the abstract class to an Interface
and have the sub classes override all the methods in the interface.
``` java
private final State start = new Start();
private final State state1 = new State1();
private final State state2 = new State2();

private State state = start;
private int variable1 = 1;
private int variable2 = 2;

private char c; 

public int methodFSM(String s) {
    int i = 0;
    // reset variables
    state = start;
    variable1 = 1;
    variable2 = 2;
    while (i < s.length()) {
        // Don't forget i++
        c = s.charAt(i++);
        state.handleInput(c);
    }
    return variable1 * variable2;
}

// State is an Interface
private interface State {
    void handleInput(char c);
}
// sub class implementing State
private class Start implements State {
    @Override
    public void handleInput(char c) {
        if (Character.isWhitespace(c)) {
            // do something
            state = start;
        }
        else if (Character.isDigit(c)) {
            // do something
            state = state1
        }
        else {
            throw new IllegalArgumentException();
        }
    }
}
// sub class implementing State
private class State1 implements State {
    @Override
    public void handleInput(char c) {
        if (Character.isWhitespace(c)) {
            // do something
            state = start;
        }
        else if (Character.isDigit(c)) {
            // do something
            state = state2
        }
        else {
            throw new IllegalArgumentException();
        }
    }
}
// sub class implementing State
private class State2 implements State {
    @Override
    public void handleInput(char c) {
        if (Character.isWhitespace(c)) {
            // do something
            state = start;
        }
        else if (Character.isDigit(c)) {
            // do something
        }
        else {
            throw new IllegalArgumentException();
        }
    }
}

```
