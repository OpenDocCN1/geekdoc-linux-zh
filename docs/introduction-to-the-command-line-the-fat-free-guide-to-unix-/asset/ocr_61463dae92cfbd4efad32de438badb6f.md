# parted

Purpose: Display and edit partitions on Linux systems.

Usage syntax: parted [OPTIONS] [DEVICE]

```
# parted -l /dev/sda
Model: ATA SAMSUNG HD080HJ/ (scsi)
Disk /dev/sda: 80.0GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos

Number  Start  End   Size  Type  File system  Flags
 1      1049kB 106MB 105MB primary ntfs boot
 2      106MB 47.2GB 47.1GB primary ntfs
 3      47.2GB 80.0GB 32.8GB extended
 5      47.2GB 78.6GB 31.4GB logical ext4
 6      78.6GB 80.0GB 1398MB logical linux-swap(v1)
Displaying the partition layout of a disk using the parted utility
```

parted is a disk partition manager for Linux systems. It is similar to the fdisk utility (which is also available for Linux), except it offers a more user friendly interface. In the above example, the -l option is used to display the partition information for the specified hard disk.

Executing parted with no options will open the specified disk for editing, as displayed in the next example.

```
# parted /dev/sda
GNU Parted 1.8.8.1.159-le0e
Using /dev/sda
Welcome to GNU Parted! Type 'help' to view a list of commands.
(parted) print
Model: ATA SAMSUNG HD080HJ/ (scsi)
Disk /dev/sda: 80.0GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos

Number  Start  End   Size  Type  File system  Flags
 1      1049kB 106MB 105MB primary ntfs boot
 2      106MB 47.2GB 47.1GB primary ntfs
 3      47.2GB 80.0GB 32.8GB extended
 5      47.2GB 78.6GB 31.4GB logical ext4
 6      78.6GB 80.0GB 1398MB logical linux-swap(v1)
Editing a disk’s partition using the parted utility
```