# Chapter 13: Backing Up and Restoring Files 559

| Restore Options | Description |
| --- | --- |
| -y | The restore command will always continue when it encounters a bad block, rather than asking you if you want to continue. |

# Restoring an entire file system

Let's return to our earlier example of the Friday crash crash. You installed a shiny new drive and your backup tapes are in hand. It is time to restore the files. For the purposes of this example, I assume that the crashed drive contained only the /home partition and that the Linux operating system is still intact. If the crashed drive you would first have to reinstall Linux before restoring the backup.

With your new disk, install the fdisk command to partition the disk, as described in Chapter 2 of the network on partitioning your disks.

Before any files can be recovered to your new drive, an empty file system must be created on it. You use the mkfs command to do this. The mkfs command can accept a variety of parameters, but you usually need to supply only the name of the device to create the file system on. Then, to prepare the new drive, type:

```
# mkfs -t ext3 /dev/sdb1
```

Alternatively, because your /home drive is listed in the /etc/fstab file, you can simply specify the /home mount point and mkfs will figure out the correct device. Thus, the preceding command can be replaced with:

```
# mkfs /home
```

> CAUTION: You should, of course, exercise caution when using the mkfs command. If you specify the device name, you could unintentionally wipe out all data on an existing file system.

After creating a file system on your new disk, mount the partition to a temporary mount point.

```
# mkdir /mnt/test
# mount /dev/sdb1 /mnt/test
```

This connects the file system to the /mnt/test directory. Now change into the directory (cd /mnt/test) and use the restore command to recover the entire file system off of your backup tape. Of course, it is assumed that you have loaded the tape into the tape.

```
# cd /mnt/test
# restore rf /dev/nf0
```

When the restore is finished, you can unmount the partition and remount it to the appropriate mount point. If you have restored the file system to a different physical partition that it was originally on, be sure to modify the /etc/fstab file appropriately so that the correct partition is mounted next time the system is rebooted.