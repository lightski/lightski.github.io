---
layout: post
title: What the Struct
---

Hacking post day ten. I skipped out on writing yesterday because it was too late at night. This week I am focusing on writing, and sleeping, earlier. But, enough about me! Let's dive into some more C material. Today is mostly about structs.

Yo dog, we heard you like variables. So we made a variable you can put more variables into. In C we call it a **struct**. **structs** are continuous areas of memory. You declare them like this:

```c
struct brewery {
    int bottles_of_beer;
    double cash_on_hand;   
};
```
We get a **struct** called brewery, which tracks bottles of beer and cash. Next, we must access these values somehow.

```c
// declare struct and vars
struct brewery mybrew, *brewptr;
brewptr = &mybrew;
// three ways to access:
bottles = mybrew.bottles_of_beer; // direct access
cash = brewptr->cash_on_hand; // pointer access
num_bottles = *((int *) brewptr); // hacky pointer cast
```
To access values the first way, we must have the struct in memory. This works sometimes, but can be a hassle. Passing **structs** around takes a lot of space on the stack. To migigate this, we use the second access method. Having a pointer to the struct is just as good. Note the arrow (->) notation is for convenience; it's the same as dereferencing the struct pointer. The first two access methods are proper ways to use structs in C. The third way technically works, but it's discouraged. How it works, is we cast the pointer as an int pointer and then directly access the memory location. It's messy because you have to track exactly how the memory is laid out in the struct.

Next, a quick note on pointers. Pointers hold a memory location, and we typically use them to refer to variables. However, we can also get a pointer to a function's location, known as a **function pointer**. Here's some source from the book showing their use.

**funcptr\_example.c**

```c
#include <stdio.h>

int func_one() {
    printf("This is function one"\n");
    return 1;
}

int func_two() {
    printf("This is function two"\n");
    return 2;
}

int main() {
    int value;
    int (*function_ptr) (); // funciton pointer!

    function_ptr = func_one;
    printf("function_ptr = 0x%08x\n", function_ptr);
    value = function_ptr();
    printf("value returned was %d\n", value);

    function_ptr = func_two;
    printf("function_ptr = 0x%08x\n", function_ptr);
    value = function_ptr();
    printf("value returned was %d\n", value);
    return 0;
}
```

So the function pointer gets set to the locations of two different functions and called. This works as you'd expect; both functions get called properly and we see that they live at different memory addresses. I'm not sure what these are used for in C, but it's here just in case.

Finally, we look at pseudo-random numbers. Truly random numbers require non-determinism. Computers produce outputs based on inputs, ie they are deterministic, so they cannot provide true randomness. However, some programs require random numbers. AI in games and cryptography are two easy examples which come to mind. In C, we can use the **srand()** and **rand()** functions from \<stdlib.h\>. **srand()**  takes a seed value, then **rand()** produces pseudo-random numbers from that seed. It is common to use the seconds elapsed since the epoch (how Linux tracks time) as a seed. Pseudo-random numbers appear random, but if you know the seed you could calculate them. 

This is the end of the C tutorial, whoo!! From here, the book shows one large C program: game_of_chance.c. Maybe I'll post source later? (it's on github). Next up is the chapter on exploitation, aka making a program do unintended things. I am quite excited to start, as that will be totally new material. Cannot wait!

More to come.


