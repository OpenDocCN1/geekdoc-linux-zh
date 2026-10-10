
## Partition Management and Maintenance

### TABLE 6.4 mkfs Options (continued)

| Option | Description |
| :--- | :--- |
| *filesystem-specific* options | Many of the underlying tools upon which `mkfs` relies support their own options. You can pass these along, but details vary from one filesystem to another. The `-c` and `-v` options are common: these perform low-level hardware checks when creating the filesystem and generate verbose output, respectively. |

*device* is the name of the device on which you want to create the filesystem, such as `/dev/sda5` or `/dev/fd0`. You should *not* normally specify an entire hard disk here (such as `/dev/sda` or `/dev/hdb`). One exception might be if it's a removable disk, but even these are often partitioned.

The *blocks* parameter sets the size of the filesystem in blocks (usually 1,024 bytes in size). You don't normally need to specify this value, since `mkfs` can determine the filesystem size from the size of the partition.

Depending on the size and speed of the disk device, the filesystem-creation process is likely to take anywhere from under a second to a minute or two. If you specify a filesystem check (which is often a good idea, particularly on new or very old disks), this process can take several minutes or possibly over an hour. Once it's done, you should be able to mount the filesystem and use it to store files.

![](img/9903a4d3f7abd8dcbef1035fa04a3406_296_0.png)

The filesystem-creation process is inherently destructive. If you accidentally create a filesystem in error, it will be impossible to recover files from the old filesystem unless you're very knowledgeable about filesystem data structures or you pay somebody with such knowledge. Recovery costs are apt to be very high.

As noted earlier, `mkfs` is just a front-end to other utilities, which are sometimes called directly instead. For instance, you might call the `mkreiserfs` utility to prepare a ReiserFS partition, `mkfs.ext3` to prepare an ext3 partition, or `mkdosfs` to prepare a FAT partition or floppy disk. Check the `/sbin` directory for files whose names begin with `mkfs` to see what other filesystem-specific `mkfs` tools exist on your system.

![](img/9903a4d3f7abd8dcbef1035fa04a3406_296_1.png)

The presence of a filesystem-creation tool on your computer doesn't necessarily mean that you'll be able to read and write the filesystem on your computer. Mounting a filesystem requires appropriate kernel support, which can be compiled and installed independently of the filesystem's `mkfs.fstype` tool.

### Checking a Filesystem for Errors

Creating partitions and filesystems are tasks you're likely to perform every once in a while—say, when adding a new hard disk or making major changes to an installation. Another task is much more common: checking a filesystem for errors. Bugs, power failures, and mechanical problems can all cause the data structures on a filesystem to become corrupted. If these problems are left unchecked, they can cause severe data loss. For this reason, Linux includes tools for verifying a filesystem's integrity and for correcting any problems that might exist. The main tool you'll use for this purpose is called `fsck`. Like `mkfs`, `fsck` is actually a front-end to other tools, such as `e2fsck` (aka `fsck.ext2` and `fsck.ext3`). The syntax for `fsck` is as follows:

```
fsck [-sACVRTNP] [-t fstype] [--] [fsck-options] filesystems
```

The more common parameters to this command enable you to perform useful actions, as summarized in Table 6.5.

| **Option** | **Description** |
| :--- | :--- |
| `-A` | This option causes `fsck` to check all the filesystems marked for routine checks in `/etc/fstab`. This option is normally used in system startup scripts. |
| `-C` | This option displays a text-mode progress indicator of the check process. Most filesystem check programs don't support this feature, but `e2fsck` does. |
| `-V` | Verbose output can be produced by using this option. |
| `-N` | This option tells `fsck` to display what it would normally do, without actually doing it. |
| `-t fstype` | Normally, `fsck` determines the filesystem type automatically. You can force the type with this flag, though. If used in conjunction with `-A`, this causes the system to check only the specified filesystem types, even if others are marked to be checked. If `fstype` is prefixed with `no`, then all filesystems *except* the specified type are checked. |
| Filesystem-specific options | Filesystem check programs for specific filesystems often have their own options. The `fsck` command passes options it doesn't understand, or those that follow a double dash (`--`), to the underlying check program. Common options include `-a` or `-p` (perform an automatic check), `-r` (perform an interactive check), and `-f` (force a full filesystem check even if the filesystem initially appears to be clean). |

Normally, you run `fsck` with only the filesystem name, as in `fsck /dev/sda6`. You can add options as needed, however. Check the `fsck` man page for less common options.

> **WARNING**  
> Run `fsck` only on filesystems that are not currently mounted or that are mounted in read-only mode. Changes written to disk during normal read/write operations can confuse `fsck` and result in filesystem corruption.

Linux runs `fsck` automatically at startup on partitions that are marked for this in `/etc/fstab`, as described later in the section “Defining Standard Filesystems.” The normal behavior of `e2fsck` causes it to perform just a quick cursory examination of a partition if it’s been unmounted cleanly. The result is that the Linux boot process isn’t delayed because of a filesystem check unless the system wasn’t shut down properly. A couple of exceptions to this rule exist, however: `e2fsck` forces a check if the disk has gone longer than a certain amount of time without checks (normally six months) or if the filesystem has been mounted more than a certain number of times since the last check (normally 20). Therefore, you will occasionally see automatic filesystem checks of ext2, ext3, and ext4 partitions even if the system was shut down correctly.

Journaling filesystems do away with filesystem checks at system startup even if the system was not shut down correctly. These filesystems keep a log of pending operations on the disk so that in the event of a power failure or system crash the log can be checked and its operations replayed or undone to keep the filesystem in good shape. This action is automatic when mounting such a filesystem. Nonetheless, these filesystems still require check programs to correct problems introduced by undetected write failures, bugs, hardware problems, and the like. If you encounter odd behavior with a journaling filesystem, you might consider unmounting it and performing a filesystem check—but be sure to read the documentation first. Some Linux distributions do odd things with some journaling filesystem check programs. Most notably, ReiserFS should not normally be checked at system startup, so distributions sometimes create special scripts or link `/sbin/fsck.reiserfs` to `/bin/true` to avoid problems. Such configurations speed system boot times should ReiserFS partitions be marked for automatic checks, but they can be confusing if you need to manually check the filesystem. If this is the case, run `/sbin/reiserfsck` to do the job.

### Adding Swap Space

Linux enables you to run programs that consume more memory than you have RAM in your system. It does this through the use of swap space, which is disk space that Linux treats as an extension of RAM. When your RAM fills with programs and their data, Linux moves some of this information to its swap space, freeing actual RAM for other uses. This feature, which is common on modern operating systems, is very convenient when your users run an unusually large number of programs. If you rely on this feature too much, however, performance suffers because disk accesses are far slower than are RAM accesses. It’s also important that you have adequate swap space on your system. If the computer runs out of swap space, programs may begin to behave erratically.
