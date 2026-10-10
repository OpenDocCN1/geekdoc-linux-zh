Adjust time between checks  Periodic disk checks are required based on time as well as the number of mounts. You can set the time between checks with the `-i interval` option, where `interval` is the maximum time between checks. Normally, `interval` is a number with the character d, w, or m appended, to specify days, weeks, or months, respectively.

Add a journal  The `-j` option adds a journal to the filesystem, effectively converting an ext2 filesystem into an ext3 filesystem.

Set the reserved blocks  The `-m percent` option sets the percentage of disk space that’s reserved for use by *root*. The default value is 5, but this is excessive on large multi-gigabyte hard disks, so you may want to reduce it. You may want to set it to 0 on removable disks intended to store user files. You can also set the reserved space in blocks, rather than by the percentage of disk space, with the `-r blocks` option.

As with most low-level disk utilities, you shouldn’t use `tune2fs` to adjust a mounted filesystem. If you want to adjust a key mounted filesystem, such as your root (/) filesystem, you may need to boot up an emergency disk system, such as the CD-ROM-based Knoppix (http://www.knoppix.org).

# Criteria for Completion

To complete this task you should have performed a disk check on one or more filesystems. You should be sure to unmount any filesystem before you check it. If your disk check revealed errors, the check program should have corrected them, possibly with some intervention by you.

![](bbox=[0.15, 0.54, 0.25, 0.58])

The Scenario specified that users reported strange disk-related behavior. Such problems can result from corrupted disk data structures, but they can also occur because of bad RAM, a bad CPU, buggy software, a system intrusion, or other problems. If a filesystem check reveals no errors, or if you correct errors but problems recur, you should investigate other possible sources of such problems.

# Task 5.7: Configure a Boot Loader

Most Linux software is stored in filesystems, which are normally held (on hard disks) in partitions. One critical piece of software, though, resides partly outside of filesystems and perhaps even outside of partitions. This software is the *boot loader*, which is the first program that a computer runs when it boots, outside of the BIOS. The boot loader is responsible for loading the Linux (or other OS’s) kernel into memory and running it. Most Linux systems use one of two boot loaders: the Linux Loader (LILO) or the Grand Unified Boot Loader (GRUB). Knowing how to configure these boot loaders will enable you to upgrade your kernel or pass new options to your kernel.