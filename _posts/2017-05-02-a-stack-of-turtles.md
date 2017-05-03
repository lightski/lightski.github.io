---
layout: post
title: A Stack of Turtles
---

Hacking book day seven. And how. Today we continue the looking at memory segments. This is a continuation of [yesterday's topic]({{ site.baseurl }} {% post_url 2017-05-01-make-my-day %}).

Recall C uses five different segments in memory: code, data, bss, heap, and stack. Where a variable is stored depends on how it is defined. Initialized static and global variables go to data; uninitialized variables remain in the bss. Heap memory is controlled by programmer; we allocate more space using **malloc()**. Remaining function variables are stored in stack, where all local context values reside (p75). 

Let's dive further into the heap, shall we? Using the other four variable segments just depends on how you initialize variables; using heap requires explicit effort (p77). Use **malloc()** to initialize memory. It returns a pointer to the memory or null if unable. When finished, release memory using **free()**. Note that **malloc()** doesn't know what type of memory it is allocating. Thus **malloc()** returns a void pointer to the memory, and we the programmer must cast the pointer to the correct type. 

This concludes the essentials of C programming. Next we move on to more advanced C topics using functions.

Our first *advanced C topic* is file access. C language supports low-level file management, using file descriptors, as well as high-level file buffered I/O using file streams. We're going to look at file descriptors; they are more direct (p81). A *file descriptor* is a unique number used to reference open files. It's like a social security card for open C files. There are four primary functions that operate on file descriptors, and they are as follows:

| function | args | description | return values |
|-----|----|----|------|
| open() | pointer to file, access mode flags |opens file for reading/writing | int file descriptor; -1 on error |
| close() | file descriptor | closes file | -1 on error |
| read() | file descriptor, pointer to data, #bytes to read | reads #bytes from file to pointer | -1 on error |
| write() | file descriptor, pointer to data, #bytes to write | writes #bytes from pointer to file | -1 on error |

The *access mode flags* sent to **open()** require more time than I've got tonight. So our discussion of file access is placed on hold. Today we concluded our discussion of memory segments, and began looking into file access. Next time we'll finish up file access and try to move through file permissions and user ids. In the next week, I hope to cover actual code exploitation. Can't wait!

More to come.

