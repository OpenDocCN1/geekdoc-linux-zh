You need to do two things before using LOADLIN.EXE:

+   1. Copy LOADLIN.EXE to a DOS partition (for example, C:\LOADLIN).
+   2. Put a copy of your kernel image (/vmlinuz) on your DOS partition.

For example, type the following from the DOS command line to boot Linux:

`loadlin c:\vmlinuz root=/dev/hda3 ro`

Make sure you insert your root partition in the command line. The ro stands for read-only. When you are first booting a Linux partition, it should be mounted as read-only to prevent data loss.

If you have a UMSDOS file system, you can type this:

`loadlin c:\vmlinuz root=/dev/hda1 rw`

The rw stands for read/write. Starting a UMSDOS file system this way is safe. Again, make sure you substitute your own partition. LOADLIN.EXE accepts a number of options: see its documentation in the LOADLIN.TGZ file under the dosutils directory on the first CD-ROM.

![](bbox=[0.08, 0.52, 0.94, 0.76])

# ## Installing and Using BootMagic

BootMagic is a commercial bootloader included with PowerQuest's PartitionMagic program. This bootloader must be installed using Windows, and may be installed and configured after you've installed Linux in a separate partition. If your computer does not have a CD-ROM drive, you'll have to use another computer to copy the BTMAGIC directory from the PartitionMagic CD-ROM onto a floppy and then onto your Windows desktop. You can then click the Setup.exe program to install BootMagic. You'll see a dialog, as shown in Figure 3.1.