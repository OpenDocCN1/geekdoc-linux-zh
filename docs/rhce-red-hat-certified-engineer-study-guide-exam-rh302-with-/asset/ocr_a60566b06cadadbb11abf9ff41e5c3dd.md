![](bbox=[0.156, 0.116, 0.353, 0.313])

he principal component of Red Hat Linux is the Linux kernel. This chapter explains basic kernel concepts, such as monolithic and loadable kernels. It also explains the basic commands for working with loadable modules and identifies and describes the packages and tools needed to rebuild the Linux kernel. This chapter is intended to be in conjunction with the following chapter, which explains how to rebuild the Linux kernel.

# Kernel Basics

The Linux operating system takes its name from its kernel, the Linux kernel. The kernel is the most basic component of an operating system. Much of a typical kernel is resident in memory at all times, whereas other operating systems are loaded when and then discarded. The kernel manages system resources such as the processor, memory, and devices and provides services used by other components of the operating system.

Unlike of most commercial operating systems, the Linux kernel is distributed in source form. This lets system administrators compile kernels that closely match the unique requirements of hosts. Being able to build a custom kernel offers the promise of improved system efficiency and performance, but the system administrator must understand the Linux kernel if these advantages are to be realized.

This section explains fundamental kernel concepts, including:

+   * Kernel versions and version numbers
* Kernel types (monolithic and modular)