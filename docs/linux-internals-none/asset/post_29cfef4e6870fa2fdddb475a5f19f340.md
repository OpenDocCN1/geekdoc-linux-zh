
# Contents

**7 Signals Handling**
- Signal Description and Default Action
- Synchronous Signals
- Signals and Interrupts, a Perfect Couple
- Data Structure—include/linux/signal.h
- Data Structure—include/linux/kernel.h

**8 kHTTPd**
- Controlling kHTTPd
- Data Structure—linux/net/structure.h

**9 Linux System Calls**
- System Calls and Event Classes on the IA32
- Interrupts
- Exceptions
- An Example of Exceptions as Objects from Java
- Vectors
- The Linux System Call Interface
- More-Complex System Calls
- The User-Space System-Call Code Library
- Tracing System Calls
- How to Add Your Own System Calls
- List of Linux/IA32 Kernel System Calls
- Data Structures—include/linux/sys.h
- Data Structures—include/asm-i386/hw_irq.h

**10 File Systems**
- Logical Volume Manager (LVM)
- The Linux Kernel’s Relation to the File System
- Kernel Data Structure Objects for File System Control Operations
- The Common Data Structure Objects Instantiated by the Kernel
- Buffers, Caches, and Memory Garbage Collection
- Linux’s Use of Inodes
- Performance Issues and Optimization Strategies
- Raw I/O
- Process Resource Limits
- Extent-based Allocation (General)
- Block-based Allocation (General)
- The Transaction-Processing or Database Issue of Safety
- Advantages of Journaling over Nonjournaling
- How a Journaling File System Works
- Metadata Logging
- Available Journaling File Systems
- IBM's JFS
- Main JFS Data Structures and Algorithms
- Standard Administrative Utilities
- How JFS is Set Up at Boot Time
- Block Allocation Map
- Inode Allocation Map
- AG Free Inode List
- IAG Free List
- Fileset Allocation Map Inodes
- Design Features of JFS versus Other File Systems
- JFS's Further Extensive Use of B+-Trees
- Leaf Nodes
- Internal Nodes
- Variable Block Size
- Directory Organization
- JFS's Support for Sparse and Dense Files
- Aggregates and Filesets
- Logs
- Logical Volume Manager Abstract
- Configuration Concept
- Example
- Overview and Concept of Commands
- Sample LVM Session Output
- Data Structures—include/linux/fsh

**A Bibliography**
- Papers and Books

**B The GNU License**

**C Logical Volume Manager Abstract**

**D Kernel Parameters v2.2.9**

Index

# Preface

In the last two years, first with version 2.0, then 2.2, and soon 2.4, Linux has undergone amazing progress to what now constitutes probably one of the most advanced operating systems for servers and workstations alike.

Especially with the upcoming 2.4 series, much effort has been put by us developers into making the kernel highly scalable and able to efficiently handle and manage huge quantities of memory, many concurrent CPUs, and a vast array of modern peripherals.

If somebody until a few years ago could go read the kernel source code and understand the main concepts by herself, it has become very hard indeed today. Not only has the size of the source code grown significantly, but as the core developers themselves learned new techniques and technologies, the algorithms and source code have become increasingly complex and hard-to-understand.

Moshe Bar’s work in bringing the intricacies of the Linux kernel 2.3.xx and 2.4 closer to the enthusiast, the system administrator, and system programmer is important to bridge the gap between kernel developers and users.

During the making of this book, I was in close contact with Moshe and had to face and answer dozens of questions. He never accepted an answer as such until he fully understood the algorithm or functionality.

As a core kernel developer, I have found this book to be a good introduction as well as a reference work to be used to look up the Linux kernel concepts.

Moshe Bar has over the years written a great deal of articles, papers, and treatises on OS principles and his involvement with prior OS projects, such as MVS, VM, and BSD shows in his thorough approach and clear technical language.

Ingo Molnar

# Introduction

Linux Internals was written to enhance the general understanding of the inner workings of Linux. Most of these “internals” happen to be in a kernel inside the Linux operating system kernel. This book is, however, not a full source code commentary in the common sense of the term. Certainly a lot of the code is commented, but the emphasis is rather on the functionality of the code, rather than on the code itself.

The Linux kernel contains the code that controls a system’s resources, user processes, data I/O, and extended functions, such as the Linux kernel-space web server kHTTPd.

## The Linux Kernel

A *kernel* is operating system software that runs in protected mode and has access to the hardware’s privileged registers. Some operating systems employ a *microkernel architecture*, where device drivers and other code are loaded and executed on demand, and do not necessarily reside always in memory.

The kernel is not a separate process running on the system. It is the guts of the operating system, which controls the scheduling of processes to achieve multitasking and provides a set of routines, constantly in memory, to which every user-space process has access.

By contrast, a *monolithic architecture*, in which all device drivers are part of the kernel proper, is more common among UNIX implementations, and is the design employed by classics such as BSD. The Linux kernel, too is a mostly monolithic kernel—all device drivers are part of the kernel proper—but unlike BSD, a Linux kernel’s device drivers also can be *loadable*, that is, they can be loaded and unloaded from memory through user commands.

This book primarily references the 2.4.x series of kernels for the Intel x86 architecture (at the time of this writing, still called 2.3.51). All code samples used throughout this book are based on the 2.3.49 kernel, although sometimes, a preview on the 2.5 kernel series is used.

## Who Should Read This Book

Linux Internals is targeted at system and network administrators, developers, and capacity planning managers. It will also appeal to Linux enthusiasts who have a good general understanding of hardware and software.
