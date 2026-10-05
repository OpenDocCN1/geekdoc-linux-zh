
# Chapter 3 · Investigating Linux's Principles and Philosophy

software world. After all, what we use today is built atop the foundation that was created in the past. Thus looking at how Linux originated will help you understand Linux as it exists today.

# Understanding Linux's Origins

![](img/77662199428609b7662c8dc9c0e45c10_57_0.png)

In 1991, as it was today, computers were classified by their sizes and capabilities. Computers could belong to any handful of categories, ranging from desktop personal computers (PCs) to supercomputers. .x86-based computers, which are the direct ancestors of today's PCs, dominated the PC marketplace of 1991; however, other types of PCs were available, including Macs. Such computers generated different CPUs and ran their own custom OS.

In 1991, most PCs ran Microsoft's Operating System (MS-DOS, PC-DOS, or DOS). DOS was extremely limited by today's standards; this single-tasking OS (capable of running only one application at a time) didn't take full advantage of the memory or CPUs at the time. The versions of Microsoft Windows were available in 1991 on top of DOS. Although the initial versions of Windows helped to work around some of DOS's limitations, they didn't fix any of them. These early versions of Windows employed cooperative multitasking, for instance, which programs could voluntarily give up CPU time to other processes. The DOS kernel could not control a program that choked CPU.

Computers today can be classified in much the same way as in 1991, although some details changed. A notable addition is embedded computers, or as smartphones.

![](img/77662199428609b7662c8dc9c0e45c10_57_1.png)

Above the PC level, Unix was a common OS in 1991. Compared to DOS and the version of Windows of that time, Unix was a sophisticated OS. Unix multiple applications and provided preemptive multitasking, in which the kernel could schedule CPU time for programs, even if the programs didn't voluntarily give up control. These features were necessities for many servers and for multiuser computers such as min and mainframes.

As time progressed, the capabilities of each class of computer have grown. By most measures, today's PCs have the power of computers or even the mainframes of 1991. The OSs used on the PCs of 1991 didn't scale well to more powerful hardware. Just having computing power itself, for this reason, DOS and its small-computer contemporaries have been largely abandoned in favor of Unix and other alternatives.

![](img/77662199428609b7662c8dc9c0e45c10_57_2.png)

Unix was not the only multiuser, multitasking in 1991. Others, as Virtual Memory Systems (VMS), were available. Unix is not relevant to Linux's history, though.

In 1991, Lin Torvalds was a student at the University of Helsinki, computer science. He was interested in learning about both Unix and the capabilities of the .x86 kernel he had just purchased. Torvalds began the program that would become the Linux kernel as a low-level emulator—a program to connect to his user's laptop computers. As his program grew, adding features that turned his terminal program into something that could be better described as an OS kernel. Eventually, he began

Today's versions of Windows are not derived from DOS. Instead, they use a new kernel that shares many features with VMS.

![](img/77662199428609b7662c8dc9c0e45c10_57_3.png)

# Exploring Linux through the Ages

writing with the goal of creating a Unix-compatible kernel—that is, a kernel that could run the wide range of Unix software that was available at the time. Unix's history, in turn, stretched back two more decades, to its origin at AT&T in 1969. Because AT&T was a telephone monopoly in the United States at AT&T's-t time, it was legally forbidden from selling software. Therefore, when its employees used Unix, AT&T basically gave the OS away. Universities were particularly enthusiastic about adopting Unix, and some began modifying it, because AT&T made the source code available. Unix had a two-decade history of open software development to start. Most Unix programs were distributed as source code, because Unix ran on a wide variety of hardware platforms—binary upgrades for one machine would seldom run on a different machine.

Early on, Linux began to tap into this reservoir of available software. As noted in Chapter 1, Linux developers were particularly keen on the GNU project's software, so Linux accumulated a collection of GNU utilities. Much of this software had been written with workstations and more-powerful computers in mind, but because computer hardware kept improving, run fine on the x86 PCs of the early 1990s.

# THE MICROKERNEL DEBATE

Linux is an example of a monolithic kernel, which is a kernel that does everything a kernel is supposed to do in one process. In 1991, a competing kernel design, known as a microkernel, was all the rage. Microkernels are much smaller than monolithic kernels; they move as many tasks as they can into nonkernel processes and manage the communications between processes.

Soon after Linux's release, Linux Torvalds engaged in a public debate with Andrew Tanbaum, the creator of Minix. Linux considered the monolithic design to be backward. As a practical matter for an end user, modern versions of Windows use microkernels, whereas Linux uses monolithic designs.

![](img/77662199428609b7662c8dc9c0e45c10_58_0.png)

> The 386BSD was a competing Unix-like in the early 1990s. Today it has forked to several related Os: FreeBSD, OpenBSD, DragonFlyBSD, and PC-BSD.

# Chapter 3 · Investigating Linux's Principles and Philosophy

# Seeing Today's World

By the mid-1990s, the most important features of Linux as it exists today had been established. Changes since then have included the following:

- **Improvements in the Kernel**: The Linux kernel has massive changes since 1991, when it lacked many of the features we rely on today. Improvements include the addition of networking features, innumerable hardware drivers, support for power management, and support for many non-x86 CPUs.
- **Improvements in Support Tools**: Just as work has progressed on the Linux kernel, improvements have also been made to the support programs on which it relies—the compilers, shells, GUIs, and so on.
- **Creation of New Support Tools**: New support tools have emerged over the years. These range from simple and small utilities to big desktop environments. In fact, some of these tools, such as modern desktop environments, are far more obvious to the user than the kernel itself.
- **Creation of New Distributions**: As noted earlier, Slackware dates to 1993 and Red Hat (the predecessor to Red Hat Enterprise, CentOS, and Fedora) originated in 1995. Other distributions have emerged in the intervening years, and some have been quite important. The Android OS used on smartphones and tablets, for instance, has become very influential over the past decade.

# Using Open Source Software

The philosophies that underlie software development for Linux are different from those that drive most software development for Windows. These differing philosophies affect how you obtain the software, what you can do with it, and how it changes over time. This section describes these principles. We also describe how Linux functions as a sort of “magnet,” integrating software from many sources into one place.

# Understanding Basic Open Source Principles

Broadly speaking, software can be described as coming in several forms, each with different expectations about payment, redistribution, and users' rights.
