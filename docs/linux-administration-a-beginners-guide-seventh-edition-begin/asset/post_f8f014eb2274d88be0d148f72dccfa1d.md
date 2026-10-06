
You can use the -f option with umount to force the unmount process. It is especially useful for Network File System (NFS)-type file systems that are no longer available.

Use the lazy unmount, specified with the -l option. This option always works when others fails. It detaches the file system from the file-system hierarchy immediately, and it cleans up all references to the file-system as soon as the system stops being busy.

The safest and most proper alternative is to bring the system down to single-user mode and then unmount the file system. In reality, of course, you don't have the luxury of being able to do this on production systems.

## etc/fstab File

As mentioned earlier, /etc/fstab is a configuration file that mount can use. This file contains a list of all partitions known to the system. During the boot process, this list is read and the items in it are automatically mounted with the options specified therein.
Here's the format of /etc/fstab file:

```
/dev/device /dir/to/mount ftype Parameters fs_freq fs_passno
```

Following is a sample /etc/fstab (lines have been added to the output to aid readability):

```
1. /mapper/fedora-root / ext4 defaults 1 1
2. UUID=a7cbf0b-40ee-4fba /boot ext4 defaults 1 2
3. /mapper/fedora-home /home ext4 defaults 1 2
4. /mapper/fedora-tmp /tmp ext4 defaults 1 2
5. /mapper/fedora-swap /swap ext4 defaults 0 0
6. /dev/s0 /media/cdrom auto user,noauto,exec 0 0
```

Let's look at some of the entries in the /etc/fstab file that have not been discussed.

Line 1: The first entry in our /etc/fstab file is for the root volume. The first column shows the device that houses the file system—the /dev/mapper/fedora-root logical volume (on more volumes in the section "Volume Management").
The second column shows the mount point—the / (slash or root) directory.
The third column shows the file type. the fourth column shows the options with which the file system should be mounted—only the default options are required in this case.

The fifth field is used by the dump utility (a simple backup tool) to determine which file systems needs to be backed up. The sixth and final field is used by the fsck program to determine whether the file system needs to be checked and also to determine the order in which checks are done.

Line 2: The next entry in our sample file is the /boot mount point. The first field of this entry shows the device—in this case, it the device identified by Universally Unique Identifier (UUID). In the case of the /boot mount point, you might notice that the field for the device looks a little different from the usual /dev/<path-to-device> convention. The use of a UUID to identify devices/partitions helps to ensure that they are correctly and uniquely identified under any circumstances—such as when a new disk is added or an existing disk is removed/replaced, or when changing the controller or bus to which the device is attached, and so.

Some distributions may use labels to identify the physical device in the first field of the /etc/fstab file. The use of labels helps to hide the actual device (partition) from which the file is mounted. When using labels, the device is replaced with a token that looks like the following: LABEL=/boot. During the installation, the partitioning program of the installer automatically sets the label on the partition. Upon reboot, the system scans the partition tables and looks for these labels. This is especially useful when Small Computer System Interface (SCSI) disks are being used. Typically, SCSI has a set SCSI ID. Using labels allows you to move the disk around and the system will still know how to mount the file even though the device might have changed, for example, from /dev/sda1 to /dev/sdb1 (see the section “Traditional Disk and Partition Naming Conventions” in a bit later in the chapter).

Labels are also useful for external media such as flash drives, USB hard drives, and so.
The other fields mean basically the same thing as the field for the root mount point discussed previously.

> The command-line utility blkid can be used to display attributes of the storage devices attached to a system. One of such attributes is the UUID of the volumes. For example, running blkid without any options will print a variety of information including the UUID of each block device on the system:

```
root@fedora-server ~] blkid
/dev/sda1: UUID="a7cbf0b-40ee-4fba" TYPE="ext4" PARTUUID="6925dab7-01"
/dev/sda2: UUID="t1c6fdg-10" TYPE="LVM2_member" PARTUUID="6925dab7-02"
/dev/mapper/fedora-swap: UUID="5f8b5428-af" TYPE="swap"
/dev/mapper/fedora-root: UUID="35b01f4-4c8" TYPE="ext4"
```

**Lines 3 and 4**: The next two entries are for the /home and /tmp mount points. They each refer to any physical entity on the system. Specifically, they refer to the fedora-home and fedora-tmp logical volumes, respectively. The remaining fields of lines 3 and 4 can be interpreted in the same manner as the fields of the preceding / (root) and /boot mount points.

**Line 5**: This is the entry for the swap partition, where virtual memory resides. In Linux, the virtual memory can be kept on a separate partition from the root partition (Note that a regular file can also be used for swap purposes). Keeping the swap space on a separate partition helps to improve performance. Also, because swap partition doesn't need to be backed up or checked with fsck at boot time, the last parameters in its entry are zeros. See the man page on mkswap for additional information.

**Line 6**: The last entry in the fstab file is worthy of mentioning the entry for removable media. In this example, the device field points to the device that represents the optical device (CD/ROM drive)—dev/sdb0. The mount point is /media/cdrom, and when an optical media (CD/DVD) is inserted and mounted on the system, the contents can be accessed from the /media/cdrom directory. The auto entry in the third field means the system will automatically try to probe the correct file system type for the device. For CD/ROMs, this is usually iso9660 or the Universal Disk Format (UDF) file system. The fourth field lists the mount options.

> TIP: Assuming the /etc/fstab configuration is properly configured with the correct device/mount points, you can run the command with only one parameter: the directory to which you want to mount. The command checks /etc/fstab for directory; if found, mount will use all parameters that have already established there. For example, here's a short command to mount a CD-ROM given the /etc/fstab file: # mount /media/cdrom

## Using fsck

The fsck tool (for File System Check) is used to diagnose and repair file systems that might have become damaged in the course of operations. Such repairs may be necessary after a system crash in which the system did not get a chance to fully flush all of its internal buffers to disk. (The fact that this tool's name—fsck—bears a striking resemblance to one of the expressions used by system administrators after a system crash, coupled with the fact that this tool can be used as a part of the recovery process, is strictly coincidental!)

Usually, the system runs fsck automatically during the boot process as it deems necessary (much in the same way Windows runs ScanDisk). If it detects a file system that was not cleanly unmounted, it runs the utility. A file check will also run if the system detects that a check has not been performed after a predetermined threshold, such as a number of mounts or time passed. Linux takes care of itself. The robust nature of the Linux file system helps in such situations. Nevertheless, you might get this message:

*** An error occurred during the file system check.
*** Dropping you to a shell; the system will reboot
*** you leave the shell.

At this point, you need to use fsck by hand and answer its prompts yourself.
If you find that a file system is not behaving as it should (log messages are an excellent hint of this type of anomaly), you may want to run fsck yourself on a running system. The only downside is that the file system in question must be unmounted in order to do this. If you choose to take this path, be sure to remount the file system when you are done.

The name fsck isn't the actual tool for the ext3 repair; it's actually just a wrapper. The fsck wrapper tries to determine what kind of system needs to be repaired and then uses the appropriate tool, passing any parameters that were passed to fsck. For the ext3 file system, the actual tool is fsck.ext3; for the ext4 file system, the actual tool is ext4; for the VFAT file system, the tool is called fsck.vfat; So, for example, if a system crash occurs on an ext4-formatted partition, you might choose to call fsck ext4 directly rather than relying on the wrapper tool fsck to call it for you automatically.

To run the /dev/mapper/fedora-home file system mounted at the /home directory, you would carry out the following steps:
Assuming the /home file system is not currently used or accessed by any process or user, mount the file system:

```
root@fedora-server ~# mount /home
```

Since we know that this particular file type is ext4, we can call the correct utility (fsck.ext4) directly to use the file system:

```
root@fedora-server ~# fsck /dev/mapper/fedora-home
fsck from util-linux-ng 2.18
efsck 1.* (17-May-2020)
/dev/mapper/fedora-home: clean, 246/3203072 files, 257426/1280496 blocks
```

This output shows that the file system is marked clean. To forcibly check the file system and answer yes to all questions in spite of what your OS thinks,

First, relax.
The fsck utility rarely finds problems that it cannot correct by itself. When it asks for human intervention, telling fsck to execute its default suggestion is often enough. Very rarely does a single pass of efsck clear up all problems. On the rare occasions when a second run is needed, it should not turn up any more errors. If it does, you are most likely facing a hardware failure. Remember to start with-
