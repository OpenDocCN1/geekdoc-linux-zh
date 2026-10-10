Before version 2.1.39 of Linux, the separation of kernel and user memory was accomplished using the segmentation process. Linux currently makes no use of segmentation. Now the separation is accomplished simply as an allocation policy. This incidentally makes x86 Linux more like Alpha Linux. The Alpha architecture has no segmentation. Segmentation is discussed in chapters 12 and 13.

# 8.2.4 Kernel Pages

The Linux paging algorithm never pages kernel memory out to disk. The Linux kernel is therefore always in RAM.

This is one reason that compiling Linux specially for each machine is worthwhile. If the kernel is compiled with code which isn't needed, such as device drivers for devices the machine doesn't have, RAM will be permanently occupied by code which is never used.

It is also the reason that machines require approximately 4 Meg of RAM, depending on the Linux version, to run Linux at all.

# 8.2.5 Kernel Modules

Although kernel memory is never touched by the paging system, it has been possible since Linux version 2.0 to add or delete chunks of kernel memory, provided they have been compiled separately as modules. The commands

```
linuxbox$ insmod module
```

for "install module" and

```
linuxbox$ rmmod module
```

for "remove module" do change the amount of RAM occupied by the kernel. To inspect memory to find out the amount of memory available, the Linux command

```
linuxbox$ free
```

is useful.

# 8.3 Address Translation

Linux user memory addresses are virtual addresses, not actual physical addresses. Linux uses paging to translate virtual addresses to RAM addresses. x86 paging obtains its translations from page tables set up by the operating system. Since the translation process is hardwired into the processor, x86 page tables must have the two-tiered structure shown in Figure 8-6.

![](bbox=[0.15, 0.76, 0.85, 0.98])

# **Figure 8-6. x86 Page Table Structure**