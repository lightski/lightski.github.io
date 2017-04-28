---
layout: post
title: Fourier the Win
---

Hacking book day 2 ready...aim...execute.

This is a continuation from [day 1]({{ site.baseurl }}{% post_url 2017-04-25-enter-the-third-age %}), so it'll make (slightly) more sense if you read that first. We continue reading the memory of the simple hello world program previously listed. 

2. Composition of the for loop is a cmp, jle, jmp, and inc. The two jmp instructions define the bounds of the loop. The first is 'within' the loop, and it checks the value of the counter variable. If counter is high, execution jumps outside of the loop section (thus ending the loop). The second instruction comes at the end of the loop; it serves to keep repeating the loop (accomplished by unconditional jmp rather than the conditional jle -- jump if less or equal jle).

3. More helpful gdb commands: c formats byte output as ascii characters, and s displays an entire string of character data. 

2. ...AND we're back, with more basic programming concepts. I will again go through these somewhat quickly. Interesting to note that "all C code must be compiled into machine instructions before it can do anything" (p38). Even though higher-level languages provide abstractions, they ultimately rest on very simple mechanisms.

3. String, in C, is array of characters. Arrays are, of course, a list of elements of a specific type (p38). Literally, several adjacent memory addresses. I predict this will be useful later. Also important to notice is the end character of a string is a 0 or null byte. Print functions look for null byte to stop printing.

3. Turns out, working with memory directly is kind of a pain. Who knew, right? So there are several C functions to read and write strings. strcpy(dest, "input string") copies the "input string" into variable dest. Use it like so (p39):

    ```c
    #include <stdio.h>
    #include <string.h>
    // stdio for printf; string for strcopy

    int main() {
        char a_string[30];
        strcpy(a_string, "Print me out please\n");
        printf(a_string);
        return 0;
    }
    ```
3.  A little more debugging turned up the **bt** command for gdb. Turns out, calls to external libraries are remembered by a data structure called the stack. gdb's bt command, short for back trace, lets us examine the stack during program execution.

That is all for today. We covered the structure of a **for** loop in assembly, some more gdb commands like s and bt, and working with Strings and arrays. Next post will be (hopefully) the end of introductory programming concepts. Hooah.

More to come.

