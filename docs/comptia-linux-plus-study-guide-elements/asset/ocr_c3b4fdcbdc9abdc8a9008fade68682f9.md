You must modify your /etc/fstab entries for any partitions on which you want to use the quota support. In particular, you must add the us quota filesystem mount option to employ user quotas, and you must add the gr quota option to use group quotas. Entries that are so configured resemble the following:

```
1/dev/hdc5 /home ext3 us quota,gr quota 1 1
```

This line activates both user and group quota support for the /dev/hdc5 partition, which is mounted at /home. Of course, you can add other options if you like.

![](bbox=[0.17, 0.3, 0.25, 0.35])

> The format of the /etc/fstab file is described in more detail in later in this chapter in “Defining Standard Filesystems.”

Depending on your distribution, you may need to configure the quota package’s SysV startup scripts to run when the system boots. Chapter 4, “Managing System Services,” describes SysV startup script management in detail.

After installing software and making configuration file changes, you must activate the systems. The simplest way to do this is to reboot the computer, and this step is necessary if you had to recompile your kernel to add quota support directly into the kernel. If you didn’t do this, though, you should be able to get by with less directive measures: using modprobe to install the kernel module, if necessary; running the SysV startup script for the quota tools; and remounting the filesystems on which you intend to use quotas by typing mount -o remount /mount-point, where /mount-point is the mount point in question.

At this point, quota support should be fully active on your computer, but the quotas themselves are not set. You can set the quotas by using edquota, which starts the Vi editor (described in Chapter 3, “Managing Processes and Editing Files”) on a temporary configuration file (/etc/quota tab) that controls quotas for the user you specify. When you exit from the utility, edquota uses the temporary configuration file to write the quota information to low-level disk data structures that control the kernel’s quota mechanisms. For instance, you might type edquota sally to edit sally’s quotas. The contents of the editor will show the current quota information:

```
Quotas for user sally:  
1/dev/hdc5: blocks in use: 3209, limits (soft = 5000, hard = 6500)  
inodes in use: 403, limits (soft = 1000, hard = 1500)
```

The temporary configuration file provides information on both the number of disk blocks in use and the number of inodes in use. (Each file or symbolic link consumes a single inode, so the inode limits are effectively limits on the number of files a user may own. Disk blocks vary in size depending on the filesystem and filesystem creation options, but they typically range from 512 bytes to 8KB.) Changing the use information has no effect, but you can alter the soft and hard limits for both blocks and inodes. The hard limit is the maximum number of blocks or inodes that the user may consume; the kernel will not permit a user to surpass these limits. Soft limits are somewhat less stringent; users may temporarily exceed soft limit