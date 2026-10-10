especially true for sound and network cards). You can specify the different hardware settings as additional parameters to the kernel in the `Linux` command and then boot from that entry in the GRUB menu.

# Root Drive Failure

Perhaps the worst feeling for a Linux system administrator is seeing that the bootloader can’t read the root drive device. However, this type of error may not be fatal, because it is sometimes possible to recover from a corrupted root drive.

# Using a Rescue Disk

Many Linux distributions provide a *rescue disk* for when fatal disk errors occur. The rescue disk usually boots either from the CD drive or as a USB stick and loads a small Linux system into memory. Since the Linux system runs entirely in memory, it can leave all of the work-station hard drives free for examination and repair. From the system command-line prompt, you can perform some diagnostic and repair tasks on your system hard drives.

The tool of choice for checking and fixing hard drive errors is the `fsck` command. The `fsck` command isn’t a program; it’s an alias for a family of commands specific to different types of filesystems (such as ext2, ext3, and ext4). You need to run the `fsck` command against the device name of the partition that contains the root directory of your Linux system. For example, if the root directory is on the `/dev/sda1` partition, you’d run the following command:

```
# fsck /dev/sda1
```

The `fsck` command will examine the inode table along with the file blocks stored on the hard drive and attempt to reconcile them. If any errors occur, you will be prompted on whether to repair them or not. If there are a lot of errors on the partition, you can add the `-y` parameter to automatically answer yes to all the repair questions. After a successful repair, it’s a good idea to run the `fsck` command once more to ensure that all errors have been found and corrected. Continue running the `fsck` command until you get a clean run with no errors.

# Mounting a Root Drive

When the `fsck` repair is complete, you can test the repaired partition by mounting it into the virtual directory created in memory. Just use the `mount` command to mount it to an available mount directory:

```
# mount /dev/sda1 /media
```

You can examine the filesystem stored in the partition to ensure that it’s not corrupted. Before rebooting, you should unmount the partition using the `umount` command:

```
# umount /dev/sda1
```

After successfully unmounting the partition, you can reboot your Linux system using the standard bootloader and attempt to boot using the standard kernel and runlevels.