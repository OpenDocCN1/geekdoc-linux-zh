2. **Option:** use LILO as the main boot manager on a primary partition on the first hard disk. This is a special case of the scenario in the following section, which also includes DOS. Using the MBR is not recommended, because, when repartitioning with another fdisk, the MBR is rewritten and LILO erased.

# DOS, OS/2, and Linux

If you have used the OS/2 boot manager for DOS and OS/2 and want to continue using it, simply add Linux to its start menu as described in the previous example.

Another possibility is to use LILO as the main boot manager on a primary partition of the first hard disk. The following complicated example of `lilo.conf` (File 7) assumes that the DOS boot partition (primary) and the Linux boot partition (also primary) are both on the first hard drive — within the 1024-cylinder limit of the two partitions. OS/2 is installed on a second hard disk. This is why a special loader (`/boot/os2_b.b`) is used in place of `/boot/chain.b`. It does not matter whether the MBR code is DOS or OS/2. The important thing is that the LILO boot partition (`/dev/sda4`) must be marked as active in the partition table with fdisk.