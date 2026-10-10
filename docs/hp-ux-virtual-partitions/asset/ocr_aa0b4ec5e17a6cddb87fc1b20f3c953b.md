![](bbox=[0.21, 0.09, 0.85, 0.58])

*Figure 11-31 Increase Size Window*

SAM will increase the size of the logical volume only if it can be unmounted. Viewing the log file after this task has been completed shows that SAM ran such commands as */sbin/lvextend* and */sbin/ext2dfs* to extend the size of the logical volume and file system, and */usr/sbin/umount* and */usr/sbin/mount* to unmount and mount the file system.

See the Logical Volume Manager detail in Chapter 9 for definitions of Logical Volume Manager terms. There is also a description of some Logical Volume Manager commands.