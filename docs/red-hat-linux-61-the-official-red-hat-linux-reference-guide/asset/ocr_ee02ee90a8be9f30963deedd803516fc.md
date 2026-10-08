# Chapter 2.
Boot Loaders

Before Red Hat Linux can run, it must be loaded into memory by a special program called a boot loader. A boot loader usually exists on the system's primary hard drive (or other media device) and has the sole responsibility of loading the Linux kernel with its required files or (in some cases) other operating systems into memory.

# 2.1. Boot Loaders and System Architecture

Each architecture capable of running Red Hat Linux uses a different boot loader. For example, the Alpha architecture uses the aboot boot loader, while the Titanium architecture uses the ELILO boot loader.

This chapter discusses commands and configuration options for the two boot loaders supplied by Red Hat Linux for the x86 architecture: GRUB and LILO.

# 2.2. GRUB

GNU GRand Unified Boot loader or GRUB is a program which enables the user to select which installed operating system or kernel to load at system time. It also allows the user to pass arguments to the kernel.

# 2.2.1. GRUB and the x86 Boot Process

This section discusses in more detail the specific role GRUB plays when booting an x86 system. For an look at the overall boot process, see Section 1.2 A Detailed Look at the Boot Process.

GRUB loads itself into memory in the following stages:

+   The Stage 1 or primary boot loader is read into memory by the BIOS by the MBR. The primary boot loader exists on less than 512 bytes of disk space within the MBR and is capable of loading either the Stage 1.5 or Stage 2 boot loader.
The Stage 1.5 boot loader is read into memory by the Stage 1 boot loader, if necessary. Some hardware requires an intermediate step to get to the Stage 2 boot loader. It is sometimes when the /boot partition is above the 1024 cylinder head of the hard drive or using LBA mode. The Stage 1.5 boot loader is found either on the /boot partition or on a small part of the MBR and the /boot partition.
The Stage 2 secondary boot loader is read into memory. The secondary loader displays the GRUB menu and command environment. This interface allows you to select which operating system or Linux kernel to boot, pass arguments to the kernel, or look at system parameters, as available RAM.
The secondary 2 boot loader reads the operating system and kernel and initrd into memory. GRUB determines which operating system to start, it loads it into memory and transfers control of the machine to that operating system.

The boot method used to boot Red Hat Linux is called the direct loading method the boot loader loads the operating system directly. There is no intermediary between the boot loader and the kernel.

+   For more on the system BIOS and the MBR, see Section 1.2.1 The BIOS.