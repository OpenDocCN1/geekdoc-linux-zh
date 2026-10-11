| Option | Use |
| :--- | :--- |
| -m | Displays size in megabytes. |
| -i | Displays inode usage information. |
| -l | Limits the listing to those in the local file system. |
| -x FILESYSTEM | Excludes the specified file system from the listing. |

Following are some examples of output produced using the `df` utility. The first example is using the `df` utility with no options. The second example produces human readable sizes for the file systems listed. The third example displays inode information for all mounted file systems.

```
# df
Filesystem 1k-blocks Used Available Use% Mounted on
/dev/hda8 4096380 1469176 2672704 36% /
/dev/hda5 15522 3710 11011 25% /boot
/dev/hdb1 9740592 6861408 2384384 74% /fun
# df -h
Filesystem Size Used Avail Use% Mounted on
/dev/hda8 3.9G 1.4G 2.5G 36% /
/dev/hda5 15M 3.6M 11M 25% /boot
/dev/hdb1 9.3G 6.5G 2.3G 74% /fun
# df -i
Filesystem Inodes IUsed IFree IUse% Mounted on
/dev/hda8 4294967295 0 4294967295 0% /
/dev/hda5 4016 27 3989 1% /boot
/dev/hdb1 1237888 9692 1228196 1% /fun
```

![](bbox=[0.11, 0.65, 0.17, 0.7])

Be sure to know the option used to display inode information for the file systems.

# Mounting and Unmounting File Systems

![](bbox=[0.11, 0.77, 0.17, 0.8])

**2.4 Devices, Linux File Systems, Filesystem Hierarchy Standard**

+   * Control filesystem mounting and unmounting. Mount and unmount filesystems manually, configure filesystem mounting on bootup, configure user-mountable removable filesystems. Includes managing file /etc/fstab.

The last step required for using a file system is that it must be **mounted**. Mounting a file system makes it available to the system and the user. This section covers the utilities used for mounting and unmounting file systems. Also covered here are the files that contain information for file systems on a Linux system. These tools are used on a daily basis when working with Linux systems and are of particular interest when preparing to use a system and when preparing for the exam.