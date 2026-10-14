![](bbox=[0.11, 0.14, 0.91, 0.56])

# Figure 21-5: SysMan Station -- Physical File System View

There are several views that can be displayed by SysMan Station, and as you have probably guessed, the hardware view is one of the most useful. We won’t look at every view, but one more that’s particularly good is the physical_filesystems view as seen in Figure 21-5.

This view lists the various systems and the CFS-serving relationship for each mounted file system. If you want to manage the CFS configuration, you can start the CFS manager from this display and change the CFS server for a file system. Additionally you may wish to keep this view active to monitor how and if the CFS relationships change throughout the life of the cluster.

# 21.2 Moving the /tmp File System

A system manager will frequently want to move the /tmp file system to either a drive local to a cluster member or to another disk to improve file system performance. Another reason to move /tmp is because a user could potentially fill up the root file system by writing to /tmp. Making it a separate file system eliminates that possibility.

# 21.2.1 Creating /tmp on a Local Disk

First create an AdvFS domain and fileset on the desired disk/partition.