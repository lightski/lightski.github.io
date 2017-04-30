---
layout: post
title: It Could Always Be Worse
---

Hacking book day four (or so...just realized my numbering is incredibly inconsistent). Today there'll be more introductory programming concepts paired with low-level architecture discussion. Let's get started.

[Last discussion]({{ site.baseurl }}{% post_url 2017-04-28-five-five-five %}) ended with pointers plus the unary operators address-of (&) and dereference (\*). Here's a good mnemonic for remembering their usage:

>When the unary operators are used with pointers, the address-of operator can be thought of as moving *backward*, while the dereference operator moves *forward* in the direction the pointer is pointing (p47; emphasis added).

Next up in our C discussion: format strings. The printf() function can be used to format data for output. By adding parameters, called *format parameters*, printf() knows to replace some part of the string with a value. Format parameters in printf() look like: %d. For each format parameter we use, we must pass an extra argument for printf() to insert into the string. For example, to print a decimal we might write: 
```c
printf("Value of myvar is: %d", myvar);
```
Here, %d is the format parameter; myvar is a variable we wish to print formatted as a decimal. Remember- myvar is just some bits in memory. C will print it out as whatever we choose, regardless of the data type we stored it as. The 1s and 0s are inherently meaningless; they get their meaning from the way they are interpreted (sort of like life).

In format parameters, there is an optional numeric argument. You can specify minimum width, eg %10d. C will pad with empty space, unless your minmum space starts with a 0 eg %09d. Here is a chart of the different parameter options; the data column is the type of format of the parameter printf() expects.

| Parameter | Output Type | Data |
|-----------|-------------| 
| %d | Signed Decimal | Value | 
| %u | Unsigned Decimal | Value |
| %x | Hexadecimal | Value |
| %s | String (prints chars until null byte) | Char Pointer |
| %n | Number of bytes written so far | Pointer |
| %p | Memory address (equiv to 0x%08x) | Pointer |

These parameters are also used for reading input. Use scanf() to get values from user input. Here's a sample showing usage of scanf()
```c
int myint;
printf("Enter an integer: ");
scanf("%d", &myint);
```
Running this prompts the user, and then saves whatever you enter into *myint*.

Writing data into, and out of, a program is foundational. I strongly agree that "Having some form of immediate feedback is fairly vital to the hacker's learning process" (p51). Even just printing the values of a variable can be enormously helpful. The sooner you get feedback from a system, the sooner you can validate assumptions.

Next big concept is type-casting. This lets us (the C compiler) interpret values as a certain data type. Typecasting syntax is: (data type) variable, eg "(int) myvar". Having explicit types is mainly to prevent programming errors; it's all just bits at the end of the day. 

We use type-casting  to save precision with division as well as using pointers for values. It also comes up when dealing with pointer types. Character data type takes up four bytes, so adding one to a character pointer increments the memory four bytes. This gives unexpected behavior when using pointers of one type to refer to memory locations of another type. So, generally we just don't do that, but if we must we can cast the pointer to fix the size. 

Using pointers of the correct type is the best practice. However, at times a void pointer is desirable. Void pointers have type void; they must be typecast when dereferencing or performing pointer arithmetic. In short, void pointers just hold a memory address. We have to tell the compiler what type of address as we use it.

This concludes today's basic programming discussion. We covered C format strings and type-casting. The big idea was that memory is only bits; it's up to the compiler to interpret correctly. The programmer guides the compiler to interpretations via data typing.

Looking forward, tomorrow's discussion will include more programming bits like command-line arguments and variable scoping. We are halfway through the book's programming discussion. So far I am enjoying the review; the book gives great examples. The book also does a good job showing the larger context through examining program memory. Still, I'm looking forward to finishing the basics and moving on to exploiting some code.

More to come.

