# 48 SYSTEM START-UP

A current development is the boot loader grub (Grand Unified Bootloader). This program is substantially more flexible than LILO and can boot many systems besides LINUX. The use of grub still requires changes to the kernel, but once these have been incorporated into the standard, this could become the boot loader of choice. At boot time, grub can read and boot arbitrary files from an Extended-2 file system, so it is much safer and more flexible than LILO.

# 3.2.1 The LINUX loader LILO

LILO by Werner Almesberger is the most widely used and flexible boot loader for LINUX. The abbreviation LILO stands for LINUX loader; LILO, however, load other operating systems too. Many LINUX users use LILO for the first time after the installation of a LINUX distribution, when they see the text LILO appear on the screen after a restart of the system. After pressing one of the keys Shift, Alt, or if either Shift or ScrollLock is activated, LILO shows a prompt for action by the user, that waits for the user to enter the name of a boot configuration to be loaded. By pressing Tab, a list of the available configurations is displayed on screen.

The LILO package consists of two interdependent parts. These parts are:

+   The program /sbin/lilo which must be called after modification to the kernel files (usually /boot/vmlinux) if LILO is used as the boot loader. This program determines the sector numbers in which the kernel image is stored and keeps this in the map file.
Various boot sectors which can start other operating systems (even from the second disk) or load a kernel image. Since these boot sectors have no information on the internal structure, the system, for example, of the Extended-2 file system, they need an up-to-date map file.
This is also the biggest disadvantage of LILO: after each modification to the kernel, the LILO program must be called to update the map file. In addition, the system administrator must ensure that a backup kernel is always available and linked into the LILO configuration. The function known from *BSD systems, to boot an arbitrary kernel from the file system, is unfortunately not available.
LILO can boot up to 16 different configurations and can be installed both in the MBR and the boot sector of primary partitions. LILO can
- serve as a boot sector on a LINUX floppy disk,
- function as the MBR on the first hard disk, and