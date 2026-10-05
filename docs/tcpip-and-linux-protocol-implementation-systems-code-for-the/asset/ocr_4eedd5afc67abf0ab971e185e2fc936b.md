# TCP/IP and Linux Protocol Implementation

Because of its special status in network code, we dissect a day in the life of a kernel module, and show how this gives Linux the properties of a microkernel, but without the overhead of server or helper processes with their associated context and IPC overheads.

Getting down to more detail, we examine a day in the life of a system call, and getting from one space to another.

After that, we take a look at the operating system's idea of time and events. We wrap up the chapter with a multiprocessor support, and in particular, the effect of symmetric multipcessing (SMP) design on other parts of the operating system and networking implementation.

# 2.2 What Is an Operating System?

An operating system (OS) provides services. Typical services that a user wants include management of storage through a filesystem and backup system; the ability to run application programs; easy access to the network; and management of a Graphical User Interface.

There are several different approaches to designing and building such software. At its simplest, each of operating system is a collection of libraries of commonly used functions. An OS usually incorporates a number of utility programs (operations and management applications). However, what makes an operating system different from other collections of code is that much of the OS code interfaces between the hardware and applications.

Services are provided by a set of layers of software which unify common elements and hide the idiosyncratic details of the underlying hardware. Access to hardware requires use of specific instructions and memory addresses that the system may wish to protect the normal user from accidentally disturbing. Hardware may autonomously wake up and attempt access memory or interrupt the processor at any moment—this is especially true of user interface hardware (mice, keyboards) and networking interfaces. While user programs (applications) are increasingly being implemented by programmers who are familiar with an event-driven programming paradigm, it is still hard to design systems that manage large numbers of competing streams of events—gone are the says when cooperative multitasking was a viable way for the everyday program to manage resources on a system. This role is largely taken by the kernel of the operating system. Applications are largely insulated from this level of complexity.

Different operating systems have been designed with different types of users in mind. This means that the three general purpose operating systems in most common use today in the world, UNIX, Windows, and MAC OS, have undergone different pressures during their development. This has led to quite a different emphasis on how services are provided.