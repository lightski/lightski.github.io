---
layout: post
title: Hairs of my Head
---

Hacking book day five. Let's get right to it.

Previously, we talked about sending input to a C program using the scanf() function. This works, but there is a more efficient way-- command-line arguments. *Command-line arguments* is a fancy way of saying *provide input as we run the program*. C language provides command line arguments to the main function when we pass in two additional parameters: int arg_count, and char \*arg_list[]. The first, arg_count, holds number of arguments passed. The second is a pointer to an array of strings where each element is an argument. The zeroth argument is always the name of the executing binary (program).

It's important to note that, in C, programmer is responsible for keeping track of memory bounds. That is, if a program tries to access memory out of it's segments it crashes. C compiler does not automatically catch this for us. So, if you assume commmand-line arguments are there but they're not, your program will probably crash (seg fault).

Our next topic is variable scoping. In C, functions are their own context independent of anything else. So, variable declared within a function is "invisible" to main() context and other functions. This means we can have variables named the same thing, but pointing to different values, as long as they exist in different function contexts.

Variables can also have global scope if they're declared outside any function. In such case, the variable is the same throughout function contexts unless it is declared again. This can lead to confusion; best practice is to avoid using global variables.

Static scope is another way variables can be declared; to do so, we prepend the keyword **static**. Static variables remain intact across function calls; however, they remain local to a particular context. That is, if you call a function multiple times, the values of it's static variables remain the same.

Following example demonstrates the concepts of scope, globals, and static variables.

```c
#include <stdio.h>

int j = 42; // j is a global variable

int func4() {
    static int k = 0; // k is static variable
    return ++k; // every call it increments then returns
}

void func3() {
    int i = 1, j = 999; // i and j are local vars
    printf("\t\t\t[in func 3] i = %d, j = %d, k = %d\n", i, j, func4());
}

void func2() {
    int i = 7;
    printf("\t\t[in func2] i = %d, j = %d, k = %d\n", i, j, func4());
    printf("\t\t[in func2] setting j = 1337\n");
    j = 1337; // writing to global j
    func3();
    printf("\t\t[back in func2] i = %d, j = %d, k = %d\n", i, j, func4());
}

void func1() {
    int i = 5;
    printf("\t[in func1] i = %d, j = %d, k = %d\n", i, j, func4());
    func2();
    printf("\t[back in func1] i = %d, j = %d, k = %d\n", i, j, func4());
}

int main() {
    int i = 3; // main's local i
    printf("[in main] i = %d, j = %d, k = %d\n", i, j, func4());
    func1();
    printf("[back in main] i = %d, j = %d, k = %d\n", i, j, func4());
    return 0;
}
```

Compile and run

```shell
gcc scope.c
./a.out
```

And we get the following output.

```
[in main] i = 3, j = 42, k = 1
	[in func1] i = 5, j = 42, k = 2
		[in func2] i = 7, j = 42, k = 3
		[in func2] setting j = 1337
			[in func 3] i = 1, j = 999, k = 4
		[back in func2] i = 7, j = 1337, k = 5
	[back in func1] i = 5, j = 1337, k = 6
[back in main] i = 3, j = 1337, k = 7
```

As you can see, value of i remains local to contexts. k increments every time we call the function. And, j is global except when we declare it locally.

That's a wrap for today. We discussed command line args, variable scope, globals, and static vars. Next topics are memory segmentation, the stac, and the heap.

More to come.

