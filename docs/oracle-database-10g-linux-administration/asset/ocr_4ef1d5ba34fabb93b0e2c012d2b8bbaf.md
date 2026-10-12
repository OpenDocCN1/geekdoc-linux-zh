# ## Operating System Overview

An operating system exists to allow the user to run programs. The Operating System consists of a number of different types of programs and layers that handle different types of functions. As with most terminology, the initial architects of the early operating systems used analogies in order to illustrate their point. The innermost core of the operating system became known as the kernel, and the outer layers of the operating system were appropriately labeled the shell. The shell is used by the user to interact with the operating system, and between the shell and the kernel lie the system utilities.

The kernel is responsible for operating systems services such as processes management, scheduling time on the CPU, memory management, and system calls. System calls allow the shell to communicate with the kernel and perform functions like accessing disks.

Several different types of kernels are very popular today, some of which may be familiar to you. The first of these is known as a monolithic kernel (shown in Figure 1-1), and is made up of only three layers.

The second type of kernel that is popular uses a microkernel. The microkernel architecture (shown in Figure 1-2) can have many more layers than the monolithic architecture.

# ## The Monolithic Kernel

A monolithic kernel is the simplest kind of kernel, and is created as one single executable, where each part of the kernel accesses the same memory structures. Monolithic kernels have a long tradition of use in operating systems such as UNIX, Windows, and DOS. Though some people believe the trend in more modern operating systems is not to use a monolithic design, Linux does use a monolithic kernel, and integrates its advantages without its traditional disadvantages.

The advantage of the monolithic kernel is that since it is one executable, all of the memory is available everywhere within the kernel. This means that data does not need to be passed between different layers of the operating system, thus improving

| Applications | Shell(s) |
| --- | --- |
| System Call Interface |  |
| Linux Kernel (monolithic) |  |
| Hardware |  |

![](bbox=[0.11, 0.9, 0.55, 0.92])