
## Chapter 14 Signals 341
- Signal Data Structures 342
- Signal Anticipation 345
- Signal Delivery 346
- Signal Recognition 349
- Signal Handler Launch 350
- Signal Handler Return 351
- Summary 351

## Chapter 15 System Initialization 353
- ISL: The Initial System Loader 354
- HPUXBOOT: The Secondary Loader 355
- Real-Mode Initialization 356
- Virtual Mode Initialization 358
- Summary 360

## Chapter 16 Tools Overview 361
- adb 361
- q4 363
- Examining Data and Code 363
- Getting Data Type Information 364
- Loading a Structure into a Pile 364
- Displaying the Contents of a Pile 365
- Using Skip to Load Structures 365
- Loading Multiple Structures 366
- Loading Linked Lists 366
- Using Values from a Pile 366
- Manipulating Piles 367
- An Example: Getting the uarea of a Process 368
- Tracing Stacks 369
- Using Perl Scripts in q4 370
- Summary 371

## Index 373

# PREFACE

While there are many books about the UNIX kernel in its various versions, this is the first to deal specifically with HP-UX and Hewlett-Packard’s PA-RISC architecture. This book is a technical resource for anyone who has to support HP-UX, write kernel modules, or just wants to know how it all works. It is suitable as a text for a class in operating system concepts or HP-UX internals.

# Chapter 1 PA-RISC 2.0 Architecture

Chapter 1 presents some of the important features of the PA-RISC architecture, still the predominant hardware platform for HP-UX. It covers the register set and how the registers are used, then explains virtual memory concepts, address translation and caching, the mechanisms provided by the architecture to support virtual memory, and some of the most common PA-RISC instructions and their use.

# Chapter 2 Procedure Calling Conventions

This chapter examines the conventions used when calling from one procedure to another: how the stack is used and how stack frames are set up, how the registers are used, how arguments are passed, and how results are returned to the calling process. Stack usage for both narrow and wide modes is explained.

# Chapter 3 The Kernel: Basic Organization

This chapter examines the basic organization of the kernel data structures, both hardware-dependent and hardware-independent. The discussion includes tables, the kernel as a resource manager, and kernel memory allocation. In addition, many common kernel algorithms and methodologies are presented for the reader's consideration.

# Chapter 4 Programs, Processes, and Threads

The process has long been the workhorse of the UNIX environment. Modern UNIX operating systems have adopted the thread as the new schedulable entity. Chapter 4 examines both the process and the thread, and their relationship to resources and task management. One of the most important aspects of understanding the process/thread environment is in flow of control followed when a system call is requested. The transition from user mode to system mode and the return to user mode are examined in detail in Chapter 4.

# Chapter 5 Process and Thread Management from the Process's Viewpoint

This chapter explores processes and threads: how they are created, how they are terminated, and how they are scheduled to run. The internal data structures that keep track of the processes and threads are explained. We cover how memory is managed for processes and how addresses are mapped, and we look at process priorities and how they change throughout the life of the process.

# Chapter 6 Managing Memory

Chapter 6 looks further into memory management by looking at systemwide memory resources. It explains how the per-process memory areas are allocated from systemwide memory and how that memory is mapped to physical memory. This chapter addresses physical and virtual memory, page regions, and address aliasing.

# Chapter 7 The HP-UX Paging System

To complete our tour of the kernel's memory management system, Chapter 7 discusses the HP-UX paging system (commonly called the swapper). The following topics are included in the discussion:
- Demand paging
- Swap versus paging
- lotstree and vhand
- Deallocation
- Pseudo-swap
- Swap chunks

# Chapter 8 Files and File Systems

This chapter looks at the structures both in memory and on disk that make up the HP-UX file systems. HP-UX supports a number of file system layouts. This chapter looks in detail at the UNIX File System layout and the Virtual File System layer, which allows the kernel to work easily with the various file system types. It also explains various caching systems and how the dynamic buffer cache is used to complete disk transfers.

Although the Veritas File System (VxFS) is part of HP-UX, its internals are proprietary to Veritas and are not covered in depth. The merits of a journal file system and extent-based disk space allocation, however, are discussed in this chapter.

# Chapter 9 The Process Life Cycle, Cradle to Grave

Chapter 9 explores the process's life cycle in detail: how it is created, how it is maintained, and how it is terminated. Shared objects are discussed from the process point of view and the following kernel routines and features are presented in detail:
- fork()
- exec()
- wait()
- exit()
- Copy-on-write
- Copy-on-access

# Chapter 10 I/O and Device Management

Chapter 10 explores how the system performs I/O. It explains how I/O is performed at a low level in the PA-RISC architecture, including addressing, DMA, and interrupts. It then discusses how I/O works from the application's point of view, including device files and I/O configuration. We cover the steps in between with a discussion of how device drivers claim devices and how I/O requests make their way from the device files through the device drivers to the physical I/O devices. I/O is presented within the umbrella of the General I/O subsystem.

# Chapter 11 The Logical Volume Manager

The logical volume manager (LVM) is a disk management subsystem. It provides a layer of abstraction between the physical disks and the disk I/O system. This chapter looks at how LVM combines physical disks into volume groups, divides those volume groups into logical disk volumes, and provides mirroring for data redundancy. The structures used within the kernel as well as the on-disk structures are discussed.

# Chapter 12 Multiprocessing and HP-UX

This chapter covers the elements of the kernel that facilitate multiprocessing. We look at some of the issues of having multiple processors sharing main memory and I/O devices. Then we look in detail at the data structures and interfaces that provide for consistent access to these resources among multiple processors. This includes spinlocks and semaphores for controlling exclusive access to resources and also load-balancing between processors.

# Chapter 13 Kernel Services

Chapter 13 investigates the mechanisms in the kernel for supporting communication between processes: semaphores, message queues, shared memory, and signals. The kernel structures that support these features and the kernel tunables that control them are explained. We look at the user interfaces to these facilities and examine the kernel callout system, which allows a process to request a future signal from the kernel.

# Chapter 14 Signals

Signals were traditionally sent from one process to another and usually meant that a process needed to terminate. With the advent of threads, the entire signal system has become more complex. Chapter 14 discusses both traditional and new uses and methods for signals. We will discuss in turn the following HP-UX kernel supported signaling schemes: System-V, Berkeley, and POSIX.

# Chapter 15 System Initialization

HP-UX runs on many different platform designs, using a variety of boot sequences. Chapter 15 explains what takes place once the specific boot criteria has been satisfied and the kernel is off and running. This sequence of events is broken down into the real main, virtual main, and I/O initialization steps.

# Chapter 16 Tools Overview

Chapter 16 explains the practical use of two important tools, adb and q4.
