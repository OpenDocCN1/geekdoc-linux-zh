
## Journaling Options in ext3

The **ext3** file system has several options that, depending on your needs, allow you to select how much information is journaled. According to Red Hat, the typical journal requires a second or so to be read and recovered. The time needed to recover from an improper shutdown of a journaled file system is not dependent on the file system size, but the amount of data in the journal.

The default setting provided by Fedora is adequate for most needs. The optimal choice depends on so many factors (computer usage, hardware used, and testing and evaluation methods) that a meaningful discussion is beyond the scope of this chapter. You learn in this chapter what the choices are and how they differ, but whether a choice is right for you can only be determined on an individual basis.

Like all journaling file systems, the traditional file system check (fsck) is not necessary on an **ext3** file system. Although only mildly annoying on a 20GB drive on your machine at home, imagine the seemingly endless hours that an **fsck** would take to run on a terabyte of data. This feature is shared in common with the other journaling file systems.

When choosing journaling options, you can trade off data integrity (keeping your data current and valid) for data transfer speed in your file system’s operation; you cannot have both because of the nature of the file system design. You can choose to expose some of your data to potential damage in the case of an improper shutdown in exchange for faster data handling, or you can sacrifice some speed to keep the state of the file system consistent with the state of the operating system.

Three modes available as options to ext3 are as follows:

- **writeback**—Enables ext3 data to stay in the file system; attaining the fastest speed possible. It does not schedule any data writes; it just enables the kernel’s 30-second writeback code to flush the buffer.
- **datavrb**—Keeps the data consistent, but with some sacrifice in speed (the default mode for Fedora).
- **journal**—Requires more disk space to journal more data. You might see slower performance because data is written twice, but there are some speed benefits if you are doing synchronous data writes as in database operations.

For most of us, the default selection represents a good trade-off. Fedora Core supports booting from an **ext3** formatted root file system with the proper drivers loaded in the **initrd** image.

The mode is selected by using the appropriate mount option in */etc/fstab*. For example, to set the file system mode to the fastest of the three modes, use `data=writeback` as the option. For more details, enter `man mount`.

## Verifying File Integrity in ext3 File Systems with the fsck Utility

The file system integrity is assured using `fsck`, or file system check, program—one of five commands in the library that are used to maintain and modify the ext3 file system.

When `fsck` is run, it performs a sequential analysis of the file system information available in the file system if it detects a directory that cannot be traced back to the root or an undeleted file with a zero link count. It places these directories and files in the /lost+found directory that is created on each physical partition by the file system formatting process. Some blocks are reserved for this and other uses by the super-user. It is possible to reduce this allocation to free additional space for regular users by special arguments to the formatting program `mke2fs`.

To run the `fsck` command, use the name of the file system as the argument. You must ensure that the file system you want to check is unmounted by using the `umount` command. If you want to `fsck` the file system at `/dev/hdc`, for example, do this:

```
# fsck /dev/hdc
```

**Tip**

If you are logged on as a regular user and `su` to root using `su`, you do not inherit root's environment and path, meaning that the preceding command will not work without using the full path: `/usr/sbin/fsck`.

Either type the full path each time, or become root with `su -`, which causes you to inherit root's environment and path; you have less to type.

The file system state is tracked in the ext3 file systems. A special field in the superblock tells the kernel that, after the file system is mounted read/write, it is marked as not `clean`; when it is properly unmounted, it is marked as `clean`. If a file system is not unmounted properly, it could contain corrupt data because all the file data might not have been written to it. (This is what the journaling file systems such as ext3 strive to eliminate.) When the system is booted, this flag is checked and if it is not `clean`, the program `fsck` is run. Internally, `fsck` is actually a wrapper program that runs the appropriate version of `fsck` for the file system in use: `fsck.minix`, `fsck.ext2`, `fsck.ext3`, `fsck.reiserfs`, `fsck.msdos`, and `fsck.vfat`. If the kernel detects an inconsistency in the superblock field, the file system is marked `erroneous`, and the file system check is forced even if other indicators suggest that `fsck` does not need to be run.

By default, the system will run `fsck` on a file system after a periodic number of reboots, regardless of the status of the `clean` flag. This behavior is triggered by a mount counter kept in the superblock or after a predetermined amount of time has elapsed since the last reboot (information also kept in the superblock). These parameters can be adjusted through the `tune2fs` command; this command can also be used to modify how the kernel handles the `erroneous` flag and, interestingly, the number of blocks reserved for the super-user, also known as `root`. This latter option is useful on very large or very small disks to make more disk space available to the user.

# Other File Systems Available to Fedora

Although **ext3** is certainly an acceptable root file system, there are other alternatives. No operating systems can support as many root file systems as Linux, which you should be aware that every file system has its strengths and weaknesses. Some are better with small files, some are better with large files, some are better at writing data, and some better at reading data. Unfortunately, there is no one perfect file system. The following sections discuss some of the other common file systems available for use with Fedora.

## The Reiser File System (reiserfs)

The other popular journaling file system for Linux is the written-from-scratch Reiser file system, **reiserfs**. It is used primarily in the SuSE distribution, which supports booting from a **reiserfs** root file system. **reiserfs** offers similar features to ext3, but there is no easy migration path from an already existing ext2 partition, as you learn to do in “Converting an Existing ext2 File System to ext3,” later in this chapter. In the past, **reiser4** didn't work well over NFS mounts, but recent versions of the **nfsd** daemons have fixed those problems. Fedora Core does offer **reiserfs**, but does not offer support for booting from it as the root partition file system, nor does it offer the choice to format non-root partitions as **reiserfs** during the installation process.

**reiserfs** is offered primarily for compatibility with existing **reiserfs** partitions you might want to access. Although the Reiser file system can be used as a root file system (meaning that Linux can be booted from a Reiser file system), Fedora has chosen not to support that option. The main problem is that **reiserfs** does not, at the time of writing, play nicely with SELinux and is therefore not recommended either by Red Hat or the NSA (SELinux’s developers).

> **NOTE**
> 
> The **reiserfs** file system has undergone a major update and release with Reiser4. The project, sponsored by The Defense Advanced Research Projects Agency (DARPA), aims to introduce improvements in a number of areas, such as maximum number of directories, files, links, sizes of individual files and size of the file system (nearly 18 terabytes). Other improvements include performance and encryption.

## JFS and XFS File Systems

Two commercial UNIX file systems have been ported (rewritten) to allow them to be used in Linux. IBM has provided its journaled file system (JFS) that is used with its commercial UNIX named AIX. Silicon Graphics, Inc. (SGI) has provided its XFS file system used by its commercial UNIX named IRIX. Because these file systems are generally suited for enterprise systems rather than home or small office systems, it seems likely that they are offered in Fedora Core Linux to ease the transition of IRIX and AIX users to Linux by eliminating the need for these users to reformat their very large file systems.

Beginning with kernel 2.6, XFS is fully supported in the kernel.
