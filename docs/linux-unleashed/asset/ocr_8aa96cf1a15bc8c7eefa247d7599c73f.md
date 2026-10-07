cases, the advice makes a lot of sense (such as resolving IRQ conflicts), in which case you should take care of the issue. (There's a table of commonly used IRQs later in this chapter.)

# # Boot and Root Disks

Even if you are installing from CD-ROM, you still need two high-capacity floppies (either 1.2MB or 1.44MB). These are the boot and root floppies. The boot floppy holds the kernel that is used to start Linux the first time, leading to your installation. The root floppy holds a small filesystem that includes utilities needed for the installation. The two disks together form a complete and very small implementation of Linux. There is enough of a system on the two floppies to actually play with Linux, although many of the utilities are missing.

# TIP

If you have a recent system, you may not need boot and root floppies at all. Current BIOS versions allow booting from the CD-ROM drive, especially when the system is all SCSI-based. Some IDE-based CD-ROM systems allow booting from the CD-ROM drive, too. If your system supports CD-ROM booting, you need only insert the Linux CD and reboot the system. The CD software automatically selects the correct boot and root images to use.

In most cases, the boot and root floppies are copied from existing files that are called “images.” The image is a recompiled version of the system that you duplicate onto the floppies, eliminating the need to start from scratch. CD-ROM and FTP distributions have directories for several boot and root images, depending on the hardware on your system. You must select the image that matches your hardware as much as possible, copy them to the disks, and start your system with the disks.

You can do most of these steps from DOS, although you can't use the DOS copy command to create the boot and root floppies. The floppies must be created with a utility that ignores the DOS formatting. This utility, commonly called RAWRITE.EXE, is included with most Linux software distributions.

# ## Selecting a Boot Kernel and Root Image

CD-ROMs usually have directories under the root directory called bootdisks.144 and rootdisks.144 (for 3.5-inch 1.44MB floppies) and bootdisks.12 and rootdisks.12 (for 5.25-inch 1.2MB floppies) that contain the boot and root images, respectively. You