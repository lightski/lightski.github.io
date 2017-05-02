---
layout: post
title: Make my Day
---

Hacking book day six, what what? Let's do this. We're moving on from variable scoping, globals, and statics. Not like *way* beyond, just *into-the-next-city* beyond. 

Big topic today is memory segmentation. C divides program's memory into five segments: text, data, bss, heap, and stack (p69). Relevant chart:

| name | what it holds | permissions | growth |
|------|----------|------------|------|
| text (code) | assembled machine language instructions | read-only | fixed size |
| data | **initialized** global and static program vars | writeable | fixed size |
| bss | **uninitialized** global and static program vars | writeable | fixed size |
| heap | programmer-allocatable blocks of memory | writeable | grows **down** to *higher* memory addresses |
| stack | temp 'scractch pad' for local vars and context during func call | writeable | grows **up** to *lower* memory addresses |

Here we come to an interesting aside on program execution. Program does not expect to read straight through text/code segment; control structures alter the flow through. As a program executes, EIP is set to first instruction in text. The processor then loops as follows (p69):
1. Read instruction at $EIP
2. $EIP += byte-length (at $EIP)
3. Execute instruction from #1
4. Loop back to #1

Let's go into more depth on the stack segment. In general, stacks are FILO (First In Last Out) data structure. Think of it like putting beads on a string, with a knot at one end (p70). Cannot get the first bead without taking the rest off. This behavior is convenient when calling functions. The outermost, or first function, has it's context buried most deeply in the stack. As function calls return, their context is easily available. It also makes sense that this must be dynamically-sized, because function calls are dynamic. Our program may have zero or many function calls on the stack at any time. 

Function's context is held in data store called *stack frame*. EBP register, aka FP *frame pointer* or LBP *local base pointer*, references local function variables in current stack frame (p70). Each stack frame holds: function parameters, local variables, the saved frame pointer (SFP), and the return address. SFP restores EBP to its previous value, and return address stores EIP's next instruction after function call (p70). 

And that's all for today. We looked into memory segmentation, and defined the five segments. Tune in next time for more discussion on memory segmentation and using the heap.

More to come.

