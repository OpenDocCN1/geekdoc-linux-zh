
![](img/c27875544958897d817484d558c208c8_32_0.png)

processors, computer games, graphical manipulation programs, and computer system utilities. The second type, **operating system** (OS) software, consists of a series of software components used to control the hardware of your computer. Without an operating system, you would not be able to use your computer. Turning on a computer loads the operating system into computer hardware, which then loads and centrally controls all other application software in the background. At this point, the **user** (the person using the computer) is free to interact with the applications, perhaps by typing on the keyboard or clicking a mouse. Applications then take the information supplied by the user and relay it to the operating system. The operating system then uses the computer hardware to carry out the requests. The relationship between users, application software, operating system software, and computer hardware is illustrated in Figure 1-1.

The operating system carries out many different tasks by interacting with many different types of computer hardware. For the operating system to accomplish this, it must contain the appropriate device driver software for every hardware device in your computer. Each **device driver** tells the operating system how to use that specific device. The operating system also provides a **user interface**, which is a program that accepts user input indicating what is to be done, forwards this input to the operating system for completion, and, after it is completed, gives the results back to the user. The user interface can be a command-line prompt, in which the user types commands, or it can be a **graphical user interface** (GUI), which consists of menus, dialog boxes and symbols (known as icons) that the user can interact with via the keyboard or the mouse. A typical Linux GUI is shown in Figure 1-2.

Finally, operating systems offer **system services**, which are applications that handle system-related tasks, such as printing, scheduling programs, and network access. These system services determine most of the functionality that is seen in an operating system. Different operating systems offer different system services, and many operating systems allow users to customize the services they offer. A **server** is a computer with an operating system that is configured to allow other computers to connect to it from across a network.

![](img/c27875544958897d817484d558c208c8_32_1.png)

**Figure 1-1** The role of operating system software

![](img/c27875544958897d817484d558c208c8_33_0.png)

**Figure 1-2** A Linux graphical user interface

## The Linux Operating System

**Linux** (pronounced “lih-nucks”) is an operating system that is used today to run a variety of applications on a variety of different hardware. Similar to other operating systems, the Linux operating system loads into computer memory when you first power on your computer and initializes (or activates) all of the hardware components. Next, it loads the programs that display the interface. From within the interface you can execute commands that tell the operating system and other applications to perform specific tasks. The operating system then uses the computer hardware to perform the tasks required by the applications.

Linux has the ability to manage thousands of tasks at the same time, including allowing multiple users to access the system simultaneously. Hence, Linux is referred to as a **multiuser** and **multitasking** operating system.

### Versions of the Linux Operating System

The core component of the Linux operating system is called the **Linux kernel**. The Linux kernel and supporting software (called function libraries) are written almost entirely in the C programming language, which is one of the most common languages that software developers use when creating programs.

Although a variety of software can be used to modify the appearance of Linux, the underlying kernel is common to all types of Linux. The Linux kernel is developed continuously; thus, it is important to understand the different version numbers of the Linux kernel to decide which kernel version is appropriate for your needs. Because the Linux kernel is directly responsible for controlling the computer's hardware (via device drivers), you might sometimes need to upgrade the Linux kernel after installing Linux, in order to take advantage of new technologies or to fix problems (also known as bugs) related to your computer's hardware. Consequently, a good understanding of your system's hardware is important in deciding which kernel to use.

![](img/c27875544958897d817484d558c208c8_34_0.png)

> A complete list of kernels, kernel versions, and their improvements can be found on the Internet at www.kernel.org.

In some cases, updates in the form of a kernel module or a kernel patch can be used to provide or fix hardware supported by the kernel. Kernel modules and kernel patches are discussed later in this book.

### Identifying Kernel Versions

Linux kernel versions are made up of the following three components:

- Major number
- Minor number
- Revision number

Let's look at a sample Linux kernel version, 3.15.9. In this example, the **major number** is the number 3, which indicates the major revision to the Linux kernel. The **minor number**, represented by the number 15, indicates the minor revision and stability of the Linux kernel. An odd minor number indicates a developmental kernel, whereas an even minor number indicates a production kernel. **Developmental kernels** are not fully tested and imply instability; they are tested for vulnerabilities by people who develop Linux software. **Production kernels** are developmental kernels that have been thoroughly tested by several Linux developers and are declared to be stable. In the previous example, the kernel has a major number of 3 and a minor number of 15. Because the minor number is odd, you know that this is a developmental kernel. This kernel will eventually be improved by Linux developers, tested, and declared stable. When this happens, the version of the kernel will change to 3.16 (indicating a production kernel).

Linux kernel changes occur frequently. Those changes that are very minor are represented by a *revision number* indicating the most current changes to the version of the particular kernel that is being released. For example, a 3.16.12 kernel has a major number of 3, a minor number of 16, and a revision number of 12. This kernel is the 12th release of the 3.16 kernel. Some kernels might have over 100 different revisions, as a result of developers making constant improvements to the kernel code.

![](img/c27875544958897d817484d558c208c8_34_1.png)

> When choosing a kernel for a mission-critical computer such as an e-mail server, ensure that the minor number is even. This reduces the chance that you will encounter a bug in the kernel and, hence, saves you the time needed to change kernels.

Table 1-1 shows the latest revisions of each key major and minor kernel released since the initial release of Linux.

| Kernel Version | Date Released | Type |
| :--- | :--- | :--- |
| 0.01 | September 1991 | First Linux kernel |
| 0.12 | January 1992 | Production (stable) |
| 0.95 | March 1992 | Developmental |
| 0.98.6 | December 1992 | Production (stable) |
| 0.99.15 | March 1994 | Developmental |
| 1.0.8 | April 1994 | Production (stable) |
| 1.1.95 | March 1995 | Developmental |
| 1.2.12 | July 1995 | Production (stable) |
| 1.3.100 | May 1996 | Developmental |
| 2.0.36 | November 1998 | Production (stable) |
| 2.1.132 | December 1998 | Developmental |
| 2.2.26 | February 2004 (latest release; was developed concurrently with newer kernels) | Production (stable) |
| 2.3.99 | May 2000 | Developmental |
| 2.4.17 | December 2001 | Production (stable) |
| 2.5.75 | July 2003 | Developmental |
| 2.6.35 | August 2010 | Production (stable) |
| 3.2.62 | January 2012 | Developmental |
| 3.4.103 | May 2012 | Production (stable) |
| 3.10.54 | June 2013 | Production (stable) |
| 3.12.28 | November 2013 | Production (stable) |
| 3.14.18 | March 2014 | Production (stable) |
| 3.15.10 | March 2014 | Developmental |
| 3.16.2 | September 2014 | Production (stable) |

Table 1-1 Latest revisions of common Linux kernels

## Licensing Linux

Companies often choose Linux as their operating system because of the rules governing Linux licensing. Unlike most other operating systems, Linux is freely developed and continuously improved by a large community of software developers. For this reason, it is referred to as *Open Source Software* (OSS).

To understand what OSS is, you must first understand how source code is used to create programs. **Source code** refers to the list of instructions that a software developer writes to make up a program; an example of source code is depicted in Figure 1-3.
