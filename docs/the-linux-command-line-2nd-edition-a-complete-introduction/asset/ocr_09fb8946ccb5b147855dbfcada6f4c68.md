can be applied to internal hard disks and other removable storage devices like USB hard drives.

# Testing And Repairing File Systems

In our earlier discussion of the /etc/fstab file, we saw some mysterious digits at the end of each line. Each time the system boots, it routinely checks the integrity of the file systems before mounting them. This is done by the fsck program (short for “file system check”). The last number in each fstab entry specifies the order in which the devices are to be checked. In our example above, we see that the root file system is checked first, followed by the home and boot file systems. Devices with a zero as the last digit are not routinely checked.

In addition to checking the integrity of file systems, fsck can also repair corrupt file systems with varying degrees of success, depending on the amount of damage. On Unix-like file systems, recovered portions of files are placed in the lost+found directory, located in the root of each file system.

To check our flash drive (which should be unmounted first), we could do the following:

```
[me@linuxbox ~]$ sudo fsck /dev/sdb1
fsck 1.40.8 (13-Mar-2008)
e2fsck 1.40.8 (13-Mar-2008)
/dev/sdb1: clean, 11/3904 files, 1661/15608 blocks
```

In my experience, file system corruption is quite rare unless there is a hardware problem, such as a failing disk drive. On most systems, file system corruption detected at boot time will cause the system to stop and direct you to run fsck before continuing.

# What The fsck?

In Unix culture, the word “fsck” is often used in place of a popular word with which it shares three letters. This is especially appropriate, given that you will probably be uttering the aforementioned word if you find yourself in a situation where you are forced to run fsck.

# Formatting Floppy Disks

For those of us still using computers old enough to be equipped with floppy diskette