When mounting non-FFS partitions or disks, you can use the `mount` command as described here, in conjunction with the -t option. Alternatively, you can use commands dedicated to each filesystem, such as mount_cd9660 and mount_msdosfs. These commands are described in Chapter 4, along with their options.

# ## Using /etc/fstab

The /etc/fstab file controls what partitions are mounted when FreeBSD boots and what partitions and disks may be mounted with truncated options, as just described. Listing 7-1 shows a simple /etc/fstab file. This listing includes a comment as the first line (indicated by the leading pound sign, #), which provides labels for each of the fields in the file. On each line, one or more spaces or tabs separate each field.

| Device | Mountpoint | FStype | Options | Dump | Pass# |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/ad0s2b | none | swap | sw | 0 | 0 |
| /dev/ad0s2a | / | ufs | rw | 1 | 1 |
| /dev/ad0s2f | /home | ufs | rw | 2 | 2 |
| /dev/ad0s1 | /windows | msdosfs | rw,-s,-u=1000 | 0 | 0 |
| /mnt/cd0 | /mnt/cdrom | cd9660 | ro,noauto | 0 | 0 |
| proc | /proc | procs | rw | 0 | 0 |
| speaker | /home/speaker/home | nfs | rw | 0 | 0 |

Most of the information in the /etc/fstab file is the same as information provided on a mount command line. In particular, the **Device** field specifies the device filename associated with the partition or disk, the **Mountpoint** field lists the mount point, and the **FStype** field specifies the filesystem type. The **Dump** field provides information on the dump frequency—the frequency with which the dump utility backs up a partition, if you use dump for backups. The **Pass#** field is the order in which fsck checks filesystems when the system boots—normally, the root (/) filesystem uses an order of 1, and other FFS partitions have an order of 2.

The **Options** field deserves more explanation. It lists options that can be passed via the -o parameter to mount. Some of these options duplicate the action of mount parameters that don’t use -o; others are unique to -o or are used only in /etc/fstab, and a few are filesystem-specific. Some common options include:

+   - **ro and rw** These options specify a read-only or a read/write mount, respectively. An initial FreeBSD configuration specifies one or the other for every filesystem.
+   - **noauto** By default, FreeBSD mounts the filesystem when it boots. Some devices, such as a CD-ROM, might be better configured with noauto, which makes FreeBSD ignore them at boot time. This setting enables you to issue a shorthand mount command, such as mount /mnt/cdrom, to mount the CD-ROM device specified in Listing 7-1.