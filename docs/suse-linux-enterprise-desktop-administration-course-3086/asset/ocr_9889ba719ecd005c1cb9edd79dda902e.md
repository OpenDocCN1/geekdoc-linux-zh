The following sections describe the process:

+   - BIOS and Boot Manager
+   - Kernel
+   - initramfs (Initial RAM File System)
+   - init

# BIOS and Boot Manager

The BIOS (Basic Input Output System) performs a power-on self test, conducts the initial detection and setup of hardware, and accesses bootable devices (such as a CD or hard drive). If the bootable device is a hard drive, BIOS also reads the MBR (Master Boot Record). Using the code in the MBR, the BIOS starts the boot manager.

The *boot manager* (such as GRUB) loads the kernel and the initrd to memory and starts the kernel.

# Kernel

The kernel (/boot/vmlinuz, which is a link to /boot/vmlinuz-kernelversion), uncompresses itself and then organizes and takes control of the continued booting of the system.

The kernel checks and sets the console (the BIOS registers the graphics cards and the screen output format), reads BIOS settings, and initializes basic hardware interfaces.

Next, the drivers, which are part of the kernel, probe existing hardware and initialize it accordingly.

The kernel controls the entire system, managing hardware access and allocating CPU time and memory to programs.

# initramfs (Initial RAM File System)

The Initial RAM File System (initramfs) is a cpio archive that the kernel can load to a RAM disk. It provides a minimal Linux environment that enables the execution of programs before the actual root file system is mounted. The initramfs must always provide an executable named init that should execute the actual init program on the root file system for the boot process to proceed.

Former SUSE Linux versions used an initial RAM disk, initrd, instead. Despite the fact that the format is now changed, the filename is still /boot/initrd; /boot/initrd is a link to /boot/initrd-kernelversion, the file that holds the gzipped cpio archive.

The kernel starts the program init contained in the initramfs. It is a shell script that, among other things, loads the kernel modules needed to mount the actual root file system, mounts the root file system, and then finally starts /sbin/init from the root file system.

To look at the script init in initramfs, unpack the cpio archive:

```
da10:~ # mkdir /tmp/initramfs
da10:~ # cd /tmp/initramfs/
da10:/tmp/initramfs # gunzip -c /boot/initrd-2.6.16.14-6-smp | cpio -i
12765 blocks
da10:/tmp/initramfs # ls
bin bootsplash dev etc init lib proc root sbin sys tmp
da10:/tmp/initramfs # less init
```