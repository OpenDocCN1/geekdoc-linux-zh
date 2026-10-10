![](bbox=[0.26, 0.11, 0.86, 0.47])

**Figure 3-1** A default GRUB menu from CentOS

# The Kernel and Initrd

Once you select a particular kernel in GRUB (or the countdown times out and it picks one for you), GRUB will load the Linux kernel into RAM, execute it, and pass along any boot-time arguments that were configured for it. Usually GRUB will also load an initrd (initial RAM disk) along with the kernel. This file, on a modern Linux system, is a gzipped cpio archive known as an initramfs file, and it contains a basic, small Linux root file system. On that file system are some crucial configuration files, kernel modules, and programs that the kernel needs in order to find and mount the real root file system.

In the old days all of this boot time capability would be built directly into the Linux kernel. However, as hardware support grew to include a number of different file systems and SCSI and IDE devices along with with extra features like software RAID, LVM, and file system encryption, the kernel got too large. Therefore, these features were split out into individual modules