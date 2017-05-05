---
layout: post
title: Rabbit Trail Redux
---

Today I am again time-poor, so I have again opted to write a little about my tooling. *Hacking: the Art of Exploitation* comes with a live CD for all your hacking needs, so I made it into a virtual machine for easy access. Here I'll talk about that process and link to a nice guide.

At first I was going to rip the iso off the included physical CD, which is time-consuming and lame. Then I found that No Starch Press's [product page for Hacking: Art of Exploitation](https://www.nostarch.com/hackingCD.htm) links to a [torrent of the iso](https://www.nostarch.com/download/Hacking%20The%20Art%20of%20Exploitation%202nd%20Edition%20Jon%20Erickson%20Official%20LiveCD%20ISO%20No%20Starch%20Press%20[mininova].torrent). I happily torrented it.

Next I used the iso file to build a virtual machine. A virtual machine is basically a miniature computer within your computer. In this case, since the *Hacking* live CD was based on Ubuntu, I now have a miniature Ubuntu system. It's especially nice, because the *Hacking* toolset is over seven years old. Anti-exploit tools in the Linux kernel have matured since then, making some of the books' exploits invalid. Additionally, the memory inspection sections are based on 32-bit architecture while I have a 64-bit machine. Using a virtual machine I can see the exact same things as the author. Everything works exactly as expected.

This setup was nice, but I wanted more. I found myself writing code in the virtual machine, and wanting to post it. This is possible with extra software provided by the virtual machine software. In my case, I tried to install some tools from VirtualBox. However, the provided installation did not work for me! I found out later this was due to the age of the gcc compiler provided with the *Hacking* disc. Anyway, in googling for a solution I came across a [very interesting github gist](https://gist.github.com/topalovic/e06a82c0f115a261e7b3e932caee3a4f). The gist described making a Vagrant box out of the *Hacking* CD. Vagrant is a semi-recent virtualization technology. It lets you configure virtual machines using command line, and the default access is SSH. Perfect for me! If everything worked out correctly, I would be able to talk to the *Hacking* box using SSH. This adds a lot of convenience to my workflow.

In short, I followed the gist's guide and set up my box. Along the way, I ran into a couple snags. The total setup took me three hours and some extra googling. So I [forked the gist](https://gist.github.com/lightski/0096743043f1165e32e257637c312765). I will add to it and write again about my modifications.

Long story short, I ended up with a very nice setup. Now, I open a shell at my vagrant directory and issue these commands.
```shell
    vagrant up
    vagrant ssh
```
This boots my virtual machine and connects me via ssh. I have the ~/src folder shared between the virtual machine and my computer. This lets me write code using my local (customized) vim, then switch to the virtual machine to compile and disassemble what I've written. Sending code to a post is as easy as using cat to read the file, copying relevant code, and pasting into the post. Very nice!

Anyway, I've very content with my setup now. Next time we'll continue the discussion of Linux UIDs.

More to come.


