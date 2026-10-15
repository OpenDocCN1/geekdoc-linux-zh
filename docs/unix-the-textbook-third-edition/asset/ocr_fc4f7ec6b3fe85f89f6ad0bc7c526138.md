format command subcommands to check on the integrity of the new disk you added.

# Example 24.4: Mirroring of Hard Disks on PC-BSD

Objectives: To mirror the boot disk, sometimes called the system disk, onto another hard disk that is added to the system sometime after the initial build of PC-BSD.

Introduction: The following example illustrates one of the most important disk maintenance procedures a user can perform: the mirroring of a physical device using zpool attach. In the example, we mirror a PC-BSD boot disk onto another hard disk of equal (or greater) size.

This is important because if one of the hard disks, perhaps your original system disk, fails, you have an exact, bootable duplicate of it in your machine with which you can start up the system again. This system disk may also have all of your user datasets on it. You can then replace the failed disk and in a few simple ZFS steps, restoring the integrity and redundancy of your system without taking it offline!

This example accomplishes the same thing that the Clonezilla Live program illustrated in Chapter 23 does, but with one significant difference. Whereas Clonezilla Live "clones" an entire disk, including the boot sectors, at only one discrete instant in time, ZFS zpool attach applied to a mirrored pair that includes the system disk creates a constantly mirrored "clone" of the system disk and any other datasets on it. This is critical, because you never know when your system disk is going to fail. You can have any number of backup schemes in place, as shown in Chapter 23 and this chapter as well, to save user datasets with rolling, incremental backups using rsync or zfs snapshot. But this example's methodology allows you to constantly have an exact clone of your entire system available as long as it is running and active.

Of course, a more advanced and necessarily complex technique for doing what is shown here would involve multiple disks, including a separate system disk, higher-level RAIDZ dataset disks, and even the disk that holds the ZIL.

If you make a mistake anywhere along the way, you can always start over by executing the cleanup step shown at the end of the example and begin again. Depending on how far you go in the procedure, you can also reformat the new disk with the gpart command and restart from the beginning.

Prerequisites:

+   1. Using PC-BSD.
+   2. That you have previously completed Example 24.3.
+   3. That you have correctly connected and put a second hard disk onto your system, and it is unpartitioned but perhaps has a GPT partition scheme and table on it. It should also be large enough to accommodate everything on the original system disk partition we are going to use.
+   4. That you have previously determined the logical device name and the full path to it using the methods "A Quick and Easy Way to Find Out the Logical Device