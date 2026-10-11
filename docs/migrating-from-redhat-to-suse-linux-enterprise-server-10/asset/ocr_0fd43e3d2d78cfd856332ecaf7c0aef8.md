Linux boot managers can be used to load Linux or other operating systems, such as Microsoft Windows.

GRUB is designed with the following 2-stage architecture:

+   *   **Stage 1.** The first stage of a boot loader is usually installed in the master boot record (MBR) of the hard disk (first stage boot loader).
+   
+       As the space in the MBR is limited to 446 bytes, this program code merely contains the information for loading the next stage.
+   
+       Stage 1 can be installed in the MBR, in the boot sectors of partitions, or on a floppy disk.

+   *   **Stage 2.** This stage usually contains the actual boot loader. The files of the second stage boot loader are located in the directory /boot/.

# ### Boot Managers in SUSE Linux

SUSE Linux Enterprise Server provides 2 boot managers for the Linux environment: GRUB (GRAnd Unified Bootloader) and LILO (LIinux LOader).

To gain a better understanding of these boot managers, you need to know the following:

+   *   GRUB Boot Manager
+   *   LILO Boot Manager
+   *   Map Files, GRUB, and LILO