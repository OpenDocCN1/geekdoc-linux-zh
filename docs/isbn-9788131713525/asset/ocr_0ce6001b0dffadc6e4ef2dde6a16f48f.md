![](bbox=[0.08, 0.13, 0.73, 0.48])

FIGURE 6-1
Linux kernel configuration utility

# 6.4.1 Initial RAM Disk Purpose

The initial RAM disk is a small self-contained root file system that usually contains directives to load specific device drivers before the completion of the boot cycle. In Linux workstation distributions such as Red Hat and Fedora Core, an initial RAM disk is used to load the device drivers for the EXT3 file system before mounting the real root file system. An *initrd* is frequently used to load a device driver that is required in order to access the real root file system.

# 6.4.2 Booting with initrd

To use the *initrd* functionality, the bootloader gets involved on most architectures to pass the *initrd* image to the kernel. A common scenario is that the bootloader loads a compressed kernel image into memory and then loads an *initrd* image into another section of available memory. In doing so, it becomes the bootloader’s responsibility to pass the load address of the *initrd* image to the kernel before passing control to it. The exact mechanism differs depending on the architecture, bootloader, and platform implementation. However, the kernel must know where the *initrd* image is located so it can load it.