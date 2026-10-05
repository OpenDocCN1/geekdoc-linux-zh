
# What is a Distribution?

![](img/23b949da14ff7bab8762f0f0361af394_138_0.png)

Figure 5-1 Distribution contents

Most of the latest Linux distributions offer the following:

- Full 32-bit and 64-bit architectures
- Preemptive multitasking
- Support for multiple users and groups
- Full networking capabilities
- Protected memory
- Clustering, including load balancing and failover
- Dynamic reconfiguration
- SMP support

## 5.1.2 Standards

A lot of effort has been put into standardizing Linux and higher-level subsystems. Organizations such as the Free freedesktop.org, and the Open Source Development Labs (OSDL) started working on many different projects in this area. These projects use and extend existing standards such as POSIX, the Single UNIX Specification, XML, DOM, CORBA, and many more. Some example projects are:

- Filesystem Hierarchy Standard
- Linux Standard Base at http://www.linuxbase.org
- Internationalization (i18N)
- Printing (OpenPrinting)
- Accessibility
- Clustering (Open Cluster Framework)
- Data Center Linux
- Carrier Grade Linux

> Note: The LSB 3.1 specification has been approved and published. "Desktop Linux futures" on page 7.

Most of these standardization efforts were focused on low-level functionality and standardization of the file layout, a new printing architecture, stabilization or creation of APIs for clustering and high availability, and to make sure that programs from independent software vendors (ISVs) are binary compatible between Linux distributions.

From a standardization point of view, the Linux desktop is currently a fast moving target. A lot of promising development is currently underway that will evolve the Linux landscape even further. For example:

- New X server extensions and modularity
- Cairo (vector graphics system)
  - With X, OpenGL, and Postscript or PDF output
- HAL (hardware abstraction layer)
- Gstreamer (streaming media framework)
- D-BUS (message bus system)

## 5.2 Technical differences

This section introduces and discusses many of the technical differences between the architecture of Windows and Linux clients.

Linux has innovations in technology and features that are not available on Windows. Linux is also highly modular and extremely configurable. And certain features have been implemented differently than they are implemented in the Windows operating system.

A Linux operating system consists of the kernel and several crucial components. Some of the terms used in this chapter might be new to someone coming from a Windows environment. For more information about these terms, refer to Appendix A, "Linux glossary for Windows users" on page 233.

The Linux operating system contains the following components (as shown in Figure 5-2 on page 114):

### Linux kernel

- Provides a set of services or kernel features to applications allowing them to run. Device drivers and modules can be added to the kernel to expand these services. The kernel also supports concepts such as multitasking and a multi-user environment.

### Devices

A device is an entity within the operating system that forms the interface to hardware. The device driver handles translation of operations on the device in the operating system to physical actions in the hardware.

### Modules

A module is dynamically loadable or unloadable kernel code that provides a service, such as a device driver. Modules provide the ability for the kernel to interface with hardware, making the hardware functionality available for use by the kernel or user space applications. Once a module is loaded into the kernel, it is considered part of the kernel, but it can be unloaded when not needed.

### Application level (user space)

Environment where applications that make use of the kernel services run. This environment or user space can be a graphical or a command line-based user interface. An application has access to the kernel services through invocation of system calls.

### The Linux kernel

User Programs and Applications

| System calls | | | | Application Level |
| :--- | :--- | :--- | :--- | :--- |
| Process Management | Memory Management | Filesystems | Device Control | Networking | Kernel Level |
| Concurrency Multitasking | Virtual Memory | Files & Directories | Device Access | Connectivity | Kernel features |
| Architecture dependent Code | Memory Manager | | Character Devices | Network Subsystem | Software support |
| | | Block Devices | | | Hardware control |

![](img/23b949da14ff7bab8762f0f0361af394_141_0.png)

Figure 5-2 Linux Operating System

## 5.2.1 Kernel booting process

One of the biggest differences when migrating to Linux is its stability. It is conceivably possible to never need a reboot, unless the kernel needs upgrading. However, when it is time to boot, the process is somewhat different that it is in Windows. The initial kernel booting process is also referred to as kernel bootstrap.

### Kernel bootstrap process

The kernel bootstrap process is:

1. Processor initialization, only low memory addressed, BIOS starts boot (GRUB, LILO).
2. Bootloader loads initrd and kernel into memory; bImage unzips itself to high memory (/boot).
3. Bootloader starts kernel, and bootloader tells kernel that there is an initrd.
4. Kernel unzips initrd and mounts it as root-filesystem.
5. Within initrd, a program called linuxrc is executed. The linuxrc program loads the modules necessary to mount various physical filesystem devices.
6. The real root filesystem is mounted; initrd is remounted to /initrd.
7. The init process starts (pid 1).

In the previous description, initrd indicates a file that is started by the kernel. every other process is a child of init.

## 5.2.2 Communication, files, and services

Communication in Linux is performed using sockets. A socket is a file that can be read or written to. This then corresponds to a receive of a send operation on the device. A network connection between two systems, for example, is built from two sockets on both ends, corresponding to an IP address and a port number.

Devices in Linux are also represented by files, usually in the /dev directory. Writing to the file corresponds to writing to the hardware.

As mentioned in 5.1.2, "Standards" on page 111, the Filesystem Hierarchy (FHS) governs the Linux filesystem. Filesystems in most Linux distributions are set up along the lines of the Filesystem Standard (Table 5-1 on page 116).

### Table 5-1 Filesystem Hierarchy Standard

| Directory | Description | Remarks |
| :--- | :--- | :--- |
| / | Root of the filesystem | All other files and filesystems are sub-directories of this. |
| /bin | Essential command binaries | Commands such as ls |
| /boot | Static files of the boot loader | Sometimes be own filesystem |
| /dev | System configuration | Contents differ for each distribution. |
| /lib | Shared libraries and kernel modules | |
| /media | Mountpoint for removable media | Used to be part of /mnt. |
| /mnt | Mountpoint for temporary mounts of filesystems | |
| /opt | Add-on application software | |
| /sbin | Essential system binaries | |
| /srv | Data for services | |
| /tmp | Temporary files | |
| /usr | Secondary hierarchy | Contains an entire subtree governed by FHS. |
| /var | Variable data | Logging, PIDs, caches, and so on. |

A more detailed description of the FHS can be found at:

http://www.pathname.com/fhs

A big difference between the Windows OS is that the concept of driveletters does not exist within Linux. This is an important difference when discussing desktops, because users are used to use this concept of the driveletter (C: containing the Windows OS and Program Files, D: usually containing data, E: being the CD-ROM, and so forth)
