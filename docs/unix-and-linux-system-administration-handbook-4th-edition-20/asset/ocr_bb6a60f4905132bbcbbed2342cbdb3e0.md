# Drivers device files

is running. The latter method is the most typical for USB devices: memory sticks, digital cameras, printers, and so on. Linux has reasonable support for a wide array of such devices. AIX and HP-UX have very limited support, and Solaris falls somewhere in between.

Table 13.1 shows the location of the kernel build directory and the standard of the installed kernel on each of our examples.

# Table 13.1 Kernel build directory and location by system

| System | Build directory | Kernel |
| --- | --- | --- |
| Linux | /usr/src/linux | /vmlinux or /boot/vmlinux |
| Solaris | ^a | /platform/hardware-class-name/unix |
| HP-UX | /standard | /stand/vmunix |
| AIX | | /usr/lib/boot/unix |

+   - a. Administrators rarely build Solaris kernels, and when they do, the administrator creates an arbitrary build directory.
- b. The AIX kernel is never reboot, even when new modules and devices are added.

# 13.2 DRIVERS AND DEVICE FILES

A device is a program that manages the system's interaction with a particular type of hardware. The driver translates between the hardware commands understood by the device and the stylized programming interface used by the kernel. The driver layer keeps the kernel reasonably device independent.

In most cases, device drivers are part of the kernel; they are not user processes. However, a driver can be accessed both within the kernel and from user. User-level access to devices is usually through special devices that live in the /dev directory. The kernel maps operations on these files calls into the code of the driver.

With the remarkable pace at which new hardware is developed, it is practically impossible to keep mainline OS distributions up to date with the latest hardware. Ergo, you will occasionally need to add a device driver to your system to support a new piece of hardware.

Device drivers are system specific, and they are often specific to a particular range of kernel revisions as well. Drivers for other operating systems (e.g., Windows) will not work, so keep in mind when you purchase new hardware.¹ In addition, devices vary in their degree of compatibility and functionality when used with various Linux distributions, so it's wise to pay some attention to the results other sites have obtained with any hardware you are considering.

+   1. The NDISwrapper project enables Windows drivers for some networking devices to be used by Linux. See sourceforge.net/projects/niswrapper for full details.

![](bbox=[0.953, 0.666, 0.995, 0.786])