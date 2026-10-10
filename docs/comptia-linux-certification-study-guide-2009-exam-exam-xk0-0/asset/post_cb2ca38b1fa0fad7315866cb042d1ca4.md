
## Self Test

8. To perform an HTTP-based network installation, you must enter the following information to establish connectivity with a remote network server.
   - A. Your workstation IP address and e-mail address.
   - B. The remote network server’s IP address and e-mail address.
   - C. The remote network server’s IP address and remote network server directory containing the Linux distribution source.
   - D. The remote network server’s IP address and your local workstation’s directory containing the Linux distribution source.

9. Your organization’s management team has decided to implement virtual partition technology. What is the name of the technology within a Linux operating system that supports virtual partitions?
   - A. Virtual file transfer (VTP)
   - B. Logical virtual management
   - C. Disk mirroring system (DMS)
   - D. Logical volume management (LVM)

10. What are the extended partitions used for on hard disk drives?
   - A. To further divide a hard disk drive into smaller partitions.
   - B. Extended partitions are not supported on hard disk drives.
   - C. Linux does not support extended hard disk drives.
   - D. Primary partitions and extended partitions cannot coexist on the same hard disk drive.

11. When using the `mkfs` command, what is the `-t` option used for when inserted as a parameter?
   - A. The `-t` option is used to test the network bandwidth.
   - B. The `-t` option is used to terminate the operating system.
   - C. The `-t` option is used to assign filesystems to partitions.
   - D. There is no `-t` parameter associated with the `mkfs` command.

12. To see all the current disk drives on your system and the current disk geometry, what command should you enter?
   - A. `mkfs -t`
   - B. `fdisk -l`
   - C. `fdisk -l`
   - D. `diskgeo -t`

13. What is the purpose of the `parted` command?
   - A. To reclaim unused disk space
   - B. To establish disk striping
   - C. To implement RAID 5
   - D. To test system’s on-board memory for defects

14. You are installing Linux on your organization’s server. This is a new installation. You must partition the hard disk for the new Linux installation. Which is the best hard disk partition architecture for supporting root, swap, and home partitions?
   - A. Primary partition architectures should be used for the root and swap partitions and extended partition architecture should be used for home partition.
   - B. The root, swap, and home partitions should all be extended partitions.
   - C. The root and home partitions should be placed on extended partition architectures and the swap partition should be placed on the primary partition.
   - D. Only swap and home should be placed on the primary partition and the root partition should not be used.

15. During the initial Linux installation process, which application is used to test your system’s RAM for an x86-based CPU architecture?
   - A. testmemx86
   - B. memtest86
   - C. memtestx86
   - D. memx86test

### Self Test Quick Answer Key

- 1. C
- 2. C
- 3. C
- 4. D
- 5. B
- 6. C
- 7. C
- 8. C
- 9. D
- 10. A
- 11. C
- 12. C
- 13. A
- 14. A
- 15. B

## Managing Filesystems

- Exam objectives in this chapter
  - Filesystem Types
  - Mounting and U(n)mounting Filesystems
  - Partitions
  - Directories
  - Filesystem Management

### Unique Terms and Definitions

- **Filesystem**: A *filesystem* provides the operating system with a framework (a structure) for the storage, organization, modification, removal, and retrieval of digital information. It is responsible for organizing and maintaining files, folders, metadata, and residual data as containers for storing digital information.
- **Swap**: The allocation of physical disk space to function as virtual memory when the amount of physical memory (random access memory [RAM]) is full. If the system needs more memory resources and the physical memory is full, inactive pages in memory are moved to the swap space. When the system swaps out pages of memory to the hard disk drive, the system’s RAM is freed up to perform additional functions.
- **Server message block file system (SMBFS)**: A mountable SMBFS for Linux that allows Windows- or Linux-based workstations access to directory/file shares on a network-based Linux server.
- **Network file system (NFS)**: NFS, as presented in Chapter 2, is a framework designed to allow a user on a client workstation to access remotely files over a network on a network-based server.

### Introduction

The Linux+ certified professional needs to have a good understanding of the creation, administration, and management of the Linux filesystem environment. This chapter presents the strategies for the creation of filesystems, the different types of filesystems, the tools used to create filesystems, and the tools used to administer filesystems.

### Filesystem Types

The computer architecture is comprised of many critical components. In Chapter 2, we discussed many of those critical components (for example, hardware, disk drive, and partition) during the installation of the Linux distribution. For this section, we will discuss Linux filesystem types in greater detail. A filesystem provides the operating system with a framework [a structure] for the storage, organization, modification, removal, and retrieval of digital information.

To achieve this objective, filesystems are responsible for organizing and maintaining files, folders, metadata, and residual data as containers for storing digital information. Regardless of the selected filesystem type, data containers can be as large as terabytes (TB) in size or as small as a sector. The size of a sector can vary among the different filesystem types; it is the smallest amount of disk space that can be assigned to hold a file. The default size of sector is typically 512 bytes.

Each form of data is described below:

- **Files** are sectors of allocated space within a filesystem used for storing digital information, which is available to access or execute. The allocated space can be contiguous or noncontiguous. To identify files, files are assigned a filename, which is identified by a sequence of alphanumerical and/or Unicode character sets. In some cases, while not mandatory, a filename can include a dot followed by a series of alphanumerical and/or Unicode character sets (for example, `report.doc`, `budget.xls`) that function as extensions. There are four different types of files within the Linux environment. The four types of files are regular, links, first-in first-out, and sockets.
- **Directories** (also known as *folders*) are sectors of allocated space within a filesystem used to group files. This association is performed and maintained within a File Allocation Table (FAT). To identify directories, directories are assigned a directory name, which is identified by a sequence of alphanumeric and/or Unicode character sets. In addition to having names, directories have structures that can be flat or hierarchical. In case of hierarchical structures, directories can contain subdirectories.
- **Metadata** is forms of data used by the operating system to further characterize files and folders. Typically, some form of indexing file is created and used. The indexing information can contain the file size, the file date and time stamp, sector location, and information pertaining to access permission and device type. The type and amount of metadata created and maintained vary among file systems. In addition, metadata can also include backup copies of files and folders for redundancy purposes. This can even include backup copies of metadata files.
- **Residual data** is a form of data remaining within the filesystem after the file, filename, folder, and folder name relationship has been severed. This typically occurs after deleting a file or folder. Residual data can vary in size. It can be as small as a sector (this is known as *slack space*). *Slack space* is any residual data remaining on a disk not currently associated with any particular file. It is the space remaining after the last byte of a file and the first byte of the next sector.

For the various different types of filesystems, the storage containers (also known as *storage media types*) can reside on many different storage devices. The storage devices can house static and dynamic generated data. As a result, different filesystem structures exist for the different types of containers. Not all operating systems provide support for the various storage containers. The Linux operating system supports a vast number of storage media types, as shown in Figure 3.1.

Listed below are descriptions of each of the storage media types:

- The *hard disk storage media* type, the most common, is used for the storing of data on hard disk drives. This type of storage device can be connected directly (known as an *internal disk drive*) or indirectly (known as an *external disk drive*) to a computer system. This form of filesystem storage is also known as *local filesystem storage*. This model
