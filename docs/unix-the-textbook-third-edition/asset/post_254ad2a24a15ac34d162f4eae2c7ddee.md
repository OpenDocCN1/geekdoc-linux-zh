
But to get more control over the whole range of subcommands and options of the zpool and zfs commands, and to be able to integrate that control with other UNIX commands, the command line is the more inclusive method of working with ZFS.

## Example 24.5: Creating a ZFS Pool on a USB Thumb Drive for Solaris

Objectives: To use zpool create to create a ZFS pool on a USB thumb drive.

Introduction: The following example uses the most essential command in ZFS, the zpool command, with the subcommand create applied to a USB thumb drive on your Solaris system. The real power of ZFS as a file system/volume manager/file backup system is most obvious in multidisk computer systems, where redundancy for files and directories can be established across two or more different physical disks. In addition, this redundancy can be extended to single-disk systems with the use of the zfs set property command, as shown in Problem 24.9 at the end of the chapter.

Many UNIX systems with a GUI interface like Gnome or KDE (e.g., Oracle Solaris, the current Solaris family UNIX system) automatically mount the USB thumb drive on the file system, and make it available as a desktop icon. This is similar to what you would experience on non-UNIX systems.

If the only thing you want to do is use the USB thumb drive to transfer files (e.g., text files, C program source code, LibreOffice documents, and so on) to and from the computer, you do not have to use the procedures of this example to accomplish that.

If you make a mistake anywhere along the way, you can always start over by executing the cleanup step shown at the end of the example and begin again.

Prerequisites:

- 1. That you have a USB thumb drive that is usable on your system and has one partition and no data on it. More specifically, if the USB thumb drive is by default formatted to FAT32, then there is a high probability that it will automatically mount and show up as an icon on your Gnome desktop in Solaris. You can also type the following on the command line as superuser, to enable automounting of removable media:

```
svcadm enable rmvolmgr
```

If your USB thumb drive does not automount, or does not appear as an icon on the Gnome desktop in Solaris, use another USB thumb drive.

- 2. That there is no pool named backup (or any other pool) already defined on the primary partition of the USB thumb drive, and there is no pool named test1 on your Solaris system. To find this out, type zpool list on the command line when the USB thumb drive has been inserted and automounts.

- 3. That you can determine the logical device name and the full path to it using the methods “A Quick and Easy Way to Find Out the Logical Device Names of Disks Actually Installed on Your System” from Section 24.2.1. The full path to our USB thumb drive is /dev/rdsk/c9t0d0 for Solaris. This may not be the same designation as the USB thumb drive on your system, but you can substitute your device designations for them.

Procedure: To complete the objectives of this example, do the following steps in the order presented.

- 1. Become the superuser.

```
bob@solaris:~$ su
Password: xxx
```

- 2. Put the thumb drive into a USB port on the computer, and it should automatically mount and appear as an icon on your Gnome desktop in Solaris. Determine the logical device name of the USB thumb drive, most easily done by typing the rmformat command on the command line, as shown in Section 24.2.1.

- 3. Create the pool, which we will name backup, on the USB thumb drive.

```
root@solaris:~# zpool create backup /dev/rdsk/c9t0d0
```

When the shell prompt reappears, the pool has been built.

Possible error messages:

- Not designating the proper full pathname to the USB thumb drive as a vdev. To create a zpool you must designate the full path to the drive.
- You should designate the entire disk, not just a single partition on it, as the vdev for zpool create.

- 4. List the zpools on your system.

```
root@solaris:~# zpool list
```

You should see your new zpool backup listed as /backup, along with any other pools that have been created by default. The listing for your new pool should also show the amount of disk space used on the drives, the total available disk space, and its mount point.

- 5. Check the listing using the df command.

```
root@solaris:~# df -h
```

In the listing you should see the new pool you created shown as /backup, right at the bottom of all the other pools created on your system by default at installation.

If you want to keep this USB thumb drive and the pool you created on it in the preceding steps so that you can do Problem 24.9 at the end of the chapter, do not continue onto the next step. If you want to reuse this USB thumb drive for another purpose, and do not want to do Problem 24.9 at the end of the chapter, proceed to the next step.

- 6. Now destroy the pool and exit as superuser.

```
root@solaris:~# zpool destroy backup
root@solaris:~# exit
```
