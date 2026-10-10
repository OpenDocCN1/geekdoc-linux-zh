The main function of the fstab file is to give the system a profile of mounted devices that can be activated simultaneously at boot time. With all your mount points specified in the fstab file, you can issue the command mount -a to mount them all (which is what happens during bootup). When the system goes through its filesystem checks during bootup, it runs fsck -p to “preen” the filesystems, making sure they are all marked “clean” (you'll learn more about the fsck actions in “Checking and Repairing Filesystems with fsck,” later in this chapter). The system then runs mount -a -t nonfs to mount all but the NFS filesystems listed in /etc/fstab.

Beyond this function, though, is an even more convenient effect of this setup. After a mount point is specified in /etc/fstab, you no longer need to remember the mount command necessary to bring it online; now, the only thing you have to know is the name of the mount point:

```
# mount /home
```

This reads in all the necessary information from the fstab file. It knows that the device you want is /dev/ada0s1g, that it's a UFS (well, FFS) filesystem, and that you want it mounted read/write. Similarly, to mount a floppy disk, all you need to enter is the following:

```
# mount /floppy
```

Now, the process of mounting disks is starting to look almost user-friendly!

The noauto option on the /cdrom and /floppy entries tells mount that these filesystems should not be mounted at boot time. As with NFS resources, there is no guarantee that a CD-ROM or floppy disk will be available when the system boots, so the noauto option prevents mount from spending pointless time trying to mount a disk that isn't there. It doesn't prevent you from easily mounting it later, however. The previous command is all you need.

You can specify any of the mount options in the fourth column of the fstab file that are applicable to the filesystem in question. For instance, anything listed in man mount can be used, as well as anything in the filesystem’s man mount_.* page if it's a nonstandard filesystem type.

The fifth column in the /etc/fstab file contains the dump level numbers. These numbers are for the benefit of the dump command, which is a venerable Unix backup utility that operates based on levels. The dump level number tells dump at what level to trigger a backup for that filesystem when it is run. For example, filesystems with a dump level number of 1 are backed up only when the dump level is 1 or lower (a dump level of 0 indicates a full backup of all filesystems). Note that specifying 0 in /etc/fstab omits that filesystem from ever being dumped.