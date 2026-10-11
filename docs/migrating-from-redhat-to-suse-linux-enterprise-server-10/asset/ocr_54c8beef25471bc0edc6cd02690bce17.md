+   
+   *   **Field 2.** Lists the mount point—the directory to which the file system should be mounted. The directory specified here must already exist. You can access the content on the media by changing to the respective directory.
+   *   **Field 3.** Lists the file system type (such as ext2, reiserfs).
+   *   **Field 4.** Shows the mount options. Multiple mount options are separated by commas (such as `noauto`, `user`, `sync`).
+   *   **Field 5.** Indicates whether to use the backup utility `dump` for the file system. `0` means no backup.
+   *   **Field 6.** Indicates the sequence of the file system checks (with the `fsck` utility) when the system is booted:
+       *   `0`: file systems that are not to be checked
+       *   `1`: the root directory
+       *   `2`: all other modifiable file systems; file systems on different drives are checked in parallel

While /etc/fstab lists the file systems and where they should be mounted in the directory tree during startup, it does not contain information on the actual current mounts.

The /etc/mtab file lists the file systems currently mounted and their mountpoints. The mount and umount commands affect the state of mounted file systems and modify the /etc/mtab file.

The kernel also keeps information for /proc/mounts, which lists all currently mounted partitions.

For troubleshooting purposes, if there is a conflict between /proc/mounts and /etc/mtab information, the /proc/mounts data is always more current and reliable than /etc/mtab.

# 1 HARDCOPY PERMITTED-NO DISTRIBUTION ALLOWED