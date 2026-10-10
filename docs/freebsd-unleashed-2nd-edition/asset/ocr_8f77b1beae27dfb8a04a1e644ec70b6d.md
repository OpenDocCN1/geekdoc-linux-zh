You're asked for the mount point; enter /var. The partition is created and added to the list, and the "Free:" space listed at the top is updated accordingly.

Now you can repeat the process, this time accepting the default size for the remaining partition (to use all the rest of the space on the disk) and entering /usr for the mount point. The resulting list will be similar to Figure 18.5.

![](bbox=[0.108, 0.228, 0.736, 0.461])

Note that in the default layout, /var, /tmp, and /usr have the Soft Updates data-integrity protection system turned on (learn more about Soft Updates in “Journaling Filesystems and Soft Updates,” in Chapter 8). A filesystem that has Soft Updates turned on is denoted by UFS+S; you can toggle this with the S key. Soft Updates are advisable for filesystems with lots of data that changes frequently; /var is therefore a good candidate, as is /usr.

# ## Adding a New Disk

You can create up to eight BSD partitions on your new disk. Don’t use the A option if you’re simply creating more space to add to your current system; instead, with the “Partition name: adsl” line selected, press C to create a new partition. If you want to make one big BSD partition out of the disk (for example, if you want to add all 80GB to /home), accept the default value for the size of the S Partition—the entire available capacity of the slice you’re in. Alternatively, you might choose to specify a size (such as “20G”) for one partition and allocate the rest to another partition. It’s up to you how to carve up the space.

Select FS to create a filesystem rather than swap space and then specify a mount point. FreeBSD 5.0 or later will attempt to automount the new filesystem at the mount point you specify. This means that you should specify the mount point carefully so that the proper entry in /etc/fstab can be made and the disk can be mounted cleanly after the disk-labeling process is concluded.