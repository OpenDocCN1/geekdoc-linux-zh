
## Using Partitions and File Systems

![](img/96d9ccd181675a8ae8b6a1146c919d2b_233_0.png)

### EXAM OBJECTIVES

Exam 101 General Linux, Part 1

**2.4 Devices, Linux File Systems, Filesystem Hierarchy Standard**

- **Create partitions and filesystems.** Create disk partitions using fdisk, create hard drive and other media filesystems using mksfs.
- **Maintain the integrity of filesystems.** Verify the integrity of filesystems, monitor free space and inodes, fix simple file-system problems. Includes commands fsck, du, df.
- **Control filesystem mounting and unmounting.** Mount and unmount filesystems manually, configure filesystem mounting on bootup, configure user-mountable removable filesystems. Includes managing file /etc/fstab.

### CHAPTER PRE-TEST

1. Which file contains information on currently mounted file systems?
2. Which command is used to display the number of inodes on a file system?
3. Which command is used to mount all file systems listed in the `/etc/fstab` file?
4. What is the default file system type for Linux partitions?
5. Which utility is used to create a partition on a Linux system?
6. Which utility is used to format a partition using the Linux swap file system?
7. Which file contains the file systems mounted automatically by the operating system?
8. Which type of partition is bootable?
9. What is the device name used by the second partition on the second IDE drive?
10. Drive information such as labels, blocks, and inode tables is stored where?

## Linux File Systems Overview

This chapter covers the tools and practices associated with file systems and their management. Simply put, a file system is a way for the operating system to arrange files on the storage media so it can find them when it needs them. You use these tools to create, maintain, and control the file systems. These tools and concepts are used throughout the book and are important when working with Linux systems. Several exam objectives are covered in this chapter so you need to have a thorough understanding of all material presented here.

As you have already discovered, Linux file systems are discussed throughout the book. File systems are a primary component of all operating systems, and understanding the function and use of these systems is important. You will be required to know the differences in the various file systems as well as the proper use of each.

A variety of media can contain files for a Linux system. Hard disks, CD-ROMs, floppies, network drives, and other removable media can all be used to store files. Each of these media uses file systems for organization. These file systems arrange files in a tree-like directory structure with subdirectories branching from the root directory. The media and operating system used to store files dictate the file system used. Linux can support a wide variety of media and file systems depending on the configuration of the Linux kernel. With this support, you can create, access, and modify these file systems.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_235_0.png)

> This chapter covers the usage of file system tools while Chapter 13 details how to install the kernel options.

The mount command is used to connect various other file systems to the primary Linux file system, which currently defaults to the ext2 file system. The root user has control over the location of these additional file systems. The root user can grant standard users the proper access to mount specific file systems such as CD-ROMs and floppy disks for use on the system. When working with removable devices, remember that each disk must be mounted to be used. If you wish to access another disk, you must first unmount the current disk, swap the disks in the drive, and then mount the new disk for use. You can also configure file systems to be mounted automatically when the system is started. This ability is useful when working with file systems stored on the network or on local hard disks in the system. The tools and files used to allow these functions are covered later in this chapter.

### File system types

Many different file systems can be accessed using Linux systems. Table 5-1 shows many of these file systems and their use.

**Table 5-1 Linux File Systems**

| File System | Use |
| :--- | :--- |
| ext2 | Linux file system. |
| iso9660 | CD-ROM file system. |
| minux | Minux file system. |
| msdos | 16-bit MS-DOS FAT file system. |
| vfat | 32-bit Windows FAT file system utilizing long filenames. |
| hpfs | OS/2 file system. |
| proc | Linux processes file system. |
| nfs | Network file system used for accessing remote systems. |
| swap | Linux swap file system. |
| sysv | UNIX System V file system. |

These file systems can be thought of as languages. Linux is multilingual but must know the correct language to speak when communicating with each file system. As you can see, Linux supports file systems used by various other operating systems. This is useful for a system that dual boots with these other operating systems. Using the support for these file systems you can access non-Linux partitions for reading and writing files. The NTFS file system used by Windows NT and Windows 2000 is one file system not listed in Table 5-1; however, support for this file system is currently being developed for Linux systems to allow for read and write access to these partitions as well. The Reiser file system, reiserfs, is another not listed in Table 5-1. This is a journaling file system used by some Linux systems to allow for greater recovery in case of a system failure. This file system will be included with later versions of the Linux kernel. Later in this chapter you will learn how to specify the file system using files and commands.

> **Cross-Reference**
> For more information on reiserfs go to `http://www.reiserfs.org`

Along with the option of the file system type, understanding the device names used when working with storage media is important. Table 5-2 shows the various device prefixes used with Linux devices.

**Table 5-2 Device Names**

| Device Name | Use |
| :--- | :--- |
| hd | IDE hard drive partitions |
| sd | SCSI hard drive partitions |
| sr | SCSI CD-ROM drives |
| fd | Floppy drives |
| st | SCSI tape drives |
| ht | IDE tape drives |
| tty | Terminals |
| lp | Printers |
| pty | Remote terminals |
| js | Joystick ports |
| midi | MIDI ports |
| ttyS | Serial ports |
| cua | COM ports |
| cdrom | CD-ROM drives. This is often just a link to the actual IDE or SCSI device. |
| modem | Modem devices |

The prefixes are combined with a device number. With hard disks partitions the drive is specified with a letter such as a for the first drive, b for the second drive, and so on. The partition is specified with a number such as 1 for the first partition, 2 for the second partition, and so on. Examples of this naming:

- hdal The first partition on the first IDE hard drive.
- hdb2 The second partition on the second IDE hard drive.
- cdrom The first CD-ROM drive.
- cdroml The second CD-ROM drive.
- sda1 The first partition on the first SCSI hard drive.
- fd0 The first floppy disk drive.

These device names are used to address devices on a Linux system. All devices are stored in the /dev directory. The device names can be linked to other devices; for example, cdrom may be linked to /dev/sr0 if there is a SCSI CD-ROM installed on the system. These links allow for standard addressing of devices on systems. By examining the contents of the /dev directory you can view the links and exact locations of the devices on a system.

> **Exam Tip** Exam questions will reference devices, so understanding this naming scheme is important.

### Considerations when making a file system

Remember several considerations when creating a new file system. The file system does not just contain the data of the files stored on the disk. Some of the disk is used for overhead associated with file systems. This includes space for pointers that store the location of data that comprises files, as well as the file system size and label. All of this information uses space on the disk drive. The default settings for these components can affect what is stored on the partition, so you need to understand these components before creating a new partition. It is more difficult to correct problems once the partition has been created and data is stored in the file system.

### Inodes

The pointers used to identify the location of data stored in files are known as *inodes*. These are used for UNIX-based file systems and are not used with FAT file systems. When you create a file system, the inodes to be used are also created. This sets the number of files that can be stored on the file system. Unless you specify the number of inodes to be created, Linux will try to determine the number of inodes needed based on the partition size. This can cause wasted space if the file system will contain a small number of large files. Disk space can also be lost if the file system will store a large number of small files. Once the inodes have been filled, no new files can be created. The default inode configuration allows for the partition to be filled with files that are 2K in size.

> **Caution** Be sure that you understand the importance of inodes. Once you have run out of inodes on a file system, no new files can be created and the rest of the space on the file system will be unusable.

### Superblocks

The inodes for a file system are stored within the superblock. The superblock is a record that also contains information about file system size and location on the disk. Other important file system configuration information such as cylinders and disk block usage is also stored here. The information stored within the superblock is crucial for accessing the file system. Because of this, several copies of the superblock are stored throughout the disk. This provides fault tolerance so that if one superblock is damaged another can be used and the file system can be restored. A backup of the superblock is always stored every 8K blocks of the file system.
