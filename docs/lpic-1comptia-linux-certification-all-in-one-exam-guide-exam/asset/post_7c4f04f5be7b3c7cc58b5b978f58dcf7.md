
## File System Errors and Utilities

- 4: File system errors left uncorrected
- 8: Operational error
- 16: Usage or syntax error
- 32: Fsck canceled by user request
- 128: Shared library error

Notice in this example that `e2fsck` was run. That’s because `fsck` is really just a front end to the following utilities:

- /sbin/fsck.msdos
- /sbin/fsck.cramfs
- /sbin/fsck.ext3
- /sbin/dosfsck
- /sbin/fsck.ext2
- /sbin/fsck
- /sbin/e2fsck
- /sbin/fsck.ext4
- /sbin/fsck.vfat
- /sbin/fsck.minix
- /sbin/fsck.reiserfs

If you run `fsck` without any options, it will query your `/etc/fstab` file to determine the file system type of the partition you want to check and then load the appropriate module for the file system. As you can see in the preceding list, versions of `fsck` exist for Reiser, ext2, ext3, and ext4 file systems.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_418_0.png)

> **NOTE** The `fsck.reiserfs` utility can be run using the `reiserfsck` front end.

After the check is complete, you can remount the partition using the `mount` command.

One very useful feature of `e2fsck` is its ability to restore a damaged superblock on ext2/3/4 file systems. Remember, earlier in this chapter we noted that the superblock is the block at the beginning of the partition that contains information about the structure of the file system. We also noted that most Linux file systems keep backup copies of the superblock at various locations in the partition. If the superblock gets corrupted, you can restore it using one of these backup copies. The syntax is **`e2fsck -f -b backup_superblock device`**. The `-f` option tells `e2fsck` to force a check, even if the file system seems to be clean. The `-b` option tells `e2fsck` which copy of the superblock it should use.

### Other Useful File System Management Utilities

Other useful file system management utilities include the following:

- **`tune2fs`**
    This utility is used to adjust various file system parameters on ext2/3/4 file systems. These are some of the options you can use:
    - `-c n` Sets the number of mounts (*n*) after which the filesystem will automatically be checked by fsck.
    - `-i interval d|m|w` Sets the maximum time between file system checks in d (days), m (months), or w (weeks).
    - `-j` Adds a journal to an ext2 file system.
    - `-L volume_label` Sets the volume label of the filesystem.

    Here is an example:

    ```bash
    ws1:/ # tune2fs -L NewVol /dev/sdb1
    tune2fs 1.41.11 (14-Mar-2010)
    ws1:/ #
    ```

- **`reiserfstune`**
    This is the Reiser equivalent of the tune2fs utility.

- **`dumpe2fs`**
    Displays lots of useful information about ext2/3/4 file systems. Use the `-h` option to make the output more readable. An example follows:

    ```bash
    ws1:/ # dumpe2fs -h /dev/sdb1
    dumpe2fs 1.41.11 (14-Mar-2010)
    Filesystem volume name:  NewVol
    Last mounted on:		/mnt/extra space
    Filesystem UUID: 95b5b6cc-19aa-49fe-972a-9a1f734906b0
    Filesystem magic number:	0x38655
    Filesystem revision #: 1 (dynamic)
    Filesystem features: has_journal ext_attr resize_inode dir_index filetype extent flex_bg sparse_super large_file huge_file unix_flags extra_isize
    Default mount options: (none)
    Filesystem state:  clean
    Errors behavior: Continue
    Filesystem OS type:  Linux
    Inode count: 402192
    Block count: 1605632
    Reserved block count: 80324
    Free blocks: 1544479
    Free inodes: 402180
    First block: 0
    Block size: 4096
    Fragment size: 4096
    Reserved GDT blocks: 391
    Blocks per group: 32768
    Fragments per group: 32768
    Inodes per group: 8208
    Inode blocks per group: 513
    Flex block group size: 16
    Filesystem created: Wed Mar 16 11:50:04 2011
    Last mount time: Wed Mar 16 14:27:42 2011
    Last write time: Wed Mar 16 14:49:50 2011
    Mount count: 2
    Maximum mount count: 28
    Last checked: Wed Mar 16 11:50:04 2011
    Check interval: 15552000 (6 months)
    Next check after: Mon Sep 12 11:59:04 2011
    Lifetime writes: 228 MB
    Reserved blocks uid: 0 (user root)
    Reserved blocks gid: 0 (group root)
    First inode: 11
    Inode size: 256
    Required extra isize: 28
    Desired extra isize: 28
    Journal inode: 8
    Default directory hash: half_md4
    Directory Hash Seed: dc2b79fe-1a2d-4511-84c4-ec421c1154e0
    Journal backup: inode blocks
    Journal features: (none)
    Journal size: 128M
    Journal length: 32768
    Journal sequence: 0x00000005
    Journal start: 0
    wsl:1: /#
    ```

- **`debugfs`**
    The `debugfs` program is an interactive file system debugger. It can be used to examine or even change the state of an ext2/3/4 file system. The syntax is `debugfs device`. When you run this command, the `debugfs:` prompt is displayed, as shown here:

    ```
    ws1:/sbin # debugfs /dev/sdb1
    debugfs 1.41.12 (14-Mar-2010)
    debugfs:
    ```

    By default, the file system is opened in read-only mode. If you need to make changes to the file system, you need to include the `-w` option to open it in read-write mode. Some of the commands you can enter at the `debugfs:` prompt include the following:
    - `show_super_stats`: Displays information equivalent to that displayed by `dumpe2fs`.
    - `write_in_file out_file`: Allows you to copy a file from the file system to another file system. This can be extremely useful in situations where you are trying to salvage an important file from a mangled file system.
    - `stat_file_or_directory.name`: Displays extended information about the file or directory specified. An example follows for a file named `myfile2.txt`:
        - Inode: 12
        - Type: regular
        - Mode: 0644
        - Flags: 0x80000
        - Generation: 556089601
        - Version: 0x00000000:00000001
        - User: 0
        - Group: 0
        - Size: 0
        - File ACL: 0
        - Directory ACL: 0
        - Links: 1
        - Blocksize: 0
        - Nbr: 0
        - Fragments: Address: 0, Num: 0, Size: 0
        - cTime: 0x4d812f93:d2d91b5c -- Wed Mar 16 15:45:55 2011
        - aTime: 0x4d812f93:d2d91b5c -- Wed Mar 16 15:45:55 2011
        - mTime: 0x4d812f93:d2d91b5c -- Wed Mar 16 15:45:55 2011
        - crTime: 0x4d812f93:d2d91b5c -- Wed Mar 16 15:45:55 2011
        - Size of extra inode fields: 28
        - EXTENTS: lines 1-12/12 (END)

- **`list_deleted_inodes`**
    Displays a list of deleted inodes in the file system. You can do a lot with `debugfs`. We don't have time or space to cover everything here. Have a look at the `debugfs` man page for more information.

- **`xfs_admin`**
    The xfs equivalent of `tune2fs`. This utility actually uses the `xfs_db` executable to modify various parameters of an xfs file system. The file system must be unmounted before you can make any changes. Some of the options you can use with this utility include the following:
    - `-j`: Enables version 2 log format, which is a journal format supporting larger log buffers.
    - `-l`: Displays the file system's label.
    - `-u`: Displays the file system's Universally Unique Identifier (UUID).
    - `-L label`: Sets the file system's label.
    - `-U uuid`: Sets the UUID of the file system.

- **`xfs_info`**
    Displays useful information about xfs file systems.

- **`xfs_metadump`**
    Dumps xfs file system metadata (such as filenames and file sizes) to a file.

## Checking for Open Files

Let's next look at how you identify open files on a Linux file system.

You can use the `lsof` command at the shell prompt to display a list of open files. Entering `lsof` at the shell prompt without any options lists all open files belonging to all active processes on the system. Useful options you can use with `lsof` include the following:

- `-s`: Displays file sizes.
- `-1`: Specifies that `lsof` should produce terse output with process identifiers only and no header. This is useful if you are piping the output of `lsof` to the `kill` command.
- `-u user_name`: Displays only open files associated with the specified user.

In the next example, a list of open files associated with the tux user on the system are displayed by `lsof`:

```
wsl:/sbin$ lsof -u tux | more
lsof: WARNING: can't stat() fuse-gvfsd-fuse-daemon file system /home/tux/.gvfs
Output information may be incomplete.

COMMAND PID USER FD TYPE DEVICE SIZE/OFF NODE NAME
gnome-key 3860 tux cwd DIR 8,3 4096 2 /
gnome-key 3860 tux rtd DIR 8,3 4096 2 /
gnome-key 3860 tux txt REG . 8,3 873828 409704 /usr/bin/
gnome-key ring-daemon
gnome-key 3860 tux mem REG 8,3 19114 411496 /lib64/
libdl-2.11.2.so
```
