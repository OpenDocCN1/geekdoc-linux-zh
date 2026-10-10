
## The `fdisk` Program

The `fdisk` program is a fairly basic text-mode tool for manipulating partitions. If you use `fdisk`, you'll need to manually create filesystems, configure RAID or LVM, or set up swap space afterward.

![](img/9903a4d3f7abd8dcbef1035fa04a3406_291_0.png)

Linux on non-MBR systems may not use a tool called `fdisk`. For instance, PowerPC versions of Linux, which employ the APM partitioning system, use a tool called `pdisk`. Further complicating matters, some PowerPC Linux distributions call their `pdisk` programs `fdisk`. If your computer uses GPT, the `gdisk` program works much like `fdisk`, although a few details differ. If you're using a non-MBR system, consult the documentation for your distribution and its disk-partitioning tool. If you prefer, you can use GNU Parted on a wide variety of partition table types, bypassing `fdisk` or its workalikes entirely.

Linux's `fdisk` is a text-based tool that requires you to type one-letter commands. You can obtain a list of commands by typing `?` or `m` at the `fdisk` prompt. Table 6.2 describes the most important `fdisk` commands.

### **TABLE 6.2** `fdisk` Commands

| Command | Description |
| --- | --- |
| d | Deletes a partition |
| l | Lists partition type codes |
| m | Displays available commands |
| n | Creates a new partition |
| o | Creates a new partition table, wiping out all current partitions |
| p | Displays (prints) the partition layout |
| q | Quits without saving changes |
| t | Changes a partition's type code |
| w | Writes (saves) changes and quits |

To start `fdisk`, type its name followed by the Linux device filename associated with your disk device, as in `fdisk /dev/hdb`. When you first start `fdisk`, the program displays its prompt. It's often helpful to type `p` at this prompt to see the current partition layout, as shown in Figure 6.1. This will help you verify that you're operating on the correct disk, if you have more than one hard disk. It will also show you the device IDs of the existing disk partitions.

The `fdisk` program identifies the extended partition, if it's present, in the `System` column of its output, as shown in Figure 6.1; these partitions may be labeled as `Extended` or `Win95 Ext'd (LBA)`. Linux treats both types identically. Primary and logical partitions are not explicitly identified as such; you must use the partition number, as described earlier in “Linux Storage Hardware Configuration,” to identify the partition type.

You can use the commands outlined in Table 6.2 to alter a disk’s partition layout, but be aware that your changes are potentially destructive. Deleting partitions will make their data inaccessible. Some commands require you to enter additional information, such as partition numbers or sizes for new partitions. For instance, the following sequence illustrates the commands associated with adding a new logical partition that's 2GB in size:

```
Command (m for help): n
Command action
   l   logical (5 or over)
   p   primary partition (1-4)
   l
First cylinder (519-784, default 519): 519
Last cylinder or +size or +sizeM or +sizeK (519-784, default 784): +2G
```

### **FIGURE 6.1** As a text-based program, `fdisk` can be run in text mode or in a terminal window, as shown here.

![](img/9903a4d3f7abd8dcbef1035fa04a3406_292_0.png)

You can enter the partition size in terms of cylinder numbers or as a size in bytes, kilobytes, megabytes, or gigabytes (which isn't mentioned in the prompt but does work). When you've made your changes, type w to write them to disk and exit. If you make a mistake, type q immediately; doing this will exit from fdisk without committing changes to disk.

## Using GNU Parted to Create Partitions

GNU Parted is a more sophisticated partitioning tool than fdisk. GNU Parted supports several partition table types, including both MBR and GPT; it enables creation of filesystems during partition creation; and it can resize and move both partitions and the filesystems they contain. GNU Parted doesn't provide full support for all filesystems, though, and the details of what filesystems it does support varies from one build to another. Ext2fs, ext3fs, and FAT are almost always supported, but beyond that you may need to experiment.

To begin using GNU Parted, type the program name followed by the device filename associated with the disk you want to modify, as in **parted /dev/hdb**. You'll be greeted by a **(parted)** prompt, at which you can type GNU Parted commands, the most important of which are summarized in Table 6.3. Note that many commands have optional parameters. In most cases, if you omit these, GNU Parted will prompt you for the relevant information.

### **TABLE 6.3 GNU Parted Commands**

| Command | Description |
|---|---|
| help [COMMAND] | Displays information on all commands or on the one specified. |
| mlabel [type] | Creates a new partition table. The type is a type code, such as msdos for MBR or gpt for GPT. |
| mkfs [number [fstype]] | Creates a new filesystem on an existing partition. You can specify a partition *number* and a filesystem type (*fstype*). |
| mkpart [type [fstype]] [start [end]] | Creates a new partition. The type is primary, extended, or logical; the fstype is the filesystem type the partition will hold; and the start and end values are specified in bytes, kilobytes, megabytes, or gigabytes. (You use letter suffixes, as in 2G, to specify units.) |
| mkpartfs [type [fstype]] [start [end]] | Creates a new partition with a filesystem. This command works just like mkpart, but it creates a filesystem in the partition. |
| move [number [start [end]]] | Moves a partition. |
| name [number [name]] | Names a partition. This option is not meaningful for MBR disks, although it does set the partition name for GPT disks. |

### TABLE 6.3 GNU Parted Commands (continued)

| Command | Description |
| :--- | :--- |
| print [free\|number\|all] | Displays information. If given by itself, the partition table is shown. The free suboption displays a summary of free (unpartitioned) space on the disk. If you specify a number, basic information on the filesystem on the specified partition is displayed. If you use the all suboption, information on all disk devices is shown. |
| quit | Exits from the program. |
| resize [number [start [end]]] | Resizes the specified partition and its filesystem to the new size (defined by the start and end points). |
| rm [number] | Deletes the specified partition. |
| select [device] | Switches from the current device to the specified one. |

![](img/9903a4d3f7abd8dcbef1035fa04a3406_294_0.png)

> GNU Parted implements its changes immediately. With fdisk, if you make a mistake, you can use the q command to exit without altering the disk. With GNU Parted, you have no such way out. You should therefore be extra careful when using GNU Parted.

As an example of GNU Parted in action, consider using it to create a new (second) partition on a 2GB USB flash disk:

```
# parted /dev/sdc
GNU Parted 1.7.1
Using /dev/sdc
Welcome to GNU Parted! Type 'help' to view a list of commands.
(parted) print

Disk /dev/sdc: 2038MB
Sector size (logical/physical): 512B/512B
Partition Table: msdos

Number  Start   End     Size    Type     File system  Flags
1       0.51kB  1000MB  1000MB  primary  fat32        lba

(parted) mkpartfs
Partition type?  primary/extended? primary
File system type? [ext2]?
Start? 1000MB
End? 2038MB
(parted)
```

In this example, the print command displayed the current partition table to verify that the correct disk was being used. Upon issuing the mkpartfs command without extra options, GNU Parted prompted for values: the partition type, the file system type (giving no response caused the default value of ext2 to be used), and the start and end points. Unlike fdisk, which deals in cylinders by default, GNU Parted expects values in other units—megabytes in this example, although kilobytes or gigabytes could have been used. Although the display was eventually replaced by the final (parted) prompt, the program briefly displayed a summary of what it did as it created the partition and then the filesystem within it.

## Creating New Filesystems

Just creating partitions isn't enough to make them useful in Linux. To make them useful, you must create a filesystem on the partition (a task that's also sometimes called “formatting” a partition). If you use GNU Parted, you may be able to create a filesystem when you create a partition. If GNU Parted doesn't support your filesystem type, if you prefer to do it manually, or if you use fdisk to create partitions, you can use the mkfs program to do the job. This tool has the following syntax:

```
`mkfs [-v] [-t fstype] [options] device [blocks]`
```

![](img/9903a4d3f7abd8dcbef1035fa04a3406_295_0.png)

> mkfs is actually just a front-end to tools that do the real work for specific file systems, such as mke2fs (also known as mkfs.ext2). You can call these tools directly if you prefer, although their syntax may vary from that of mkfs.

The mkfs parameters can be used to perform several tasks, as summarized in Table 6.4.

### TABLE 6.4 mkfs Options

| Option | Description |
| :--- | :--- |
| -V | This option causes mkfs to generate verbose output, displaying additional information on the filesystem-creation process. |
| -t fstype | You specify the filesystem type with the -t fstype option. Common values for fstype include ext2 (for ext2fs), ext3 (for ext3fs), ext4 (for ext4fs), reiserfs (for ReiserFS), xfs (for XFS), jfs (for JFS), and msdos (for FAT). Some other options are available as well. |
