
## Filesystem Attributes

- Block size: 4096
- Fragment size: 4096
- Group descriptor size: 64
- Reserved GDT blocks: 1024
- Blocks per group: 32768
- Fragments per group: 32768
- Inodes per group: 8192
- Node blocks per group: 512
- Flex block group size: 16
- Filesystem created: Mon Jun 17 13:49:59 2019
- Last mount time: Fri Jun 28 21:14:38 2019
- Last write time: Mon Jun 17 13:53:39 2019
- Mount count: 8
- Maximum mount count: -1
- Last checked: Mon Jun 17 13:49:59 2019
- Check interval: 0 (<none>)
- Lifetime writes: 20 GB
- Reserved blocks uid: 0 (user root)
- Reserved blocks gid: 0 (group root)
- First inode: 11
- Inode size: 256
- Required extra isize: 32
- Desired extra isize: 32
- Journal inode: 8
- First orphan inode: 5117383
- Default directory hash: half_md4
- Directory Hash Seed: fa95a22a-a119-4667-a73e-78f77af6172f
- Journal backup: inode blocks
- Checksum type: crc32c
- Checksum: 0xe084fe23

ext filesystems have mount counts. The count is increased by 1 each time the filesystem is mounted, and when a threshold value (the maximum mount count) is reached the system will be automatically checked with e2fsck on the next boot.

The maximum mount count can be set with the -c N parameter, where N is the number of times the filesystem can be mounted without being checked. The -C N parameter sets the number of times the system has been mounted to the value of N. Note that command line parameters are case-sensitive, so -c is different from -C.

It is also possible to define a time interval between checks, with the -i parameter, followed by a number and the letters d for days, m for months and y for years. For example, -i 10d would check the filesystem at the next reboot every 10 days. Use zero as the value to disable this feature.

-L can be used to set a label for the filesystem. This label can have up to 16 characters. The `-U` parameter sets the UUID for the filesystem, which is a 128 bit hexadecimal number. In the example above, the UUID is `6e2c12e3-472d-4bac-a257-c49ac07f3761`. Both the label and UUID can be used instead of the device name (like `/dev/sda1`) to mount the filesystem.

The option `-e BEHAVIOUR` defines the kernel behaviour when a filesystem error is found. There are three possible behaviours:

- **continue**
  Will continue execution normally.
- **remount-ro**
  Will remount the filesystem as read-only.
- **panic**
  Will cause a kernel panic.

The default behaviour is to `continue`. `remount-ro` might be useful in data-sensitive applications, as it will immediately stop writes to the disk, avoiding more potential errors.

ext3 filesystems are basically ext2 filesystems with a journal. Using `tune2fs` you can add a journal to an ext2 filesystem, thus converting it to ext3. The procedure is simple, just pass the `-j` parameter to `tune2fs`, followed by the device containing the filesystem:

```
# tune2fs -j /dev/sda1
```

Afterwards, when mounting the converted filesystem, do not forget to set the type to `ext3` so the journal can be used.

When dealing with journaled filesystems, the `-J` parameter allows you to use extra parameters to set some journal options, like `-J size=` to set the journal size (in megabytes), `-J location=` to specify where the journal should be stored (either a specific block, or a specific position on the disk with suffixes like M or G) and even put the journal on an external device with `-J device=`.

You can specify multiple parameters at once by separating them with a comma. For example: `-J size=10,location=100M,device=/dev/sdb1` will create a 10 MB journal at the 100 MB position on the device `/dev/sdb1`.

> **WARNING**
>
> tune2fs has a "brute force" option, `-f`, which will force it to complete an operation even if errors are found. Needless to say, this should be only used with extreme caution.

### Maintaining XFS Filesystems

For XFS filesystems, the equivalent of `fsck` is `xfs_repair`. If you suspect that something is wrong with the filesystem, the first thing to do is to scan it for damage.

This can be done by passing the `-n` parameter to `xfs_repair`, followed by the device containing the filesystem. The `-n` parameter means “no modify”: the filesystem will be checked, errors will be reported but no repairs will be made:

```
# xfs_repair -n /dev/sdb1
Phase 1 - find and verify superblock...
Phase 2 - using internal log
    - zero log...
    - scan filesystem freespace and inode maps...
    - found root inode chunk
Phase 3 - for each AG...
    - scan (but do not clear) agi unlinked lists...
    - process known inodes and perform inode discovery...
    - agno = 0
    - agno = 1
    - agno = 2
    - agno = 3
    - process newly discovered inodes...
Phase 4 - check for duplicate blocks...
    - setting up duplicate extent lists...
    - check for inodes claiming duplicate blocks...
    - agno = 1
    - agno = 3
    - agno = 0
    - agno = 2
No modify flag set, skipping phase 5
Phase 6 - check inode connectivity...
    - traversing filesystem ...
    - traversal finished ...
    - moving disconnected inodes to lost+found ...
Phase 7 - verify link counts...
No modify flag set, skipping filesystem flush and exiting.
```

If errors are found, you can proceed to do the repairs without the `-n` parameter, like so: `xfs_repair /dev/sdb1`.

`xfs_repair` accepts a number of command line options. Among them:

- **-l LOGDEV and -x RTDEV**
  These are needed if the filesystem has external log and realtime sections. In this case, replace LOGDEV and RTDEV with the corresponding devices.
- **-m N**
  Is used to limit the memory usage of xfs_repair to N megabytes, something which can be useful on server settings. According to the man page, by default xfs_repair will scale its memory usage as needed, up to 75% of the system’s physical RAM.
- **-d**
  The “dangerous” mode will enable the repair of filesystems that are mounted read-only.
- **-v**
  You may have guessed it: verbose mode. Each time this parameter is used, the “verbosity” is increased (for example, -v -v will print more information than just -v).

Note that xfs_repair is unable to repair filesystems with a “dirty” log. You can “zero out” a corrupt log with the -L parameter, but keep in mind that this is a last resort as it may result in filesystem corruption and data loss.

To debug an XFS filesystem, the utility xfs_db can be used, like in xfs_db /dev/sdb1. This is mostly used to inspect various elements and parameters of the filesystem.

This utility has an interactive prompt, like parted, with many internal commands. A help system is also available: type help to see a list of all commands, and help followed by the command name to see more information about the command.

Another useful utility is xfs_fsr, which can be used to reorganize (“defragment”) an XFS filesystem. When executed without any extra arguments it will run for two hours and try to defragment all mounted, writable XFS filesystems listed on the /etc/mtab/ file. You may need to install this utility using the package manager for your Linux distribution, as it may not be part of a default install. For more information consult the corresponding man page.

### Guided Exercises

- 1. Using `du`, how can we check how much space is being used by just the files on the current directory?
- 2. Using `df`, list information for every ext4 filesystem, with the outputs including the following fields, in order: device, mount point, total number of inodes, number of available inodes, percentage of free space.
- 3. What is the command to run `e2fsck` on `/dev/sdc1` in non-interactive mode, while trying to automatically fix most errors?
- 4. Suppose `/dev/sdb1` is an ext2 filesystem. How can you convert it to ext3, and at the same time reset its mount count and change its label to UserData?
- 5. How can you check for errors on an XFS filesystem, *without* repairing any damage found?
