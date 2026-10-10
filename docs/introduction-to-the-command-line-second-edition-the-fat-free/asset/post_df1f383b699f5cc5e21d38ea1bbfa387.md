
## Section 10: File Systems

**Overview**

This section covers usage of basic file system management commands. It also covers popular partition editors for Unix, Linux, and BSD systems such as `fdisk` and `parted`. These commands can be used to create, modify, and delete file systems.

> **Warning**
>
> *The following commands can cause irreparable damage to your system if used incorrectly. Always experiment with new commands in a testing environment.*

**Commands covered in this section:**

| **Command** | **Purpose** |
| :--- | :--- |
| `fdisk` | Display and edit hard disk partitions. |
| `parted` | Display and edit partitions on Linux systems. |
| `mkfs` | Create file systems. |
| `fsck` | Check and repair file systems. |
| `badblocks` | Check a disk drive for bad blocks. |
| `tune2fs` | Adjust Linux file system parameters. |
| `mount`, `umount` | Mount/unmount local and remote file systems. |
| `mkswap` | Create swap space storage. |
| `swapon`, `swapoff` | Activate/deactivate swap space. |
| `swaponfo`, `swaptinfo` | Display swap space information. |
| `sync` | Flush file system buffers. |

### Glossary of terms used in this section:

| Term | Definition |
| :--- | :--- |
| Blocks | Physical storage units on a disk drive. |
| File System | A method and format for storing data on a disk drive. |
| Format | The process of preparing a disk drive for a specific file system. |
| Mount | Process used to attach storage devices to a local system. |
| Partition | A division of a disk drive. |
| Swap | A file or partition that acts as secondary storage for RAM. |

### fdisk

**Purpose:** Display and edit hard disk partitions.

**Usage syntax:** `fdisk [OPTIONS] [DEVICE]`

```
# fdisk -l /dev/sda
Disk /dev/sda: 160.0 GB, 16004189*696 bytes
255 heads, 63 sectors/track, 19457 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Disk identifier: 0x96000000

| Device | Boot | Start | End | Blocks | Id | System |
| :------- | :---- | :------ | :----- | :---------- | :---- | :----------------------|
| /dev/sda1 | * | 1 | 12 | 96358+ | de | Dell Utility |
| /dev/sda2 | | 13 | 19457 | 156191962+ | 5 | Extended |
| /dev/sda5 | | 13 | 504 | 3951958+ | 82 | Linux swap / Solaris |
| /dev/sda6 | | 505 | 19457 | 152239941 | 83 | Linux |
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_178_0.png)

**fdisk** is a disk partition editor for Unix, Linux, and BSD systems. In the above example, the `-l` option is used to display the partition information for the specified hard disk.

Executing **fdisk** with no options will open the specified disk for editing, as displayed in the next example.

```
# fdisk /dev/sda
Command (m for help): p

Disk /dev/sda: 160.0 GB, 160041885696 bytes
255 heads, 63 sectors/track, 19457 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Disk identifier: 0x96000000

| Device | Boot | Start | End | Blocks | Id | System |
| :------- | :---- | :------ | :----- | :---------- | :---- | :----------------------|
| /dev/sda1 | * | 1 | 12 | 96358+ | de | Dell Utility |
| /dev/sda2 | | 13 | 19457 | 156191962+ | 5 | Extended |
| /dev/sda5 | | 13 | 504 | 3951958+ | 82 | Linux swap / Solaris |
| /dev/sda6 | | 505 | 19457 | 152239941 | 83 | Linux |
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_178_1.png)

In this example, the **fdisk** utility starts an interactive shell that can be used to display and modify a disk's partitions. Within the shell, command keys are used to perform a specific task. The following table describes the basic commands available within the **fdisk** utility.

| Command | Function |
| :--- | :--- |
| **m** | Display the help menu |
| **p** | Display the partition table |
| **n** | Create a new partition |
| **a** | Make a partition bootable |
| **d** | Delete a partition |
| **l** | List partition types |
| **q** | Quit without saving changes |
| **w** | Save changes and exit |

> **Warning**
> *Incorrectly using the `fdisk` utility can cause data loss or leave your system unbootable. Always use caution when editing disk partitions and make sure to have a backup of your important data.*

Common usage examples:

- `fdisk -l` List the partition tables for all devices
- `fdisk -l [DEVICE]` List the partition tables on the specified device
- `fdisk [DEVICE]` Open the specified device for editing

### parted

**Purpose:** Display and edit partitions on Linux systems.

**Usage syntax:** `parted [OPTIONS] [DEVICE]`

```shell
# parted -1 /dev/sda
Model: ATA SAMSUNG HD080HJ/ (scsi)
Disk /dev/sda: 80.0GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos

Number Start End Size Type File system Flags
1 1049kB 106MB 105MB primary ntfs boot
2 106MB 47.2GB 47.1GB primary ntfs
3 47.2GB 80.0GB 32.8GB extended
5 47.2GB 78.6GB 31.4GB logical ext4
6 78.6GB 80.0GB 1398MB logical linux-swap (v1)
Displaying the partition layout of a disk using the parted utility
```

**parted** is a disk partition manager for Linux systems. It is similar to the `fdisk` utility (which is also available for Linux), except it offers a more user friendly interface. In the above example, the `-1` option is used to display the partition information for the specified hard disk.

Executing **parted** with no options will open the specified disk for editing, as displayed in the next example.

```shell
# parted /dev/sda
GNU Parted 1.8.8.1.159-1e0e
Using /dev/sda
Welcome to GNU Parted! Type 'help' to view a list of commands.
(parted) print
Model: ATA SAMSUNG HD080HJ/ (scsi)
Disk /dev/sda: 80.0GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos

Number Start End Size Type File system Flags
1 1049kB 106MB 105MB primary ntfs boot
2 106MB 47.2GB 47.1GB primary ntfs
3 47.2GB 80.0GB 32.8GB extended
5 47.2GB 78.6GB 31.4GB logical ext4
6 78.6GB 80.0GB 1398MB logical linux-swap (v1)
Editing a disk's partition using the parted utility
```

The following table provides an overview of basic `parted` partition editing commands.

| Command | Function |
| :--- | :--- |
| `print` | Display the partition table |
| `help` | Display the help menu |
| `mkpart` | Create a new partition |
| `rm` | Delete a partition |
| `quit` | Exit the program |

Common usage examples:

- `parted -l` List the partition tables for all devices
- `parted -l [DEVICE]` List the partition tables on the specified device
- `parted [DEVICE]` Open the specified device for editing

### mkfs

**Purpose:** Create file systems.

**Usage syntax:** `mkfs [OPTIONS] [DEVICE]`

```
# mkfs -t ext4 /dev/sdb1
mke2fs 1.41.9 (22-Aug-2009)
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
122400 inodes, 489131 blocks
24456 blocks (5.00%) reserved for the super user
First data block=0
Maximum file system blocks=503316480
15 block groups
32768 blocks per group, 32768 fragments per group
8160 inodes per group
Superblock backups stored on blocks:
	32768, 98304, 163840, 229376, 294912

Writing inode tables: done
Creating journal (8192 blocks): done
Writing superblocks and file system accounting information: done

This file system will be automatically checked every 21 mounts or
180 days, whichever comes first.  Use tune2fs -c or -i to override.

Creating an ext4 formatted file system using the mkfs command
```

The **`mkfs`** command creates (AKA formats) a file system on a disk drive. In the above example, the **`mkfs`** command is used on a Linux system to format the first partition of the `/dev/sdb` disk drive.

> **Warning** *The **`mkfs`** command will destroy all data on the target device.*

> **Note** *Usage syntax and supported options for **`mkfs`** vary across the different Unix, Linux, and BSD platforms. The above example was created on a Linux system. See `man mkfs` to find the correct usage syntax for your system.*

Common usage examples:

- `mkfs -t [FSTYPE] [DEVICE]` : Create a file system on the specified drive
- `mkfs -ct [FSTYPE] [DEVICE]` : Check for bad blocks before formatting
