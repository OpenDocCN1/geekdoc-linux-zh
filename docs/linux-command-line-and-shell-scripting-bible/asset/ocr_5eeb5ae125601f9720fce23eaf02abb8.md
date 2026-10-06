The kernel is primarily responsible for four main functions:

+   * System memory management
* Software program management
* Hardware management
* Filesystem management

The following sections explain each of these functions in more detail.

# System memory management

One of the primary functions of the operating system kernel is memory management. Not only does the kernel manage the physical memory available on the server, it can also create and manage virtual memory, or memory that does not actually exist.

It does this by using space on the hard disk, called the swap space. The kernel swaps the contents of virtual memory locations back and forth from the swap space to the actual physical memory. This allows the system to think there is more memory available than what physically exists (shown in Figure 1-2).

FIGURE 1-2

The Linux system memory map

![](bbox=[0.137, 0.542, 0.684, 0.897])