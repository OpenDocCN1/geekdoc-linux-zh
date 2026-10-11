6. Enter edquota <username>, then enter the number of inodes and 1KB blocks available, as follows:

```
fs </filesystemname> blocks (soft=20000, hard=22000)\\n\n\t\t\tinodes (soft=0, hard=0)
```

This command sets a 20MB soft quota on disk and a 22MB hard quota for user username.

7. Enter quota -v <username> to see if your desired settings were applied.

8. Turn the quota on by entering quotaon </filesystemname>.

Use the edquota command to add or subtract from a disk quota. To see all of the user quotas in effect, use the repquota </filesystemname> command. Disk quotas are usually set only on the specific directories that users can access and store personal files on, such as the /home directory. You issue the quotaon </filesystemname> (for example, quotaon /home) command to turn on quotas, typically as part of a startup script or a script that mounts a file system. The quotaon command turns on accounting, which is a logging system that reports on disk utilization for disk quotas on a per-user basis. When a file system is unmounted, the disk quotas are turned off. You can also turn quotas off by using the quotaoff </filesystemname> command. The vfstab file lists userquota or groupquota for any file system for which the repquota option is set.

> NOTE If you establish disk quotas, you should inform users what those quotas are. Otherwise, when a user exceeds their quota and sees a message like file system full or write failed for operations such as saving edited files or trying to retrieve e-mail, they won't be able to diagnose the problem from standard commands that show the amount of disk free space, such as df and du (described earlier).

# Disk Repair

For any number of reasons, file systems get corrupted. This can occur when your system crashes and a file isn't properly written back to disk from memory, when power is lost, or when a disk gets a physical error (damaged sector). Solaris provides the fsck (file system check) command to maintain and repair disk partitions, and when you give this command, a file system-specific fsck program is called and runs.

The fsck command goes through the following sequence of steps:

+   Check blocks and sizes. Inodes are checked for valid entries. When an error is detected, fsck posts the error PARTIALLY TRUNCATED INODE I=n (Salvage)? Answering Y (yes) repairs this error.