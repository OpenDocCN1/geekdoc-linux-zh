Similar steps can be used to configure a partition or a component of a RAID array. It's also a flag; just substitute raid for lvm in response to the Flag to Invert prompt just shown. If you're following along with a RHEL 6 system, first confirm the result. Exit from parted, and run the following commands:

```
# parted /dev/sdb print
# fdisk -l /dev/sdb
```

You'll see the lvm flag as shown previously from the parted command; you'll see the following confirmation in the output to the fdisk command:

Device Boot Start End Blocks Id System
/dev/ada1 1 263 487424 fd Linux LVM

If you've set up the baseline virtual system described in Chapter 2, this is an excellent opportunity to set up partitions as components of LVM volumes. Now that you have the tools, it does not matter whether you use fdisk or parted for the purpose. You can choose to use all free space. Just be sure to create a partition on more than one hard disk for this purpose, to help illustrate the power of logical volumes.

# Graphical Options

As suggested earlier, excellent graphical front ends are available for disk partitions. The GParted and QtParted options are based on parted and are designed for the GNOME and KDE desktop environments, respectively. As they are not available from the Red Hat Network, they are not supported by Red Hat and therefore won't be available for any Red Hat exams.

One graphical option available for RHEL 6 is known simply as Disk Utility, available from the gnome-disk-utility package. Once appropriate packages are installed, you can open Disk Utility from the command line interface with the palimpsest command.

The Disk Utility screen shown in Figure 6-3 reveals an application that's far from perfect. The screen depicts the baseline virtual machine created in Chapter 2; it lists the virtual hard drive, device /dev/vda, as if it were a peripheral hard drive. Fortunately, that is a trivial error; the functionality of the tool is not affected. It is still a very capable tool that can organize your drives or destroy all of your data in a number of ways.

The functionality includes the following clickable options:

+   - Format Drive Supports changes to the entire drive.
+   - Benchmark Allows measurements of read and write performance.