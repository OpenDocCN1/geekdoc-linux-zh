# redhat Chapter 1.

# # Boot Process, Init, and Shutdown

An important and powerful aspect of Red Hat Linux is the open, user-configurable method it uses for starting the operating system. Users are free to configure many aspects of the boot process, including specifying the programs launched at boot-time. Similarly, system shutdown gracefully terminates processes in an organized and configurable way, although customization of this process is rarely required.

Understanding how the boot and shutdown processes work not only allows customization of Red Hat Linux, but also makes it easier to troubleshoot problems related to starting or shutting down the system.

# ## 1.1. The Boot Process

Below are the basic stages of the boot process for an x86 system:

+   1. The system BIOS checks the system and launches the first stage boot loader on the MBR of the primary hard disk.
2. The first stage boot loader loads itself into memory and launches the second stage boot loader from /boot/ partition.
3. The second stage boot loader loads the kernel into memory, which in turn allows necessary modules and mounts the partition read-only.
4. The kernel transfers control of the boot process to the /sbin/init program.
5. The /sbin/init program loads all services and user-space tools, and mounts partitions listed in /etc/fstab.
6. The user is presented with a login prompt for the freshly booted Linux system.

Because configuration of the boot process is more common than the customization of the shutdown process, the remainder of this chapter detail how the boot process works and how it can be customized to suit specific needs.

# ## 1.2. A Detailed Look at the Boot Process

The beginning of the boot process varies depending on the hardware platform being used. However, once the kernel is found and loaded by the boot loader, the default boot process is identical across all architectures. This chapter focuses on the x86 architecture.

# ### 1.2.1. The BIOS

When an x86 computer is booted, the processor looks at the end of memory for the Basic Input/Output System or BIOS and runs it. The BIOS controls not only the first step of the boot process, but also provides the lowest level interface to peripheral devices. For this reason it is written into read-only, permanent memory and is always available for use.

Other platforms use firmware to perform low-level tasks roughly equivalent to those of the BIOS on an x86 system. For instance, Itanium-based computers use the Extensible Firmware Interface (EFI) Shell, while Alpha systems use the SRM console.

Once loaded, the BIOS tests the system, looks for peripherals, and then finds a local device with which boot the system. Usually, it checks diskette drives and CD-ROM drives present for bootable media, then, failing that, looks to the system's hard drives. In most cases, the