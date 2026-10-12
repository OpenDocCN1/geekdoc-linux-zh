
# Repairing Filesystems

Some disk data is kept in memory temporarily before being written to disk for performance reasons. (See the earlier discussion of the sync mount option.) If the kernel does not have an opportunity to actually write this data, the filesystem can become corrupted. This can happen in several ways, for example:

- The storage device (for example, a diskette) can be manually removed before the kernel has finished with it.
- The system might suffer a power loss.
- The Linux kernel locks up or reboots the system. Thankfully this is a very rare occurrence.
- The user might mistakenly turn off the power or accidentally press the Reset button.

As part of the boot process, Linux runs the **fsck** program, whose job it is to check and repair filesystems. Most of the time, the boot follows a controlled shutdown (see the manual page for **shutdown**), and in this case, the filesystems will have been unmounted before the reboot. In this case, **fsck** says that they are "clean." It knows this because before unmounting them, the kernel writes a special signature on the filesystem to indicate that the data is intact. When the filesystem is mounted again for writing, this signature is removed.

If, on the other hand, one of the disasters listed takes place, the filesystems will not be marked "clean" when **fsck** is invoked. As usual, it will notice this and begin a full check of the filesystem. This also occurs if you specify the *-f* flag to **fsck**. To prevent errors creeping up on it, **fsck** also enforces a periodic check; a full check is done at an interval specified on the filesystem itself (usually every 20 boots or 6 months, whichever comes sooner), even if it were unmounted cleanly.

The boot process (see Chapter 9, "System Startup and Shutdown") checks the **root** filesystem and then mounts it read/write. (It's mounted read-only by the kernel; `fsck` asks for confirmation before operating on a read/write filesystem, and this is not desirable for an unattended reboot.) First, the **root** filesystem is checked with the following command:

```
fsck -V -a /
```

Executing this command checks all the other filesystems:

```
fsck -R -A -V -a
```

These options specify that all the filesystems should be checked (-a) except the **root** filesystem, which doesn't need checking a second time (-R), and that operations produce informational messages about what it is doing as it goes (-V), but that the process should not be interactive (-a). The latter is specified because, for example, there might not be anyone present to answer any questions from `fsck`.

In the case of serious filesystem corruption, the approach breaks down because there are some things that `fsck` will not do to a filesystem without your permission. In this case, it returns an error value to its caller (the startup script), and the startup script spawns a shell to allow the administrator to run `fsck` interactively. When this happens, this message appears:

```
***An error occurred during the file system check.
***Dropping you to a shell; the system will reboot
***when you leave the shell.
Give root password for maintenance
(or type Control-D for normal startup);
```

This is a troubling event, particularly because it might well appear if you have other problems with the system—for example, a lockup (leading you to press the Reset button) or a spontaneous reboot. None of the online manuals are guaranteed to be available at this stage because they might be stored on the filesystem whose check failed. This prompt is issued if the **root** filesystem check failed or the filesystem check failed for any of the other disk filesystems.

When the automatic `fsck` fails, you need to log in by specifying the **root** password and run the `fsck` program manually. When you have typed in the **root** password, you are presented with the following prompt:

> (Repair filesystem) #

You might worry about what command to enter here or indeed what to do at all. At least one of the filesystems needs to be checked, but which one? The preceding messages from `fsck` should indicate which, but it isn't necessary to go hunting for them. You can give `fsck` a set of options that tells it to check everything manually, and this is a good fallback:

```
fsck -A -V ; echo == $? ==
```

This is the same command as the previous one, but the -R option is missing, in case the root filesystem needs to be checked, and the -a option is missing, so fsck is in its interactive mode. This might enable a check to succeed just because it can now ask you questions. The purpose of the `echo == $? ==` command is to unambiguously interpret the outcome of the fsck operation. If the value printed between the equal signs is less than 4, all is well. If this value is 4 or more, more recovery measures are needed. The meanings of the various values follow:

- 0 No errors
- 1 Filesystem errors corrected
- 2 System should be rebooted
- 4 Filesystem errors left uncorrected
- 8 Operational error
- 16 Usage or syntax error
- 128 Shared library error

If this does not work, it might be because of a corrupted superblock; fsck starts its disk check and if this is corrupted, it can't start. By good design, the ext2 filesystem has many backup superblocks scattered regularly throughout the filesystem. Suppose the command announces that it has failed to clean some particular filesystem—for example, /dev/sda1. You can start fsck again using a backup superblock by using the following command:

```
fsck -t ext2 -b 8193 /dev/sda1
```

8193 is the block number for the first backup superblock. This backup superblock is at the start of block group 1. (The first is numbered 0.) There are more backup superblocks at the start of block group 2 (16385) and block group 3 (24577); they are spaced at intervals of 8,192 blocks. If you made a filesystem with settings other than the defaults, these might change. mk2fs lists the superblocks that it creates as it goes, so that is a good time to pay attention if you're not using the default settings. There are further things you can attempt if fsck is still not succeeding, but these situations are rare and usually indicate hardware problems so severe that they prevent the proper operation of fsck. Examples include broken wires in the IDE connector cable and similar nasty problems. If this command still fails, you might seek expert help or fix the disk in a different machine.

These extreme measures are unlikely; a manual fsck, in the unusual circumstance where it is actually required, almost always fixes things. After the manual fsck has worked, the root shell that the startup scripts provide has done its purpose. Type exit to exit it. At this point, to make sure that everything goes according to plan, the boot process is started again from the beginning. This second time around, the filesystems should all be error-free and the system should boot normally.
