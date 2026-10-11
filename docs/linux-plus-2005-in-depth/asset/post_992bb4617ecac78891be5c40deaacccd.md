
between a program and a process is small. A program is a file stored on your computer, whereas a process is that file in action, performing a certain task.

Two different types of programs are executed on a computer: **applications**, which include those programs designed for a specific use and with which you commonly interact, such as word processors, computer games, graphical manipulation programs, and computer system utilities, and **operating system (OS)** software, which consists of a series of software components used to control the hardware of your computer. Without an operating system, you would not be able to use your computer. Turning on a computer loads the operating system into computer hardware, which loads and centrally controls all other application software in the background. Applications then take the information that users send them and relay that information to the operating system. The operating system then uses the computer hardware to carry out the requests. The relationship between users, application software, operating system software, and computer hardware is illustrated in Figure 1-1.

![](img/09bf13b782f71165e17bb3839040c96a_21_0.png)

**FIGURE 1-1** *The role of operating system software*

The operating system carries out many different tasks by interacting with many different types of computer hardware. For the operating system to accomplish this, it must contain the appropriate **device driver** software for every hardware device in your computer. Each device driver tells the operating system how to use that specific device. The operating system also provides a **user interface**, which is an application program that accepts user input indicating what is to be done, forwards this input to the operating system for completion, and, after it is completed, gives the results back to the user. The user interface can be a **command-line prompt** where the user must type a command to tell the operating system what to do, or it can be a **graphical user interface (GUI)**, which consists of a series of visual depictions of tasks known as icons, that the user can use to control the operating system, as shown in Figure 1-2.

![](img/09bf13b782f71165e17bb3839040c96a_22_0.png)

**FIGURE 1-2** *A Linux graphical user interface*

Finally, operating systems offer **system services**, which are applications that handle system-related tasks, such as printing, scheduling programs, and network access. These system services determine most of the functionality that is seen in an operating system. Different operating systems offer different system services, and many operating systems allow users to customize the services they offer.

## **The Linux Operating System**

**Linux** (pronounced “Lih-nucks”) is an operating system that is used today to run a variety of applications on a variety of different hardware. Similar to other operating systems, the Linux operating system loads into computer memory when you first power on your computer and initializes all of the hardware components. Next, it loads the programs required to give you an interface from which you can enter commands that tell the operating system and other applications to load to perform specific tasks. In the usual way, the operating system then uses the computer hardware to perform the tasks required by the applications.

Linux has the ability to manage thousands of tasks at the same time, including allowing multiple users to access the system simultaneously. Hence, Linux is referred to as a **multiuser** and **multitasking** operating system.

### Versions of the Linux Operating System

The core component of the *Linux* operating system is called the Linux **kernel**. The Linux kernel and supporting function libraries are written almost entirely in the C programming language, which is one of the most common languages that software developers use when creating programs.

Although a variety of different software can be used to modify the appearance of Linux, the underlying kernel is common to all Linux. The Linux kernel is developed continuously, and, thus, it is important to understand the different **version** numbers of the Linux kernel to decide which kernel version is appropriate for certain needs. Because the Linux kernel is directly responsible for controlling the hardware (via device drivers) in your computer, upgrading the Linux kernel might be necessary to take advantage of new technologies such as *IEEE 1394 (FireWire)*, or to fix problems (also known as *bugs*) the present kernel has with existing hardware. Consequently, a good understanding of what hardware features your system needs to use is important in deciding which kernel to use.

![](img/09bf13b782f71165e17bb3839040c96a_23_0.png)

> **NOTE**
>
> A complete list of kernels, kernel versions, and a list of their improvements can be found on the Internet at `http://www.kernel.org`.

In some cases, a kernel module or a kernel patch can be used to provide or fix hardware supported by the kernel. Kernel modules and kernel patches are discussed later in this book.

### Identifying Kernel Versions

Linux kernel versions are made up of the following three components:

- Major number
- Minor number
- Revision number

Let's look at a sample Linux kernel version, *2.5.9*. In this example, the **major number** is the number 2, which indicates the major revision to the Linux kernel. The **minor number**, represented by the number 5, indicates the minor revision and stability of the Linux kernel. If the minor number is odd, it is referred to as a developmental kernel, whereas if the minor number is even, it is referred to as a production kernel. **Developmental kernels** are not fully tested and imply instability; they are tested for vulnerabilities by people who develop Linux software. **Production kernels** are developmental kernels that have been thoroughly tested by several Linux developers and are declared to be stable. In the previous example, the kernel has a major number of 2 and a minor number of 5. Because the minor number is odd, it indicates that this is a developmental kernel. This kernel will eventually be improved by Linux developers, tested, and declared stable. When this happens, the version of this kernel will change to 2.6 (indicating a production kernel).

Linux kernel changes occur frequently. Those changes that are very minor are represented by a revision number indicating the most current changes to the version of the particular kernel that is being released. For example, a $2.6.12$ kernel has a major number of 2, a minor number of 6, and a revision number of 12. This kernel is the 12th release of the 2.6 kernel. Some kernels might have over 100 different revisions as a result of developers making constant improvements to the kernel code.

> **TIP**
>
> When choosing a kernel for a mission-critical computer such as an e-mail server, ensure that the minor number is even. This reduces the chance that you will encounter a bug in the kernel and, hence, saves you the time needed to change kernels.

Table 1-1 shows the latest revisions of each major and minor kernel released since the initial release of Linux.

**Table 1-1 Latest revisions of common Linux kernels**

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
| 2.2.26 | February 2004 | Production (stable) |
| 2.3.99 | May 2000 | Developmental |
| 2.4.17 | December 2001 | Production (stable) |
| 2.5.75 | July 2003 | Developmental |
| 2.6.7 | June 2004 | Production (stable) |

## **Licensing Linux**

The method of Linux licensing is one of the major reasons companies choose Linux as their operating system. As an operating system, Linux is unique compared to most other operating systems because it is freely developed and continuously improved by a large community of software developers. For this reason, it is referred to as **Open Source Software (OSS)**. To understand what OSS is, you must first understand how source code is used to create software programs. **Source code** refers to the list of instructions that a software developer writes to make up a program; an example of source code is depicted in Figure 1-3.

```c
#define MODULE
#include <linux/module.h>
int init_module(void){
    printk("My module has been activated.\n");
    return 0;
}
void cleanup_module(void){
    printk("My module has been deactivated.\n");
}
```

![](img/09bf13b782f71165e17bb3839040c96a_25_0.png)

After the instructions are finished, the source code is compiled into a format (called machine language) that only your computer’s processor can understand and execute. To edit an existing program, you must edit the source code and then recompile it.

The format and structure of source code follows certain rules defined by the **programming language** in which it was written. Many different programming languages are available that you can use to write source code for Linux. After being compiled into machine language, all programs look the same to the computer operating system, regardless of the programming language from which they were created. As a result, software developers choose a programming language to create source code based on ease of use, functionality, and comfort level.

The concept of Open Source Software enables software developers to read the source code of other people’s software, modify that source code to make the program better, and redistribute
