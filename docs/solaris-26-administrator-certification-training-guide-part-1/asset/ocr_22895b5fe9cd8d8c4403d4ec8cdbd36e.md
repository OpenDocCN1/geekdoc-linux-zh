Normally, fsck is run noninteractively at bootup to preen the file systems after an abrupt system halt in which the latest file system changes were not written to disk. Preening automatically fixes any basic file system inconsistencies and does not try to repair more serious errors. While preening a file system, fsck fixes the inconsistencies it expects from such an abrupt halt. For more serious conditions, the command reports the error and terminates. It then gives the operator a message to run fsck manually.

# How to Determine If a File System Needs Checking

File systems must be checked periodically for inconsistencies to avoid unexpected loss of data. As stated in the previous section, checking the state of a file system is automatically done at bootup; however, it is not necessary to reboot a system to check if the file systems are stable. The following procedure outlines a method for determining the current state of the file systems and whether they need to be fixed.

+   1. Become superuser.
2. Type fsck -m /dev/rdsk/cntndsn and press Enter. The state flag in the superblock of the file system you specify is checked to see whether the file system is clean or requires checking. If you omit the device argument, all the UFS file systems listed in /etc/fstab with a fsck pass value of greater than 0 are checked.

In this example, the first file system needs checking: the second file system does not:

```
fsck -m /dev/rdsk/c0t0d0s6
** /dev/rdsk/c0t0d0s6
ufs fsck: sanity check: /dev/rdsk/c0t0d0s6 needs checking
fsck -m /dev/rdsk/c0t0d0s7
** /dev/rdsk/c0t0d0s7
ufs fsck: sanity check: /dev/rdsk/c0t0d0s7 okay
```

# To Run fsck Manually

You might need to manually check file systems when they cannot be mounted or when you've determined that the state of a file system is unclean. Good indications that a file system might need to be checked are error messages displayed in the console window or system crashes for no reason.

When you run fsck manually, fsck reports each inconsistency found and fixes innocuous errors. For more serious errors, the command reports the inconsistency and prompts you to choose a response. Sometimes corrective actions performed by fsck result in some loss of data. The amount and severity of data loss can be determined from the fsck diagnostic output.