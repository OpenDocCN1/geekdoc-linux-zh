
change parameters—For example, various timeout values for the TCP transport protocol or configuration parameters of other protocol instances. There is even a way to use the Proc file system to enable and disable certain functions at runtime, such as packet forwarding.

IP Next Generation: Since Version 2.1.38, the Linux kernel provides a stable and relatively complete implementation of the new Internet Protocol IPv6. (See Chapter 23.)

And, finally, the best argument: Linux is free of charge. Everyone can download it from the Internet or buy it on CD for a few dollars, usually with a few gigabyte applications (some of them being more useful, some less) and with extensive installation instructions and free support. This means that, for very little money, you can get a high-performing, extremely stable, and easily adaptable operating system that turns a Pentium PC into a high-performing workstation, a highly reliable server, or an individually configurable Internet router.

This chapter has been a brief introduction to Linux: the next chapter will introduce the internal structure of the Linux kernel. We will then discuss the basic structure of communication systems in general and the structure of the Linux network architecture in particular.

## CHAPTER 2
## The Kernel Structure

This chapter deals with the basic architecture of the Linux kernel and its components. It provides an overview of the most important areas of the kernel, such as the different forms of activity in the kernel, memory management, device drivers, timers, and modules. Each of these issues will be discussed briefly in this book, to give you an insight into why knowing them is essential for the tasks and processes of each component. Detailed information about each of these issues is found in other books and references. A choice of corresponding sources is given in the bibliography, where we particularly recommend [RuCo01]; [BBDK+01], and [BoCo00].

The goal of this chapter is to describe the framework in which the Linux network operates. All areas described below offer basic functions required to offer network services in the first place. This is the reason why is an essential prerequisite for an understanding of the implementation of the Linux networking architecture.

Figure 2-1 shows the structure of the Linux kernel. The kernel can be divided into six different sections, each possessing a clearly defined functionality and offering this functionality to the other kernel components. This organization is also reflected also in the kernel's source code, where each of these sections is structured in its own subtree.

- Process management: This area is responsible for creating and terminating processes and other activities of the kernel (software interrupts, tasks, etc.). In addition, this is the area where inter communication (signals, pipes, etc.) takes place. The scheduler is the main component of process management. It handles all active, waiting, and blocked processes and take care that all application processes obtain their fair share of the processor's computing time.

- Memory management: The memory of a computer is one of the most important resources. A computer's performance strongly depends on the main memory it is equipped with. In addition, memory management is responsible for allowing each process its own memory section, which has to be protected against access by other processes.

![](img/5a25b942ec3329b8799f2b5f0de564f6_33_0.png)

FIGURE 2-1
Structure of the Linux kernel according to [RuCo01].

- File systems: In UNIX, the file system as a central role. In contrast to other operating systems (e.g., Windows NT), almost everything is handled over the file system interface. For example, device drivers can be addressed as files and the Proc file system (see Section 2.8) allows you to access data and parameters with the kernel. These two functionalities can be used very effectively and elegantly, so that they are often used for debugging purposes (see Appendix B.)

- Device drivers: Device drivers abstract from the underlying hardware in every operating system, and they allow you to access this hardware. The modular concept of Linux we will introduce in Section 2-4 offers a way to add or remove device drivers during a running operation, despite its monolithic kernel.

- Network: Network operations have to be managed by the operating system, because certain network operations cannot be allocated to a specific process, such as handling an incoming packet. Incoming packets are asynchronous events. They have to be collected, identified, and forwarded before a process can handle them. This is the reason why the kernel is responsible for the handling of packets across process and network interfaces.

Within the kernel, defined interfaces are used to facilitate the design of new functionalities. For instance, there is an interface to the virtual file system, which can be used to add new file systems. The availability of more than a dozen supported file systems shows clearly that this interface was a good design decision by the Linux developers, because no other operating system provides such a large supply of supported file systems The Linux network architecture also includes many interfaces supporting the dynamic enhancement of the wealth of protocols and network drivers.

The components shown on dark background in Figure 2–1 provide interfaces for the dynamic registration of new functionalities, so that such functionalities can be easily implemented in modules.

## 2.1 MONOLITHIC ARCHITECTURES AND MICROKERNELS

In contrast to current operating-system developments tending toward a microkernel architecture, the Linux operating system is based on a monolithic kernel. In microkernel architectures, such as the Mach kernel [Tan5] or the Windows NT kernel, the operating system kernel represents merely the absolute minimum of functionality. Good examples are interprocess communication (IPC) and memory management (MM). Building on the microkernel, the remaining functionality of the operating system is moved to independent processes or threads, running outside the operating system kernel. They use a defined interface to communicate with the microkernel.

In monolithic kernels, to which the Linux kernel belong, the entire functionality is concentrated in one (large) kernel. In addition to the basic mechanisms known from microkernels, the Linux system kernel also device drivers, file system drivers, most instances of the network protocols, and much more.(See Figure 2–1.) Compared to microkernel architectures, the use of monolithic kernel has both benefits and drawbacks, as we will see below.

The benefits include that the entire functionality of the operating system is concentrated in the kernel, allowing the system to work efficiently. You can access resources directly within the kernel, so costly system calls and context changes are needed less frequently. One major drawback is the source code for the operating system kernel can quickly become complex, even messy, because no interfaces are required within the kernel. In addition, the development of new drivers can be made more difficult by the lack of interface definition. For example, if you install a new device, you have to retranslate the entire kernel to ensure that device driver can be compiled with the kernel, a need avoided by microkernel architectures.

That Linux based on a monolithic operating-system kernel is due to historical reasons. A system that had not been planned to become such a big project, at the beginning, has continually developed further, so that it became impossible, at some point in time, to migrate to a microkernel architecture. However, since Version 2.0, Linux has made a step towards microkernel architectures. More specifically, the possibility was created of moving certain functionalities into modules, which are loaded into the kernel at runtime, from which they can be removed.

This removed an important drawback of monolithic kernels and opened the wat to loading drivers or other functionalities at runtime. In addition, modularization offers another benefit: Uniform interfaces are defined. This feature has been characteristic only of microkernel architectures. Linux has a number of interfaces, allowing the kernel to be dynamically enhanced by a number of functionalities. This very flexibility and openness of its interfaces is one of the most important benefits of Linux.
