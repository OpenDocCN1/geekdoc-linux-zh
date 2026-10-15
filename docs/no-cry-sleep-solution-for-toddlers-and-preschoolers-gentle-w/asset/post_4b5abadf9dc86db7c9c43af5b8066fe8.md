
## TABLE 30-11 Commonly Used fdisk Commands

| Command | Action |
|---|---|
| a | Toggle a bootable flag |
| l | List known partition types |
| m | List commands |
| n | Add a new partition |
| p | Print the partition table |
| q | Quit without saving changes |
| t | Change a partition's system ID |
| w | Write table to disk and exit |

different type of partition, such as a swap partition, press T to indicate the type you want. Enter the partition number, such as 82 for a swap partition. When you are finished, press W to write out the changes to the hard disk, and then press ENTER to continue.

### parted

As an alternative to fdisk, you can use parted (www.gnu.org/software/parted). parted lets you manage hard disk partitions, create new ones, and delete old ones. Unlike fdisk, it also lets you resize partitions. For you to use parted on the partitions in a given hard drive, none of the partitions on that drive can be in use. This means that if you wish to use parted on partitions located on that same hard drive as your kernel, you have to boot your system in rescue mode and choose not to mount your system files. For any other hard drives, you only need to unmount their partitions and turn your swap space off with the swapoff command. You can then start parted with the parted command and the device name of the hard disk you want to work on. The following example starts parted for the hard disk /dev/hda.

```
parted /dev/hda
```

You use the print command to list all your partitions. The partition number for each partition will be listed in the first column under the Minor heading. The Start and End columns list the beginning and end positions that the partition uses on the hard drive. The numbers are in megabytes, starting from the first megabyte to the total available. To create a new partition, use the mkpart command with either primary or extended, the file system type, and the beginning and end positions. You can create up to three primary partitions and one extended partition (or four primary partitions if there is no extended partition). The extended partition can, in turn, have several logical partitions. Once you have created the partition, you can later use mkfs to format it with a file system. To remove a partition, use the rm command and the partition number. To resize a partition, use the resize command with the partition number and the beginning and end positions. You can even move a partition using the move command. The help command lists all commands.

### mkfs

Once you create your partition, you have to create a file system on it. To do this, use the mkfs command to build the Linux file system and pass the name of the hard disk partition as a parameter. You must specify its full pathname with the mkfs command. Table 30-12 lists the options for the mkfs command. For example, the first partition on the second hard drive has the device name /dev/hdb1. You can now mount your new hard disk partition, attaching it to your file structure. The next example formats that partition:

```
# mkfs -t ext3 /dev/hdb1
```

The mkfs command is really just a front end for several different file system builders. A file system builder performs the actual task of creating a file system. Red Hat supports various file system builders, including several journaling file systems and Windows file systems. The name of a file system builder has the prefix mkfs and a suffix for the name of the type of file system. For example, the file system builder for the ext3 file system is mkfs.ext3. For Reiser file systems, it is mkfs.reiserfs, and for Windows 16-bit file systems (95, 98, ME), it is mkfs.vfat. Some of these file builders are just other names for traditional file system creation tools. For example, the mkfs.ext2 file builder is just another name for the mke2fs ext2 file system creation tool, and mkfs.msdos is the mkdosfs command. As ext3 is an extension of ext2, mkfs.ext3 simply invokes mke2fs, the tool for creating ext2 and ext3 file systems, and directs it to create an ext3 file system (using the -j option). Any of the file builders can be used directly to create a file system of that type. Options are listed before the device name. The next example is equivalent to the preceding one, creating an ext3 file system on the hdb1 device.

```
mkfs.ext3 /dev/hdb1
```

## TABLE 30-12 The mkfs Options

| Options | Description |
|---|---|
| Blocks | Number of blocks for the file system. There are 1,440 blocks for a 1.44MB floppy disk. |
| -t file-system-type | Specifies the type of file system to format. The default is the standard Linux file system type, ext3. |
| file-system-options | Options for the type of file system specified. Listed before the device name, but after the file system type. |
| -V | Verbose mode. Displays description of each action mkfs takes. |
| -v | Instructs the file system builder program that mkfs invokes to show actions it takes. |
| -c | Checks a partition for bad blocks before formatting it (may take some time). |
| -l file-name | Reads a list of bad blocks. |
