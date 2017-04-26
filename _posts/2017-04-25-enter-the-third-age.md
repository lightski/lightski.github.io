---
layout: post
title: Enter the Third Age
---

Day 1 hacking book read through GO!

Today is all about reading memory and the low-level workings of our programs. Enjoy.

1. Hackers get their edge from knowing how all the pieces interact with the big picture. (p20), ie programs are much more than source code. 
2. Enter objdump, linux tool which allows us to print out what the compiled file is doing at the CPU level. Here we see memory address and instructions. objdump, as many Linux utilities, defaults to AT&T syntax (lots of % and $ signs). The intel syntax is a little nicer and it's just a -M intel away! Alternatively, set it in .gdbinit with 
```shell
echo "set dis intel" > ~/.gdbinit
```
 (p25).
3. CPU has several fast access 'local variables' called registers. The first four mainly act as temporary variables for CPU while executing machine instructions. The second four typically point to locations in memory rather than holding values themselves. CPU uses the ninth register, EIP, to point to current instruction it's reading. Very important for debugging (p24-5). Here they are in a glorious chart:

    | Name | Description |
    |------|-------------| 
    | EAX | accumulator register |
    | ECX | counter register | 
    | EDX | data register | 
    | EBX | base register | 
    | ESP | stack pointer |
    | EBP | base pointer | 
    | ESI | source index |
    | EDI | destination index |
    | EIP | instruction pointer |
4. Intel assembly follows convention of 
```
operation <destination>, <source>
```
If you always get that backwards (like me) here's a quick mnemonic- like email first say to:, then from:. 
4. Assembly operations are largely easy mnemonics as well. We have **mov** to move to destination from source, and **sub** and **inc** to subtract and increment (results stored in destination). **cmp** performs comparisons. Instructions starting with j perform some sort of jump to a new address. For example, **jle** jumps to destination if previous **cmp** resulted in less than or equal. (p25-6).
5. Since a running program is mostly just processor and segments of memory, examining memory is the first way to look at what's really going on (p27).
6. Gdb is the GNU debugger. Very helpful tool to step through running program and inspect memory in realtime. Here are some gdb commands :

    | Command | Description |
    |------|-------------|
    | list | list source if available (gcc -g) |
    | break main | set breakpoint at main instruction |
    | run | run program |
    | info register eip | print value of eip |
    | x | examine memory |
    | x/t $eip | display $eip in hexadecimal |
    | x/8xw $eip | examine next 8 words (4 bytes) hexidecimal |
    | x/i $eip | display $eip as assembly insruction |
7. In the course of examining memory, we find some bytes get reversed (depending on how you print them). This is due to litle-endian byte order: x86 stores least-significant bits last. Gdb will compensate for this, but it's important to know if you want to write memory.

The next several pages are an in-depth debugging session in which we examine memory in-depth. Very excited to continue and hope I can summarize this well.

In summary, today we went deep under the veil. We started discussing assmebly language, which describes how the CPU actually operates. We examined some basic assembly syntax and helpful gdb commands to expose the computers inner-workings. Looking forward to continuing this deep-dive into programming.

More to come.
