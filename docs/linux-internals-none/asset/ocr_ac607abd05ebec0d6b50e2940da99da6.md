# # Introduction

Linux Internals was written to enhance the general understanding of the inner workings of Linux. Most of these “internals” happen to be in a kernel inside the Linux operating system kernel. This book is, however, not a full source code commentary in the common sense of the term. Certainly a lot of the code is commented, but the emphasis is rather on the functionality of the code, rather than on the code itself.

The Linux kernel contains the code that controls a system’s resources, user processes, data I/O, and extended functions, such as the Linux kernel-space web server kHTTPd.

# ## The Linux Kernel

A *kernel* is operating system software that runs in protected mode and has access to the hardware’s privileged registers. Some operating systems employ a *microkernel architecture*, where device drivers and other code are loaded and executed on demand, and do not necessarily reside always in memory.

The kernel is not a separate process running on the system. It is the guts of the operating system, which controls the scheduling of processes to achieve multitasking and provides a set of routines, constantly in memory, to which every user-space process has access.

By contrast, a *monolithic architecture*, in which all device drivers are part of the kernel proper, is more common among UNIX implementations, and is the design employed by classics such as BSD. The Linux kernel, too is a mostly monolithic kernel—all device drivers are part of the kernel proper—but unlike BSD, a Linux kernel’s device drivers also can be *loadable*, that is, they can be loaded and unloaded from memory through user commands.

This book primarily references the 2.4.x series of kernels for the Intel x86 architecture (at the time of this writing, still called 2.3.51). All code samples used throughout this book are based on the 2.3.49 kernel, although sometimes, a preview on the 2.5 kernel series is used.

# ## Who Should Read This Book

Linux Internals is targeted at system and network administrators, developers, and capacity planning managers. It will also appeal to Linux enthusiasts who have a good general understanding of hardware and software.