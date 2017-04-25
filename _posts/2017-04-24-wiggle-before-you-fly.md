---
layout: post
title: Wiggle Before You Fly
---

Today is day 0 in my read through of *Hacking: the Art of Exploitation* by Jon Erickson. As such, today's post will include background material as well as some of my initial thoughts.

I intend to use this blog primarily as a place to [publicly] stash my notes. So I will not be posting many step-by-step guides or anything, at least not to start. Most posts will be summaries of the book content, with a healthy sprinkling of my thoughts interspersed throughout.

1. The book comes with a live cd which you can use on your computer. Very awesome! For my purpose, a virtual machine works a little better. So I downloaded the iso [online](https://www.nostarch.com/hackingCD.htm) and created a virtual machine using [VirtualBox](https://www.virtualbox.org/wiki/VirtualBox).
2. Next I'll begin writing while reading through the book. Prepare yourself! Note that any page references eg (p4) refer to a page within *Hacking: the Art of Exploitation*. 
3. hacked solutions follow the rules of the system, but they use those rules in counter-intuitive ways (p2). In the context of security, this can be restated as "hackers will find better uses for your software unless you remove them first."
4. The Hacker Ethic: art of logic; let information flow (p2). Hackers want to be free to pursue knowledge for the sake of building elegant logic.
5. computer security: survival of the fittest/ adapt to survive / defense and attack co-evolve. Just as in nature, predators evolve better attacks and prey must adapt or die out.
6. Hackers appreciate elegance. There are near-infinite solutions to any given problem. Most of them are trivial and require lots of space and time. Businesses are interested in easy solutions to make money; these are not necessarily the most elegant in terms of logic. Hackers appreciate solutions for their clever approach.
7. A program is a set of instructions. For example, building a LEGO set is a very simple program. The set designer gets to write the program; consumers pay for the program; and finally someone gets to run the program and (hopefully) end up with a cool model. Computers do the same step-by-step thing. I once heard someone say that computers are stupid but very good at following specific instructions. You have to break down what you want, but once the computer understands, it will do anything.
8. However, computers only know binary. Translators take Machine Language to binary; Compilers take HLL to binary. Machine Language is specific to the computer hardware (processor) so is very time-consuming and error-prone to write. Higher-level languages, such as C and Java, are closer to human English and much easier for humans to write. Compilers take source code of these languages and transform the instructions into binary which a computer can run.
9. And now for introductory programming concepts in Pseudocode. I will go over the next several sections pretty quickly as it is review for me. Each of these topics could easily be their own post.
9. If-then-else: the conditionals. Just as in mathemtical reasoning, `if (condition) then do thing1 else thing2`. If the condition is true we do thing1, otherwise we do thing2.
10. Some languages require the word `then` to follow `if (condition)`; other languages do not. The nice thing is these are surface-level differences. The concepts and structure underneath are what matter.
10. While/until loops: do something multiple times. 
11. For loops: when you know how many times to do something; aka 'while with a counter' (p10).
12. Variable: changeable data buckets. Minor aside on data types and precision- int vs float. Ints hold integer values (whole numbers) while floats hold precision after decimal point. This can lead to data loss, in the case of saving a number after dividing. Eg int a = 12/5 leaves a == 2 rather than 2.5 the correct answer. Would need a to be a float to save that .5.
13. Arithmetic operators: multiplication, division, addition, subtraction, and modulus. Just like in school. Oh, except modulus uses the % symbol and returns the remainder of a division. For example, 22 / 5 is 4 with 2 left over. 22 % 4 = 2. Also, the difference between pre-increment and post-increment
```c
    int a, b;
    a = 5;
    b = ++a * 7;
```
Produces `a == 6 and b == 42`, whereas:
```c
    int a, b;
    a = 5;
    b = a++ * 7;
```
Produces `a == 6 and b == 35`. As you can see, pre/post increment (and the same operators in subtraction) are difficult to reason about. I reccommend only using these alone; never use pre/post operators in a larger mathematical stream. You'll confuse anyone reading the code (such as your future self).
13. More boolean operators: comparison and logical (AND, OR). Symbols are similar to the same operators in mathematics.

    | symbol | english phrase |
    |--------|---------|
    | x < y | x is less than y |
    | x <= y | x is less than or equal to y |
    | x > y | x is greater than y |
    | x >= y | x is greater than or equal to y |
    | x == y | x equal to y |
    | x != y | x is NOT equal to y |
    | !x | NOT x |
    | x == y \|\| y == z | x is equal to y OR y is equal to z |
    | x == y && y == z | x is equal to y AND y is equal to z |
14. Functions: group of instructions you can call by name. Good for managing complexity which is the program's ultimate purpose. Can return a variable value. Declaration is similar to variable but still slightly different. Section included this lovely little factorial function (p17):
```c
int factorial(int x){
    int i;
    for(i=1; i<x; i++)
        x *= i;
    return x;
}
```
14. Function prototypes: the C compiler likes to know about functions before they're used. Implementation can come at end of program. Compiler just needs the function's: name, return type, and argument data types. 
15. First program! Writes "Hello, world!" x10 to the console. The start of something...magical. I wrote this out quickly using the included LiveCD inside a VirtualBox VM. 

Summary: hacking is the appreciation of elegant logical solutions. Hackers are curious about the deep workings of systems, especially information systems. Computer programming is foundational to hacking. Programming involves breaking tasks down step-by-step such that a computer can perform each step. Programming uses several concepts from mathematics and logic to create systems. Computers aren't smart but they sure work hard!

And, phew, there we go. One day of reading/blogging finished. The blogging end took longer than I anticipated so maybe I'll change the format in the future? We'll see. 

More to come.

