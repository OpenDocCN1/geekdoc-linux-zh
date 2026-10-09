Installing the kernel in this manner updates the **grub.cfg** GRUB configuration file to include the new kernel. The GRUB boot loader is covered below.

# # REBOOTING

Reboot the system by selecting **Main menu: System⏥Quit** and then clicking **Restart**. If you are working at the console, press **CONTROL-ALT-DEL**. You can also give a reboot command from the console, a character-based terminal, or a terminal emulator.

# # GRUB: THE LINUX BOOT LOADER

+   * MBR	A boot loader is a very small program that the *bootstrap* (page 1138) process uses as it brings a computer from off or reset to a fully functional state. The boot loader frequently resides on the starting sectors of a hard disk called the master boot record (MBR).

+   * BIOS	The *BIOS* (page 1137), which is stored in an *EEPROM* (page 1147) on the system's motherboard, gains control of a system when you turn on or reset the computer. After testing the hardware, the BIOS transfers control to the MBR, which usually passes control to the partition boot record. This transfer of control starts the boot loader, which is responsible for locating the operating system kernel (kept in the /*boot* directory), loading that kernel into memory, and starting it running. The /*boot* directory, which may be mounted on a separate partition, must be present for the system to boot *Linux*. Refer to “Boot ing the System” on page 444 for more information on what happens from this point forward.

+   * LBA addressing mode and the /*boot* partition	All newer hard disks support LBA (logical block addressing) mode. LBA permits the /*boot* directory to appear anywhere on the hard disk. For LBA to work, it must be supported by the hard disk, the BIOS, and the operating system (GRUB in the case of *Linux*). Although both GRUB 2 and GRUB legacy support LBA addressing mode, some BIOSes do not. For this reason, it is a good idea place the /*boot* directory in its own partition located near the beginning of the hard disk. With this setup, the root (/) filesystem can be anywhere on any hard drive that *Linux* can access regardless of LBA support. Also, systems with LVM require a separate boot partition. In some instances, without a separate /*boot* partition, the system may boot at first, but then fail as you update the kernel and the kernel files move further from the beginning of the disk.

+   * GRUB 2	GRUB stands for Grand Unified Boot loader. With release 9.10 (Karmic Koala), Ubuntu introduced GRUB 2, which this book refers to simply as GRUB. This book refers to the first release as GRUB legacy. GRUB 2 is a complete rewrite of GRUB legacy; few of the configuration files are the same.