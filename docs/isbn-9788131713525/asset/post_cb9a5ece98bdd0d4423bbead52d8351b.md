
## 7.6.1 Suggestions for Additional Reading

*   This chapter examined the role of the bootloader and discovered the limited execution context in which a bootloader must exist.
*   Das U-Boot has become a popular universal bootloader for many processor architectures. It supports a large number of processors, reference hardware platforms, and custom boards.
*   U-Boot is configured using a series of configuration variables in a board-specific header file. Appendix B contains a list of all the standard U-Boot command sets supported in a recent U-Boot release.
*   Porting U-Boot to a new board based on a supported processor is relatively straightforward. In this chapter, we walked through the steps of a typical port to a board with similar support in U-Boot.
*   There is no substitute for detailed knowledge of your processor and hardware platform when bootloader modification or porting must be accomplished.
*   We briefly introduced additional bootloaders in use today so you can make an informed choice for your particular requirements.

### References

*   *Application Note: Introduction to Synchronous DRAM*  
    Maxwell Technologies  
    www.maxwell.com/pdf/me/app_notes/Intro_to_SDRAM.pdf
*   *Using ld, the GNU linker*  
    Free Software Foundation  
    www.gnu.org/software/binutils/manual/ld-2.9.1/ld.html
*   *The DENX U-Boot and Linux Guide (DULG) for TQM8xxL*  
    Wolfgang Denx et al., Denx Software Engineering  
    www.denx.de/twiki/bin/view/DULG/Manual
*   RFC 793, "Trivial File Transfer Protocol"  
    The Internet Engineering Task Force  
    www.ietf.org/rfc/rfc793.txt
*   RFC 951, “Bootstrap Protocol”  
    The Internet Engineering Task Force  
    www.ietf.org/rfc/rfc951.txt
*   RFC 1531, “Dynamic Host Control Protocol”  
    The Internet Engineering Task Force  
    www.ietf.org/rfc/rfc1531.txt
*   PowerPC 405GP Embedded Processor user’s manual  
    International Business Machines, Inc.
*   Programming Environments Manual for 32-bit Implementations of the PowerPC Architecture  
    Freescale Semiconductor, Inc.
*   Lilo Bootloader  
    www.tldp.org/HOWTO/LILO.html
*   GRUB Bootloader  
    www.gnu.org/software/grub/

# Chapter 8

![](img/7a1144833e62564667e7dd9eb4c9f03d_220_0.png)

**In this chapter**

*   Device Driver Concepts page 190
*   Module Utilities page 199
*   Driver Methods page 205
*   Bringing It All Together page 209
*   Device Drivers and the GPL page 211
*   Chapter Summary page 211

One of the more challenging aspects of system design is partitioning functionality in a rational manner. The familiar device driver model found in UNIX and Linux provides a natural partitioning of functionality between your application code and hardware or kernel devices. In this chapter, we develop an understanding of this model and the basics of Linux device driver architecture. After reading this chapter, you will have a solid foundation for continuing your study of device drivers using one of the excellent texts listed at the end of this chapter.

This chapter begins by presenting Linux device driver concepts and the build system for drivers within the kernel source tree. We examine the Linux device driver architecture and present a simple working example driver. We introduce the user space utilities for loading and unloading kernel modules.¹ We present a simple application to illustrate the interface between applications and device drivers. We conclude this chapter with a discussion of device drivers and the GNU Public License.

### 8.1 Device Driver Concepts

Many experienced embedded developers struggle at first with the concepts of device drivers in a virtual memory operating system. This is because many popular legacy real-time operating systems do not have a similar architecture. The introduction of virtual memory and kernel space versus user space frequently introduces complexity that is not familiar to experienced embedded developers.

One of the fundamental purposes of a device driver is to isolate the user's programs from ready access to critical kernel data structures and hardware devices. Furthermore, a well-written device driver hides the complexity and variability of the hardware device from the user. For example, a program that wants to write data to the hard disk need not care if the disk drive uses 512-byte or 1024-byte sectors. The user simply opens a file and issues a write command. The device driver handles the details and isolates the user from the complexities and perils of hardware device programming. The device driver provides a consistent user interface to a large variety of hardware devices. It provides the basis for the familiar UNIX/Linux convention that everything must be represented as a file.

> ¹ The terms module and device driver are used here interchangeably.

#### 8.1.1 Loadable Modules

Unlike some other operating systems, Linux has the capability to add and remove kernel components at runtime. Linux is structured as a monolithic kernel with a well-defined interface for adding and removing device driver modules dynamically after boot time. This feature not only adds flexibility to the user, but it has proven invaluable to the device driver development effort. Assuming that your device driver is reasonably well behaved, you can insert and remove the device driver from a running kernel at will during the development cycle instead of rebooting the kernel every time a change occurs.

Loadable modules have particular importance to embedded systems. Loadable modules enhance field upgrade capabilities; the module itself can be updated in a live system without the need for a reboot. Modules can be stored on media other than the root (boot) device, which can be space constrained.

Of course, device drivers can also be statically compiled into the kernel, and, for many drivers, this is completely appropriate. Consider, for example, a kernel configured to mount a root file system from a network-attached NFS server. In this scenario, you configure the network-related drivers (TCP/IP and the network interface card driver) to be compiled into the main kernel image so they are available during boot for mounting the remote root file system. You can use the initial ramdisk functionality as described in Chapter 6, “System Initialization,” as an alternative to having these drivers compiled statically as part of the kernel proper. In this case, the necessary modules and a script to load them would be included in the initial ramdisk image.

Loadable modules are installed after the kernel has booted. Startup scripts can load device driver modules, and modules can also be “demand loaded” when needed. The kernel has the capability to request a module when a service is requested that requires a particular module.

Terminology has never been standardized when discussing kernel modules. Many terms have been and continue to be used interchangeably when discussing loadable kernel modules. Throughout this and later chapters, the terms *device driver*, *loadable kernel module (LKM)*, *loadable module*, and *module* are all used to describe a loadable kernel device driver module.

#### 8.1.2 Device Driver Architecture

The basic Linux device driver model is familiar to UNIX/Linux system developers. Although the device driver model continues to evolve, some fundamental structures have remained nearly constant over the course of UNIX/Linux evolution. Device drivers are broadly classified into two basic categories: *character devices* and *block devices*. Character devices can be thought of as serial streams of sequential data. Examples of character devices include serial ports and keyboards. Block devices are characterized by the capability to read and write blocks of data to and from random locations on an addressable medium. Examples of block devices include hard drives and floppy disk drives.

#### 8.1.3 Minimal Device Driver Example

Because Linux supports loadable device drivers, it is relatively easy to demonstrate a simple device driver skeleton. Listing 8-1 illustrates a loadable device driver module that contains the bare minimum structure to be loaded and unloaded by a running kernel.

**Listing 8-1: Minimal Device Driver**

```c
/* Example Minimal Character Device Driver */
#include <linux/module.h>

static int __init hello_init(void)
{
    printk("Hello Example Init\n");
    return 0;
}

static void __exit hello_exit(void)
{
    printk("Hello Example Exit\n");
}

module_init(hello_init);
module_exit(hello_exit);

MODULE_AUTHOR("Chris Hallinan");
MODULE_DESCRIPTION("Hello World Example");
MODULE_LICENSE("GPL");
```
