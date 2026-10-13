+   - Before you do anything to your computer, back up all your data. There's nothing more upsetting than deleting the Web site you just created and haven't yet uploaded to the Web server.
+   - If you intend to partition the hard drive, run a disk defragmenter program. The disk needs to be cleaned up before a partition utility can split the drive into two or more pieces.

# Task: Creating an Installation Boot Disk

One of the advantages of purchasing Linux in a boxed set is that the boxed set usually includes a boot disk and any other floppy disks you might need. If you have only the installation CD for your Linux distribution and your computer boots from the floppy drive, you will need to create an installation boot disk.

**New Term**
Computers boot from different places, depending on the BIOS settings. Some computers attempt to start the system by locating startup instructions from the floppy drive before looking to the hard drive. Other computers look to the CD-ROM first. If your computer boots from the CD-ROM, you're in great shape—just put the CD-ROM into the CD drive when you are ready to start installing Linux. If your computer boots from the floppy drive, you will need a boot disk that starts the installation program on the CD-ROM.

![](bbox=[0.2, 0.68, 0.3, 0.78])

> Some Linux distributions require that you create other floppy disks. TurboLinux needs an Extra Hardware disk, which it uses during the installation to help configure the computer hardware. Slackware and Red Hat also use a rescue disk, which comes in handy when the system isn't working properly. Debian can be converted to use floppies to install the system.

To create an installation boot disk, you will need the distribution CD-ROM, a blank 3.5-inch disk, the rawrite program, and the user documentation for rawrite. To use the rawrite program in MS-DOS, follow these steps:

+   1. Display the MS-DOS prompt in Microsoft Windows. Select Start, Programs, MS-DOS Prompt.
+   2. Change to the CD-ROM drive. Type D: and press Enter (where D: is the drive letter for your CD-ROM drive).
+   3. Change to the directory where the rawrite program is located on the CD-ROM. Linux-Mandrake, Red Hat, and TurboLinux store rawrite in the \dosutils directory (type cd dosutils and press Enter). In Slackware, rawrite is in the \install directory. An example is shown in Figure 1.5.