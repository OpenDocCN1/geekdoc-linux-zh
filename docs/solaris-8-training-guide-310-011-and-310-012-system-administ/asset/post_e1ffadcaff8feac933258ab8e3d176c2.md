
## Apply Your Knowledge

C. mkfs

D. format

10. What is not true about logical block sizes?
A. The logical block size is the size of the blocks the Unix kernel uses to read or write files.
B. By default, the logical block size is 8192 bytes.
C. A larger logical block size increases efficiency for file systems in which most of the files are large.
D. A small logical block size increases efficiency for file systems in which most of the files are large.

11. What is the default number of bytes per inode?
A. 2048
B. 1024
C. 8192
D. 64

12. In Solaris, which of the following is referred to as the smallest allocable unit of disk space?
A. Fragment
B. Data block
C. Logical block
D. Byte

13. What is another name for swap space?
A. Virtual memory
B. Random Access Memory
C. Partition C or Slice 2
D. Static memory

14. When should a file system be checked with fsck?
A. If the file system was unmounted properly
B. After a power outage
C. Whenever a file system cannot be mounted
D. When data has been accidentally deleted

15. What does fsck do when it preens a file system?
A. Forces checking of the file system
B. Checks and fixes the file system non-interactively
C. Checks writeable file systems only
D. Only checks to determine if a file system needs checking

16. Which of the following files contains a list of file systems to be automatically mounted at bootup?
A. /etc/fstab
B. /etc/dfs/dfstab
C. /etc/vfstab
D. /etc/rc2.d/S74autofs

17. What does the mountall command do?
A. Mounts the CD-ROM and floppy automatically
B. Mounts all file systems specified in a file system table
C. Shares all files systems so that they can be mounted
D. Mounts the tape in the tape drive

## Apply Your Knowledge

18. What command(s) is/are used to display disk space information?
- A. du
- B. df
- C. quota
- D. repquota
- E. All of the above

19. Which of the following mount options is used to mount file systems that have files larger than 2GB?
- A. largefiles
- B. nolargefiles
- C. lf
- D. nlf

20. What should you do to enable UFS logging on a file system?
- A. Use the -o logging option with the mount command.
- B. Use the -l option with the mount command.
- C. Use the ufslog option with the mount command.
- D. Use the logging feature in the newfs command when creating the file system.

21. Which of the following represents the correct format for an entry in the /etc/vfstab file?
- A. device to mount, device to fsck, mount point, FS type, fsck pass, mount at boot, mount options.
- B. device to fsck , device to mount, mount point, FS type, fsck pass, mount at boot, mount point
- C. mount point, device to mount, device to fsck, mount point, FS type, fsck pass, mount at boot
- D. mount point, device to fsck, device to mount, mount point, FS type, fsck pass, mount at boot

22. Which of the following commands shows you the disk usage of each file in each subdirectory of a file system?
- A. du
- B. df
- C. ls
- D. printenv

23. Which of the following commands displays disk space occupied by mounted file systems?
- A. df
- B. du
- C. ls
- D. printenv

## Apply Your Knowledge

## Answers to Review Questions

1. D. On a standard Solaris file system, a file system cannot span multiple disks or slices. It’s only possible when using virtual file systems (that is, DiskSuite).

2. A. Disk configuration information is stored on the disk label.

3. A. The boot block stores the procedures used in booting the system. Without a boot block, the system does not boot.

4. A. The slice information for a particular disk can be viewed by using the prtvtoc command.

5. A. The following are virtual file systems: swapfs, procfs, lofs, cachefs, tmpfs, /var/run, and mnttfs.

6. D. The format utility is used to retrieve corrupted disk labels, repair defective sectors, format and analyze disks, partition disks, and label disks.

7. D. Here are a few of the more important things contained in a superblock:
- Size and status of the file system
- Label (file system name and volume name)
- Size of the file system’s logical block
- Date and time of the last update
- Cylinder group size
- Number of data blocks in a cylinder group
- Summary data block
- File system state (clean, stable, or active)
- Pathname of the last mount point

8. A., C. An inode contains all of the information about a file except its name, which is kept in a directory. The inode information is kept in the cylinder information block and contains the following:
- The type of the file (regular, directory, block special, character special, link, and so on)
- The mode of the file (the set of read/write/execute permissions)
- The number of hard links to the file
- The user-id of the file’s owner
- The group-id to which the file belongs
- The number of bytes in the file
- An array of 15 disk-block addresses
- The date and time the file was last accessed
- The date and time the file was last modified
- The date and time the file was created

9. B. newfs is the recommended command to create file systems.

10. D. As a general rule, a larger logical block size increases efficiency for file systems in which most of the files are large. Use a smaller logical block size for file systems in which most of the files are small.

11. A. The default number of bytes per inode is 2048 (2KB), which assumes that the average size of each file is 2KB or greater.

12. A. The file system fragment size is the smallest allocable unit of disk space, which is 1,024 bytes.

## Apply Your Knowledge

13. A. Swap space is also referred to as virtual memory.

14. A., B., C. fsck should be run after a power outage, when a file system is unmounted improperly, or whenever a file system cannot be mounted.

15. B. Normally, fsck is run noninteractively at bootup to preen the file systems after an abrupt system. Preening automatically fixes any basic file system inconsistencies and does not try to repair more serious errors. While preening a file system, fsck fixes the inconsistencies it expects from such an abrupt halt. For more serious conditions, the command reports the error and terminates.

16. C. The /etc/vfstab file contains a list of file systems to be automatically mounted when the system is booted to the multiuser state.

17. B. The mountall command mounts all file systems specified in a file system table (vfstab).

18. E. The following commands can be used to display disk space usage: du, df, quota, repquota

19. A. The largefiles mount option lets users mount a file system containing files larger than 2GB.

20. A. Use the -o logging option to the mount command to enable UFS logging on a file system.

21. A. The correct format for the /etc/vfstab file is as follows:
device to mount, device to fsck, mount point, FS type, fsck pass, mount at boot, mount options

22. A. Use the du (directory usage) command to report the number of free disk blocks and files.

23. A. The df command with no options lists all mounted file systems and their device names. It also lists the total number of 512-byte blocks used and the number of files.

## OBJECTIVES

The following test objectives are covered in this chapter:

### Construct a file system
Constructing file systems is a routine task for system administrators. A complete understanding of when to utilize and how to construct each type of file system found in Solaris 8 is required.

### Tune a file system
Solaris provides a method for fine-tuning many of the parameters assigned to file systems. The system administrator needs to understand these parameters and adjust them to achieve optimum performance.

### Use large file systems
Solaris can accommodate applications that will be supporting large files that are larger than 2GB. However, the proper file system parameters must be set to accommodate these large files.

### Use additional options when mounting and unmounting file systems
Each file system type supports many options that control how the file system will function and perform. The system administrator needs to be familiar with all of these options when mounting and unmounting file systems.

### Work with removable media and Volume Manager
Solaris has accommodations for managing removable media, such as removable disk and CD-ROM, via the Volume Manager. The system administrator needs to know how to enable and disable this facility as well as understand the associated configuration files.
