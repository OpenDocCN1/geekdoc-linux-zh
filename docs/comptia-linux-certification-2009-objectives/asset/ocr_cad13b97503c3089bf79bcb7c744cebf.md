# TOPIC A

# Explore the Linux Kernel

The first component that initializes in the Linux boot process is the kernel. It provides all the essential services that are required for running the computer, and controls the rest of the processes that happen on the computer. In this topic, you will identify the role of the Linux kernel and its functions.

If a system crashes or stops performing, it actually means that the kernel or an operation critical to the working of the kernel has crashed. As a Linux+ administrator, you need to understand the functionality of the kernel to be able to troubleshoot and provide solutions.

# The Kernel

**Definition:**

The kernel is the core of an operating system on which all other components rely. It is loaded first and remains in the main memory. It contains the system-level commands and other functions that are hidden from users. The kernel manages filesystem access, memory, processes, devices, and resource allocation in a system. The kernel also controls all the hardware devices plugged into the system.

![](bbox=[0.77, 0.34, 0.84, 0.375])

The Kernel

**Example:**

![](bbox=[0.24, 0.48, 0.48, 0.67])

*Figure 8-1: The kernel’s role in an operating system.*

# The Linux Kernel

The Linux kernel, which is the core constituent of the Linux operating system, manages all other resources on the system. It performs functions such as sharing resources and allocating of memory, input and output operations, security settings, and user access. It controls the interaction between software applications and underlying system resources. The kernel initializes itself during the boot process and then starts running the other processes. By default, the kernel loads with a minimal set of functions required to run a system. The kernel’s functionality can be expanded by installing kernel modules. The kernel is required to synchronize the operations of multiple processes and govern resources.

![](bbox=[0.77, 0.77, 0.84, 0.805])

The Linux Kernel