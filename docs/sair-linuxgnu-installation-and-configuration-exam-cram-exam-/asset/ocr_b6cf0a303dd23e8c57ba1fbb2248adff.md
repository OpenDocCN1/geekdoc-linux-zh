On an older hard drive, cylinder 1023 may be as low as 512MB.

If you're removing Linux from your computer, you can remove LILO from your MBR with the MS-DOS fdisk /MBR command. If you really want to do this, load the fdisk command on a bootable floppy disk first.

# Mounts (/etc/fstab/)

The volumes that you configured when you installed Linux, plus a few more, are included in the /etc/fstab/ file. The volumes shown in Figure 6.1 are mounted when Linux boots on your computer.

# Mount File Format

The key information is shown in the first three columns of the /etc/fstab/ file. The other columns are included for reference:

+   - **Volume**—The first column indicates the subject volume. For example, the volume in the first line of Figure 6.1 corresponds to the first logical drive on the first hard disk on your computer.
+   - **Mount point**—The second column corresponds to the directory mounted on the specified volume. For example, the second line of Figure 6.1 shows the /boot directory mounted on the first partition on the first hard drive.
+   - **Format**—The third column corresponds to the way each volume is mounted. For example, ext2 corresponds to the second extended file system.
+   - **Mount option**—The fourth column specifies the types of users that can mount, whether they can read or write, and what can be run from the mounted directory.

![](bbox=[0.07, 0.78, 0.93, 0.95])

Figure 6.1 A sample /etc/fstab file.