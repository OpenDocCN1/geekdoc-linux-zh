
Although vendors all use standardized disk hardware, there’s a lot of variation among systems in the software domain. Accordingly, you’ll see a lot of vendor-specific details in this chapter. We try to cover each system in enough detail that you can at least identify the commands and systems that are used and can locate the necessary documentation.

## 8.1 | I JUST WANT TO ADD A DISK!

Before we launch into many pages of storage architecture and theory, let’s first address the most common scenario: you want to install a hard disk and make it accessible through the filesystem. Nothing fancy: no RAID, all the drive’s space in a single logical volume, and the default filesystem type.

Step one is to attach the drive and reboot. Some systems allow hot-addition of disk drives, but we don’t address that case here. Beyond that, the recipes differ slightly among systems.

Regardless of your OS, it’s critically important to *identify and format the right disk drive*. A newly added drive is not necessarily represented by the highest-numbered device file, and on some systems, the addition of a new drive can change the device names of existing drives. Double-check the identity of the new drive by reviewing its manufacturer, size, and model number before you do anything that’s potentially destructive.

### Linux recipe

![](img/14d78e3cecac4581d37024baf1e94cca_255_0.png)

Run **sudo fdisk -l** to list the system’s disks and identify the new drive. Then run any convenient partitioning utility to create a partition table for the drive. For drives 2TB and below, install a Windows MBR partition table. **cfdisk** is the easiest utility for this, but you can also use **fdisk**, **sfdisk**, **parted**, or **gparted**. Larger disks require a GPT partition table, so you must partition with **parted** or its GNOME GUI, **gparted**. **gparted** is a lot easier to use but isn’t usually installed by default.

Put all the drive’s space into one partition of unspecified or “unformatted” type. Do not install a filesystem. Note the device name of the new partition before you leave the partitioning utility; let’s say it’s **/dev/sdc1**.

Next, run the following commands and sequence, selecting appropriate names for the volume group (*vgname*), logical volume (*volname*), and mount point. (Examples of reasonable choices: homevg, home, and **/home**.)

```bash
$ sudo pvcreate /dev/sdc1                 # Prepare for use w/LVM
$ sudo vgcreate vgname /dev/sdc1           # Create volume group
$ sudo lvcreate -l 100%FREE -n volname vgname # Create logical volume
$ sudo mkfs -t ext4 /dev/vgname/volname     # Create filesystem
$ sudo mkdir mountpoint                     # Create mount point
$ sudo vi /etc/fstab                        # Set mount opts, mountpoint
```

In the /etc/fstab file, copy the line for an existing filesystem and adjust it. The device to be mounted is /dev/vgname/volname. If your existing fstab file identifies volumes by UUID, replace the UUID=xxx clause with the device file; UUID identification is not necessary for LVM volumes.

Finally, run sudo mount mountpoint to mount the filesystem.

See page 224 for more details on Linux device files for disks. See page 236 for partitioning information and page 251 for logical volume management. The ext4 filesystem family is discussed starting on page 255.

### Solaris recipe

Run sudo format and inspect the menu of known disks to identify the name of the new device. Let’s say it’s c9t0d0. Type <Control-C> to abort.

Run zpool create poolname c9t0d0. Choose a simple poolname such as “home” or “extra.” ZFS creates a filesystem and mounts it under /poolname.

See page 225 for more details on disk devices in Solaris. See page 264 for a general overview of ZFS.

### HP-UX recipe

Run sudo ioscan -fn -C disk to identify the device files for the new disk; let’s say they are /dev/disk/disk4 and /dev/rdisk/disk4.

Next, run the following command sequence, selecting appropriate names for the volume group (vgname), logical volume (volname), and mount point. (An example of reasonable choices: homevg, home, and /home.)

```
$ sudo pvcreate /dev/rdisk/disk4        # Prepare for use w/LVM
$ sudo vgcreate vgname /dev/disk/disk4   # Create volume group
$ vgdisplay vgname                       # View VG stats
...                                      
Free PE      freespace                   # Note this value
$ sudo lvcreate -l freespace -n volname vgname   # Create logical volume
$ sudo mkfs /dev/vgname/volname          # Create filesystem
$ sudo mkdir mountpoint                  # Create mount point dir
$ sudo vi /etc/fstab                     # Set mounting options
```

In the /etc/fstab file, copy the line for an existing filesystem and adjust it. The device to be mounted is /dev/vgname/volname.

Finally, run sudo mount mountpoint to mount the filesystem.

See page 225 for more details on HP-UX disk device files. See page 251 for logical volume management information. The VxFS filesystem is discussed starting on page 256.
