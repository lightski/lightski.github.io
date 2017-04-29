---
layout: post
title: Five Five Five
---

Hacking book day 3 whoop whoop! 30 minutes to write and publish here we go. More basic programming concepts than you can shake a stick at.

First up, it's "Signed, Unsigned, Long, and Short". These have to do with variable sizing. Signed vars can be + or -; they have a **sign**. Unsigned, are only positive. All values are stored as binary, so what's the difference? Signed values require one bit to indicate positive or negative, so they store a smaller range than unsigned. Note that signed negative values are stored as two's complement. Storing in two's complement gives us a nice property: negative binary plus it's oppostive ends up being zero. So we can do subtraction with a simple adder circuit. And finally, long and short just vary the amount of memory, so they store larger or smaller values. The exact amount is architecture-dependent. 

Next we turn our attention to pointers. Recall that

>The EIP register is a pointer that "points" to the current insruction during a program's execution by containing its memory address (p43).

This idea, that one area of memory points to another, is used in C as well. Moving physical memory takes time, storage space, and computation, so it's much easier to simply pass around a pointer to memory. In C, pointers are defined using asterisk (\*). The pointer type determines what type of data is pointed to. For example,
```c
int *pointer; // points to an int
char *pointer2; // points to char
int a = 12;
pointer = a;
```
It's very important to remember that these pointers hold the address (memory location), not a value. To retrieve memory contents of a variable, we dereference it using the asterisk (\*) operator. In the example above, pointer is set to the memory location of variable a. To retrieve the value of a (12), we write \*pointer. If we want the memory location of any variable, we simply prepend the ampersand (&) operator. Note that both the asterisk and ampersand notations exist in gdb as well as C.

Tonight's session was a brief overview of data scoping as well as pointers. Can't wait to see where we go next.

More to come.
