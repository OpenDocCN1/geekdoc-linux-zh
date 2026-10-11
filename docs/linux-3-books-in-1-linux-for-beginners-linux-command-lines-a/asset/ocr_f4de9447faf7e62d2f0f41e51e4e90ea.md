Since there is sufficient space to store the code for GRUB2 stage 1.5, which does not need a lot of space, the additional space is used to contain file system drivers such as FAT, EXT, and NTFS. This means that a standard EXT file system is enough to store the code for GRUB2 stage 2. The location for the GRUB2 stage 2 code is at /boot/grub2.

# ## Stage 2

All the files that are needed to execute stage 2 of GRUB2 are located at /boot/grub2 and its subdirectories. Stage 2 of GRUB2 does not have any image files like it did in stage 1 and 1.5. Instead, it loads runtime modules when needed from the directory at /boot/grub2/i386-pc.

The main objective of GRUB2 stage 2 is to find the Linux kernel and load it into memory so that the control can be passed to the kernel. The Linux kernel files are stored in the /boot directory. One can identify Linux kernel files easily since they are all prefixed with **vmlinuz**. You can list down all the kernel files for your Linux system by simply listing down the /boot directory contents.

So when your system boots up, you get a screen where all the kernels available on your Linux system are listed, and you can select one of them to pass the control to the respective kernel.

# ## Kernel

All the kernels available today are stored in a compressed format for space optimization, but they can self-extract themselves. We know that the Linux kernel can be located in the /boot directory. When you select a particular kernel on the boot menu, it gets executed and starts extracting itself so that the system can use the files. When the kernel is executed, it makes a call to **systemd** and eventually passes the control to systemd.

This is the end of the Linux boot process. At this point in time, both the bootloader and systemd are in a running state but are not useful to the end-user since nothing else is running yet.

# ## The Startup Sequence

The Linux startup sequence is initiated after the boot sequence concludes.