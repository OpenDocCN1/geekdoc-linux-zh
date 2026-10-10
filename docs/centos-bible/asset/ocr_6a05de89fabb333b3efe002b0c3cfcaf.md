```
/dev/devpts     /dev/pts     devpts    gid=5,mode=620  0 0
/dev/shm        /dev/shm     tmpfs     defaults       0 0
/dev/proc       /proc        proc      defaults       0 0
/dev/sys         /sys         sysfs     defaults       0 0
/dev/VolumeGroup/LogVol01  swap     swap   defaults       0 0
/dev/sda1        /mnt/win     vfat      noauto       0 0
```

All file systems listed in this file are mounted at boot time, except for those set to noauto in the fourth field. In this example, the root (/) and swap hard disk partitions are configured as logical volume management (LVM) volumes. This means that they may consist of multiple hard disk partitions. You can use the pvdisplay command to see what physical volumes make up each logical volume. An advantage of LVM volumes is that, if you run out of space in a logical volume, you can simply attach a new physical volume (such as a disk partition) to extend its size. You don't have to resize or create a new partition.

The proc, sys, /dev/shm, and /dev/pts file systems are not associated with particular devices. The floppy disk and CD-ROM drive entries are no longer included in the /etc/fstab file by default. That's because those media types are now handled by the hald daemon and are mounted automatically when they are inserted. The actual mount points will change based on the CD or DVD's volume name (implemented on that medium itself).

I also added one additional line for /dev/sda1, which allows me to mount the Windows (vfat in this case, but nfs support can be added) partition on my computer so I don't have to always boot Windows to get at the files on my Windows partition.

> **NOTE** To access the Windows partition described previously, I must first create the mount point (by typing mkdir /mnt/win). I can then mount it when I choose by typing (as root) mount /mnt/win.

You find the following in each field of the fstab file:

+   * Field 1 — The name of the device representing the file system. The word none is often placed in this field for file systems (such as /proc and /dev/pts) that are not associated with special devices. Notice that this field can now include the LABEL or UUID options. Using UUID, you can indicate a universally unique identifier (UUID). LABEL indicates a volume label instead of a device name. The advantage to the LABEL approach is that, since the partition is identified by volume name, you can move a volume to a different device name and not have to change the fstab file.

+   * Field 2 — The mount point in the file system. The file system contains all data from the mount point down the directory tree structure, unless another file system is mounted at some point beneath it.

+   * Field 3 — The file system type. Valid file system types are described in the "Supported File Systems" section earlier in this chapter.

+   * Field 4 — Options to the mount command. In the preceding example, the noauto option prevents the indicated file system from being mounted at boot time. Also, ro says