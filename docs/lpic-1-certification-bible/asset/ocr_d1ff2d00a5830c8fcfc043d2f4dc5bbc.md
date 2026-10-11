T he kernel is the core of the Linux system. Most Linux distributions ship with a kernel that supports as much hardware as possible and that comes with as many features as possible. The problem with this is you sometimes get a kernel that is not as lean and mean as possible. Some features may cause problems or slow the kernel down. Even if you never upgrade a system’s hardware, you will most likely have to upgrade the Linux kernel eventually. New kernels provide performance increases, security fixes, and new hardware support.

This chapter goes through obtaining, configuring, compiling, and installing a new kernel, as well as configuring drivers and modules to support new hardware.

# ## Kernel Overview

The Linux kernel can seem daunting to new users, but does not need to be. The Linux kernel is responsible for mediating between the system’s hardware and Linux programs. It handles the memory management for the operating system to make sure each process gets its own memory range. The kernel also divides up the processor’s time to make sure each application gets a fair share of the processor’s use. Hardware drivers are also part of the kernel and provide an interface for the operating system and its applications to talk to hardware.

# ## Kernel development

When it is time to update the kernel on a system, you may be surprised at the number of choices you have. The Linux kernel development system can sometimes be confusing, but understanding it is important so that you know which version to use on a system.

Linus Torvalds, the original Linux kernel author, is still head of the kernel development effort. Many other people around the world also work on the kernel and submit new patches and features. Who does the kernel development is not as important as how they release their work.

At any given time, two current kernel versions will usually be available. Why two? Because a stable tree and a development tree are being worked on simultaneously.

The kernel version numbers are pretty simple to understand. They use the following syntax:

```
*major.minor.patch*
```