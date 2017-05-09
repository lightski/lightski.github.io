---
layout: post
title: At Long Last
---

Hacking post day eeelevenish, and it's *finally* time! We start the code exploitation chapter and begin hacking. 

Recall that exploitation is making programs do unintended things. Security flaws, often, are extra pieces of functionality used in ways the original programmer did not expect. Small logic errors or seemingly unused code can lead to larger consequences.

One typical flaw is the *off by one* error. This happens when programmer miscounts the number of elements in a loop or conditional check. For example, suppose you want to build a one-hundred meter long fence with posts every 10 meters. How many posts do you need? Intuitively, the answer is ten. But that is incorrect; you actually require eleven. These sorts of errors occur regularly while coding.

Another common problem is quickly expanding complexity. Programmers sometimes get in a hurry and are unable to fully test functionality. The book gives the example of Microsoft's IIS handling Unicode characters. IIS is designed to serve both read-only and read-write content. Read-write directories give the user of a website full control of the system, so it's important to limit that access to certain subdirectories. Unfortunately, IIS later added Unicode support. Unicode expansion happened after the backslash check, so attackers could pass in Unicode characters to escape to different directories. Several worms used this vulnerability to deface websites.

Next we come to the classic security fault: buffer overflows. Suppose a C programmer allocates 8 bytes of memory, and tries to write 9 bytes to that space. This action is not stopped by the operating system (until more recent security measures), and it often causes the program to crash. But if we're careful, we can execute arbitrary code this way. Here's some sample code with a buffer overflow in it.

**overflow_example.c**

```c
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[]) {
   int value = 5;
   char buffer_one[8], buffer_two[8];

   strcpy(buffer_one, "one");
   strcpy(buffer_two, "two");

   printf("[BEFORE] buffer_one is at %p and contains \'%s\'\n", buffer_one, buffer_one);
   printf("[BEFORE] buffer_two is at %p and contains \'%s\'\n", buffer_two, buffer_two);
   printf("[BEFORE] value is at %p and is %d (0x%08x)\n", &value, value, value);

   printf("\n[STRCPY] copying %d bytes into buffer_two\n\n", strlen(argv[1]));
   strcpy(buffer_two, argv[1]);

   printf("[AFTER] buffer_one is at %p and contains \'%s\'\n", buffer_one, buffer_one);
   printf("[AFTER] buffer_two is at %p and contains \'%s\'\n", buffer_two, buffer_two);
   printf("[BEFORE] value is at %p and is %d (0x%08x)\n", &value, value, value);
}
```
And here it is in action:
```shell
vagrant@vagrant-laptop:~/src $ gcc overflow_example.c 
vagrant@vagrant-laptop:~/src $ ./a.out 12345                                     
[BEFORE] buffer_one is at 0xbffffc78 and contains 'one'
[BEFORE] buffer_two is at 0xbffffc70 and contains 'two'
[BEFORE] value is at 0xbffffc84 and is 5 (0x00000005)

[STRCPY] copying 5 bytes into buffer_two

[AFTER] buffer_one is at 0xbffffc78 and contains 'one'
[AFTER] buffer_two is at 0xbffffc70 and contains '12345'
[AFTER] value is at 0xbffffc84 and is 5 (0x00000005)
vagrant@vagrant-laptop:~/src $ ./a.out 12345678901234567890                                 
[BEFORE] buffer_one is at 0xbffffc68 and contains 'one'
[BEFORE] buffer_two is at 0xbffffc60 and contains 'two'
[BEFORE] value is at 0xbffffc74 and is 5 (0x00000005)

[STRCPY] copying 20 bytes into buffer_two

[AFTER] buffer_one is at 0xbffffc68 and contains '901234567890'
[AFTER] buffer_two is at 0xbffffc60 and contains '12345678901234567890'
[AFTER] value is at 0xbffffc74 and is 0 (0x00000000)
vagrant@vagrant-laptop:~/src $
```

The buffers are 8 bytes long, so we can safely store anything up to 8 characters in them. When we pass in a longer input, the extra bytes overwrite other variables. How, exactly is this exploitable? Tune in tomorrow to find out.

More to come.

