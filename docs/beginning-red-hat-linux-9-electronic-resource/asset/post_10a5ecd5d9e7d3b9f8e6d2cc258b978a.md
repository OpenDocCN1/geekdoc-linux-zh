
```
(parted) rm 4
(parted) resize 2 101.975 5773.359
```

9. Now that we have learned to resize partitions, we can try and restore things to their original state (at the start of this example). We delete the newly created partition using the rm command, specifying the partition number of the partition we wish to remove. Finally, we resize Partition 2 to its original size:

```
(parted) print
Disk geometry for /dev/hda: 0.000-6149.882 megabytes
Disk label type: msdos
Number  Start     End       Size      File system  Flags
1       0.031     101.975   101.9MB  ext3         boot
2       101.975   5773.359  5.6GB    ext3
3       5773.359  6149.882  376MB    linux-swap
(parted) quit
```

10. The print command confirms our latest attempt to resize the partition. Once we are done experimenting, we exit the parted program using the quit command.

## Adding a New Hard Disk

Regardless of the hard disk real estate that we start out with, it is very likely that most of us will run out of disk space before the end of the lifecycle of our machines. This is when we will most likely get a disk upgrade by purchasing an additional hard disk or replace the current disk with one that has more storage capacity.

When we first installed Red Hat Linux 9 on the system, we did not have to bother about explicitly setting up our hard disk – the installer took care of this behind the scenes. But if we need to add a disk ourselves, there are a few manual steps that we need to perform.

## Detecting the Hard Disk

After hooking up the new hard disk to the system, and before going any further, it is necessary to ensure that the disk has been recognized by the operating system. Usually, Red Hat’s kudzu configuration tool will allow us to configure our new hardware when it is detected during the bootup process.

To ensure that the new disk has been recognized, we need to examine the kernel startup messages – these messages can be viewed using the dmesg command. We need to look for detection messages corresponding to our new hard disk. Here is a typical dmesg line, which indicates that the new hard disk has been detected:

```
$ dmesg | grep -i maxtor
hdb: Maxtor 90651U2, ATA DISK drive
```

> An alternative is to list the contents of /proc/partitions, which lists all the currently available partitions including those that have not been mounted yet. Here is the listing of a typical /proc/partitions file. For our purposes, it is sufficient to look for a new row in the table and note the name column, in this case hdb.

```
$ cat /proc/partitions
major minor #blocks  name
    3      1  104391 hda1
    3      2 5807497 hda2
    3      3  385560 hda3
    3      0 6297480 hda
   22      0  661728 hdo
   40     32 2805000 hdd
   40     64  24865 hdd1
   40     65 2337991 hdd2
   40     66  1939878 hdd3
```

*Note: The original OCR text for /proc/partitions contained significant noise and misalignment. The above table represents a cleaned-up, standard interpretation of such a listing, focusing on the relevant entries mentioned in the text (specifically the new disk 'hdb' which was likely 'hdd' in this specific OCR sample or a similar large disk, but the text refers to 'hdb' in the prompt. However, looking at the raw text: "22 0 661728 hdo" seems to be a misread of "hdb" or similar, and "40 32..." are likely noise. In standard Linux /proc/partitions, columns are Major, Minor, Blocks, Name. I will reconstruct the table based on standard formats and the specific values provided in the OCR, correcting obvious errors like 'hdo' to likely 'hdb' or keeping it if it's a specific example, but usually 'hdo' is not a valid disk name. Given the context says 'hdb', I will assume the '22 0 661728 hdo' line is a misread of a new disk, possibly 'hdb' with major 22? No, major 22 is usually IDE. Let's look at the raw: `22 0 661728 hdo`. It's highly probable 'hdo' is 'hdb' misread. And the subsequent lines with 40, 32, 280... are likely garbled data from another line or just noise. I will present the clean lines that make sense.*

If there are no kernel startup messages or listings in /proc/partitions, then it is quite likely that the disk was not detected. There are several possible reasons for the system's failure to detect the disk. To eliminate the possibility of a hardware setup problem, we should check all hardware settings such as the master-slave mode settings of the hard disk and compare them with the manufacturer's recommended settings. It's possible that the detection failure may have occurred because the correct driver is missing from the kernel; this problem can be remedied by re-compiling a kernel, or by using a dynamically loadable kernel module that has support for the new hard disk. Chapter 10 has details on how to perform these steps.

## Partitioning the Hard Disk

Once the disk has been detected, it is usually assigned a /dev name (such as /dev/hdb) automatically by the system. Once we know what this name is, as can be seen from the dmesg output or the /proc/partitions file, we need to partition the device.

If we intend to create a swap partition on this disk, the rule of thumb is to create a partition that is at least 2.5 times the size of the available physical RAM. We may use parted, fdisk, sfdisk (or another similar command) to partition the new drive. During the partitioning process, it is necessary to specify the intended file system for this hard disk.

## Formatting the Hard Disk

After partitioning, the next logical step is to format the disk. The formatting process prepares the partition for a certain file system type to create files and directories. During this process several file system-specific information may be created on the partitions. Formatting is very much specific to the file system that will be installed on the partition. For instance, to format the first partition of the /dev/hdb disk to use the ext3 file system, the following command is used:

```
# mkfs.ext3 -c /dev/hdb1
```

The -c option forces a check for disk errors.

## Mounting the Hard Disk

Now that we have partitioned and formatted the disk, it is ready for use and needs to be mounted to a file system mount point. For example, suppose we intend to mount the new partition to the directory /public. For this, we can use the following command:

```
# mount -t ext3 /dev/hdb1 /public
```

Although this command mounts the partition for now, it is *not* enough to mount the partition automatically when the system reboots. For **automatic mounting**, we need to add an entry to the /etc/fstab file. A typical entry would look like the one below:

| Filesystem | Mount point | Type | Options | Dump | Pass |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/hdb1 | /public | ext3 | defaults | 1 | 1 |

The first entry (/dev/hdb1) represents the partition containing the file system to be mounted. The second entry (/public) represents the directory that this file system should be mounted to. The third entry (ext3) indicates the file system type. The fourth entry indicates the permissions for the device; permissions determine the type of operations that may be performed on the file system. In this case, the default permissions (that is, allowing both read and write access) is in effect. The last two entries indicate operating system parameters (dump frequency and parallel *fsck* number) that may be left set to 1.

*The parted command has a copy command that enables entire file systems to be copied from one partition to another. This is particularly useful during disk upgrades that involve the replacement of an existing disk with a larger one. It is possible to add the new disk to the system without removing the older disk – possibly in a master–slave configuration. If you want to set this up, you should look at the disk manufacturer’s documentation.*

*Once both disks are hooked up to the system, we could use the parted copy command to copy the old file systems to the new partitions. Once the copy is complete, the old disk may be removed from the system or re-used (even perhaps as a swap disk) on the same system.*

From this point, we are ready to use the /public directory (in this case) just like any other directory on the system.

## File System Maintenance

For deriving optimum performance out of the file system, and to guard against data corruption, we need to ensure proper maintenance of the system in general and the file system in particular as it manages the persistent part of the operating system.

## Precautions

When it comes to file system maintenance, there are a number of simple precautions that help in preventing costly mishaps. It is extremely important that the system be properly shut down before restarting the machine. This is because on a running system, usually a significant part of the file system is always being worked upon in memory. In fact, if possible, it is a good idea to run the `sync` command before shutting down the machine, as this will flush unwritten file system blocks in memory to the disk – and hence avoid boot time file system inconsistencies.

As you’ll recall from Chapter 1, during the Red Hat Linux 9 installation we are prompted to create a boot disk. It is always a good idea to create a boot disk. This is particularly useful if the partition containing the bootable image of the kernel becomes corrupted. With a boot disk it is possible to boot up to a minimal shell and run diagnostics and repair tools.

If you have important data on your system, it is always a good idea to use some form of backup utility to back up the system periodically. We look at this in more detail in Chapter 10.

## Running fsck

Most Unix file system partitions contain a **super block**, which is essentially a ‘book-keeping section’ of that partition. When a system is shut down gracefully (that is, without errors), a flag is set to indicate the graceful shutdown. When the system comes up the next time, it examines this flag to see if the shutdown was graceful or not. If not, the system may require us to run diagnostic and repair tools on that partition.

The most popular diagnostics and repair utility on Linux (and in the UNIX world) is `fsck`. Running `fsck` with the `y` option allows `fsck` to proceed with any repairs that need to be performed in the course of diagnostic analysis. The `N` option to `fsck` would perform a dry run, i.e. the actual repair routines would not be performed but only printed out. Here is a typical output with the `N` option on a partition with a corrupted superblock.

```
$ /sbin/fsck -N /dev/hda
fsck 1.27 (8-Mar-2002)
[/sbin/fsck.ext3 (1) -- /dev/hda] fsck.ext3 /dev/hda
$ /sbin/fsck -y /dev/hda
fsck 1.27 (8-Mar-2002)
e2fsck 1.27 (8-Mar-2002)
Couldn't find ext3 superblock, trying backup blocks...
fsck.ext3: Bad magic number in super-block while trying to open /dev/hda
```

The superblock could not be read or does not describe a correct ext3 file system. If the device is valid and it really contains an ext3 file system (and not swap or ufs or something else), then the superblock is corrupt, and you might try running e2fsck with an alternate superblock:

```
e2fsck -b 8193 <device>
```
