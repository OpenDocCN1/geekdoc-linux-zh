![](bbox=[0.08, 0.49, 0.35, 0.78])

**Fig. 1.13 The opening X Windows screen in Caldera Open Linux 1.3**

distributions now include KDE and to follow much of the material in this book you must have KDE installed. Note that with some systems the \"startx\" command will actually run KDE. Once back at the Linux command prompt and assuming KDE is installed, it can be run using this command:

```
Kde
```

When KDE has loaded the screen should look something like Figure 1.14, but the exact appearance depends on the version in use and the default settings. Using KDE is covered in chapters 3 and 4, and it will not be considered further here. However, by exploring the menu system you should have no difficulty in running a few programs such as some of the games.

# **Dual booting**

As pointed out previously, Linux can be used in dual boot systems where we have the choice of booting into Linux or another operating system such as Windows 98. The installation process is similar. With the dual boot approach, but at the hard disc partitioning stage there will already be one or more partitions on the disc, which are the ones used by the existing operating system. The \"p\" option of Fdisk can be used to show the existing partitions. Before you start to allocate the free space to the Linux partitions. These are partitions are produced using the same basic procedure that is used for a normal Linux installation, but the partition numbers will be higher due to the existing partitions. If there are already two primary partitions on the disc, the main Linux and Linux swap partitions would be partitions three and four. Remember that no more than four primary partitions can be accommodated. One partition will already be the bootable partition, and this will normally be left as the boot partition.

There is not usually any major problem in getting a PC to dual boot, but it is wise to avoid booting straight into one or other of the operating systems on the basis of having Lilo installed on a floppy disc rather than on the hard disc. With this disc not in the drive at boot-up the computer will boot into the other operating system in the normal fashion. If the disc is in the drive, Lilo runs and boots Linux. It may appear as though Linux is booting from the floppy disc, but strictly speaking it is booting from the hard disc. Lilo points the boot-up process in the right direction, and from

![](bbox=[0.08, 0.07, 0.35, 0.36])

**Fig. 1.14 The opening screen in KDE 1.0**