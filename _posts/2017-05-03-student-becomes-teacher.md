---
layout: post
title: Student Becomes Teacher
---

Hacking book day eight, whoa dude. Today we're going all-in on *advanced* C topics. Enjoy. 

Recall that [yesterday's discussion]({{ site.baseurl }}{% post_url 2017-05-02-a-stack-of-turtles %}) included a section on file system. Today we continue that conversation by discussing *access mode flags*. Access mode flags describe how C will access a file. The flags are defined in the C language headers **fcntl.h** and **sys/stat.h**. Access mode must use at least one of these flags:
- *O_RDONLY*: read-only access
- *O_WRONLY*: write-only access
- *O_RDWR*: both read and write

Additionally, access mode may have optional flags. Here are some of the more useful ones (p84):
- *O_APPEND*: write data to file end
- *O_TRUNC*: if file exists, shorten it to length 0
- *O_CREAT*: if file does not exist, make it

To combine these flags, we use bitwise OR operator (the pipe "\|"). For example, write only with create option is: O\_WRONLY\|O\_CREAT. Internally, these flags are strings of bits in different positions. So bitwise ORing them adds the bits together and erases no information.

When creating a file with *O_CREAT*, additional flags are required to specify the file's permissions. They are defined in **sys/stat.h**, can be combined using bitwise OR, and are as follows (p87):
- *S_IRUSR*: File owner can read this file.
- *S_IWUSR*: File owner can write this file.
- *S_IXUSR*: File owner can execute this file.
- *S_IRGRP*: File group can read this file.
- *S_IWGRP*: File group can write this file.
- *S_IXGRP*: File group can execute this file.
- *S_IROTH*: Others can read this file.
- *S_IWOTH*: Others can write this file.
- *S_IXOTH*: Others can execute this file.

If you know Linux file permissions, these are exactly the same. If not, we're going to go over them right now. On Linux, whomever creates a file is the owner. The group that owner belongs to is assigned to the group of the file. And anyone is other users who are not a member of the group. Each of these have three permissions which may be set in any permutation: **r**ead, **w**rite, and **e**xecute. Here's a concrete example:

```shell
 ~/src $ ls -l
total 16
-rwxr-xr-x 1 billy workers 7257 May  2 23:09 a.out
-rw-r--r-- 1 billy workers  994 Apr 30 23:53 scope.c
-rw-r--r-- 1 root  root     169 May  2 23:09 stack_example.c
```

As you can see, running **ls -l** displays the file permissions as well as owner and group information. Above, a.out belongs to billy and the workers group. Billy can read, write, and execute a.out; anyone in the workers group can read and execute a.out; and anyone else can read and execute a.out.

Shorthand for these permissions is (base 10) 4, 2, 1 because each permission has three binary bits. Read permission alone is 100, write alone is 010, and execute alone is 001 in binary. Each of {read, write, execute} can apply to each of {owner, group; others}. That's three sets of three bits for a total of nine binary bits. Thus, it is common in Linux to express file permissions using a set of three base ten numbers. For example, the permissions on a.out above would be (base 10) 755 which is 111\|101\|101. 

Finally, the **chmod** utility lets us change file permissions. Basic usage is chmod 644 myfile. See **man chmod** for more advanced usage.

Today we wrapped up our discussion of file access in C. We looked at the different access mode flags, combining them, and the different file permissions under Linux. Permissions seem odd at first, but once you've studied them a bit they become very simple. Next up we continue our discussion of advanced topics with User IDs. 

More to come.

