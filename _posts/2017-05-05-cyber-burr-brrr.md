---
layout: post
title: Cyber Burr Brrr
---

Hacking post day the ninth. These days, it's all about the cyber. We continue with a discussion of Linux user IDs (aka UIDs (aka cyber UIDs)).

Every user and group in Linux has a unique ID number; they are UIDs and GIDs respectively. View IDs using the **id** command on Linux shell.
```shell
$ id user
$ id $(whoami)
```

First command will return results of "user" UIDs plus any applicable GIDs. The second command gets the logged in user (via subshell) then asks for IDs related to that. So far, so good.

Sometimes, multiple users must make changes to a shared file. Linux has a permission to allow this, called *set user ID* aka setuid. Set it on myfile.sh like so: sudo chmod u+s ./myfile.sh. When a program has this permission, it runs as the file's **owner** instead of current user. The UID we're running as currently is known as the *effective UID* or euid.

In C, we can view both uid and euid with very simple functions. Here's a brief demo program:
```c
#include <stdio.h>

int main() {
    printf("real uid: %d\n", getuid());
    printf("effective uid: %d\n", geteuid());
}
```

So, when we need to provide access to some shared resource, we can give root access to that resource. Set our program to run as root. Then, track the uid running the program. When writing to resource, record uid of author. To retrieve data from resource, read uid and only return results written by that uid. Clear as mud.

Thus ends our discussion of UID, GUID, and eUID. Tomorrow we'll continue travelling the way of C with structs.

More to come.
