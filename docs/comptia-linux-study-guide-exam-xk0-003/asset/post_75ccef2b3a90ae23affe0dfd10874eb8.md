
You must modify your `/etc/fstab` entries for any partitions on which you want to use the quota support. In particular, you must add the `usrquota` filesystem mount option to employ user quotas, and you must add the `grpquota` option to use group quotas. Entries that are so configured resemble the following:

```
/dev/hdc5 /home ext3 usrquota,grpquota 1 1
```

This line activates both user and group quota support for the `/dev/hdc5` partition, which is mounted at `/home`. Of course, you can add other options if you like.

![](img/9903a4d3f7abd8dcbef1035fa04a3406_303_0.png)

> The format of the `/etc/fstab` file is described in more detail later in this chapter in “Defining Standard Filesystems.”

Depending on your distribution, you may need to configure the quota package’s SysV startup scripts to run when the system boots. Chapter 4, “Managing System Services,” describes SysV startup script management in detail.

After installing software and making configuration file changes, you must activate the systems. The simplest way to do this is to reboot the computer, and this step is necessary if you had to recompile your kernel to add quota support directly into the kernel. If you didn’t do this, though, you should be able to get by with less disruptive measures: using `modprobe` to install the kernel module, if necessary; running the SysV startup script for the quota tools; and remounting the filesystems on which you intend to use quotas by typing `mount -o remount /mount-point`, where `/mount-point` is the mount point in question.

At this point, quota support should be fully active on your computer, but the quotas themselves are not set. You can set the quotas by using `edquota`, which starts the Vi editor (described in Chapter 3, “Managing Processes and Editing Files”) on a temporary configuration file (`/etc/quota.tab`) that controls quotas for the user you specify. When you exit from the utility, `edquota` uses the temporary configuration file to write the quota information to low-level disk data structures that control the kernel’s quota mechanisms. For instance, you might type `edquota sal ly` to edit sal ly’s quotas. The contents of the editor will show the current quota information:

```
Quotas for user sal ly:
/dev/hdc5: blocks in use: 3209, limits (soft = 5000, hard = 6500)
inodes in use: 403, limits (soft = 1000, hard = 1500)
```

The temporary configuration file provides information on both the number of disk blocks in use and the number of inodes in use. (Each file or symbolic link consumes a single inode, so the inode limits are effectively limits on the number of files a user may own. Disk blocks vary in size depending on the filesystem and filesystem creation options, but they typically range from 512 bytes to 8KB.) Changing the use information has no effect, but you can alter the soft and hard limits for both blocks and inodes. The hard limit is the maximum number of blocks or inodes that the user may consume; the kernel will not permit a user to surpass these limits. Soft limits are somewhat less stringent; users may temporarily exceed soft limit values, but when they do so, the system issues warnings. Soft limits also interact with a grace period; if the soft quota limit is exceeded for longer than the grace period, the kernel begins treating it like a hard limit and refuses to allow the user to create more files. You can set the grace period by using edquota with its -t option, as in edquota -t. Grace periods are set on a per-filesystem basis, rather than a per-user basis.

A couple more quota-related commands are useful. The first is quotacheck, which verifies and updates quota information on quota-enabled disks. This command is normally run as part of the quota package's SysV startup script, but you may want to run it periodically (say, once a week) as a cron job. (Chapter 3 describes cron jobs.) Although theoretically not necessary if everything works correctly, quotacheck ensures that quota accounting doesn't become inaccurate. The second useful auxiliary quota command is repquota, which summarizes the quota information on the filesystem you specify, or on all filesystems if you pass it the -a option. This tool can be very helpful in keeping track of disk usage.

## Partition Control

In addition to creating partitions and the filesystems they contain, system administrators must be able to control where these low-level filesystems are mounted in the Linux directory tree. If you want to make your changes permanent, you must modify a file called /etc/fstab. On a high-performance system, you might also want to link two or more disks together to improve performance or reliability.

### Identifying Partitions

If you installed Linux on the system, chances are you told it what partitions to use. If you don't remember what Linux called your partitions at system installation, you can use the fdisk program to find out. Pass it the -l parameter (that's a lowercase L, not a number 1) and the name of a disk device to obtain a listing of the partitions on that disk:

```
# fdisk -l /dev/hdb
```

Disk /dev/hdb: 255 heads, 63 sectors, 1216 cylinders
Units = cylinders of 16065 * 512 bytes

| Device | Boot | Start | End | Blocks | Id | System |
| :----- | :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/hdb1 | | 257 | 1216 | 7711200 | 5 | Extended |
| /dev/hdb2 | | 1 | 192 | 154208+ | fb | Unknown |
| /dev/hdb3 | | 193 | 256 | 51480+ | 17 | Hidden HPFS/NTFS |
| /dev/hdb5 | | 257 | 516 | 2088418+ | 6 | FAT16 |
| /dev/hdb6 | * | 517 | 668 | 1220908+ | 7 | HPFS/NTFS |
| /dev/hdb7 | | 669 | 1216 | 4401778+ | 83 | Linux |

This output shows the device name associated with each partition, the start and end cylinder numbers, the number of 1024-byte blocks in each partition, each partition’s hexadecimal (base 16) ID code, and the partition or OS type associated with that code. The fdisk program creates a similar display for GPT disks.

If Linux boots, you can also use the df utility (described later in “Using df”) to identify the partitions your system is using. This tool won’t identify partitions that aren’t mounted, though, including swap partitions and partitions you simply aren’t using (such as those for non-Linux OSs, unless they’re currently mounted).

## Mounting and Unmounting Partitions

Linux provides the mount command to mount a filesystem to a mount point—that is, to make the filesystem available as files and directories in the specified mount point, which is an ordinary directory. The umount command reverses this process. (Yes, umount is spelled correctly; it’s missing the first n.) In practice, using these commands is usually not too difficult, but they support a large number of options.

### Syntax and Parameters for mount

The syntax for mount is as follows:

```
mount [-alrsw] [-t fstype] [-o options] [device] [mountpoint]
```

Common parameters for mount support a number of features, as summarized in Table 6.6. device is the device filename associated with the partition or disk device, and mountpoint is the directory from which you want to access your files. Both parameters are normally required, but you may omit one of them under certain circumstances, as described shortly.

**TABLE 6.6 mount Options**

| Option | Description |
| :----- | :--------------------------------------------------------- |
| -a | This parameter causes mount to mount all the filesystems listed in the `/etc/fstab` file, which specifies the most-used partitions and devices. The upcoming section “Defining Standard Filesystems” describes this file’s format. |
| -r | This parameter causes Linux to mount the filesystem read-only, even if it’s normally a read/write filesystem. |
| -v | As with many commands, this option produces verbose output—the program provides comments on operations as they occur. |
| -w | This parameter causes Linux to attempt to mount the filesystem for both read and write operations. This is the default for most filesystems, but some experimental drivers default to read-only operation. |
