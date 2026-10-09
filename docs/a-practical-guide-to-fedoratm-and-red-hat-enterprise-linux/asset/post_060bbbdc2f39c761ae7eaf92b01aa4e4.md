
(none) option to verify the integrity of a file system; run `xfs_repair` without an option to repair a file system. The following message explains why you must mount the XFS file system to play the changes stored in the log before you repair it. After mounting the file system, unmount it and run `xfs_repair` to repair the file system.

```
# xfs_repair /dev/sdb1
Phase 1 - find and verify superblock...
Phase 2 - using internal log
- zero log...
    ERROR: The file system has valuable metadata changes in a log which needs to
    be replayed.  Mount the file system to replay the log, and unmount it before
    re-running xfs_repair.  If you are unable to mount the file system, then use
    the -L option to destroy the log and attempt a repair.
    Note that destroying the log may cause corruption -- please attempt a mount
    of the file system before doing this.
```

```
# mount /dev/sdb1 /myxfs
# umount /dev/sdb1
# xfs_check /dev/sdb1

# xfs_repair /dev/sdb1
Phase 1 - find and verify superblock...
Phase 2 - using internal log
- zero log...
- scan file system freespace and inode maps...
- found root inode chunk
Phase 3 - for each AG...
- scan and clear agi unlinked lists...
- process known inodes and perform inode discovery...
- agno = 0
- agno = 1
- agno = 2
- agno = 3
- process newly discovered inodes...
Phase 4 - check for duplicate blocks...
- setting up duplicate extent list...
- check for inodes claiming duplicate blocks...
- agno = 0
- agno = 1
- agno = 2
- agno = 3
Phase 5 - rebuild AG headers and trees...
- reset superblock...
Phase 6 - check inode connectivity...
- resetting contents of realtime bitmap and summary inodes
- traversing file system
- traversal finished
- moving disconnected inodes to lost+found ...
Phase 7 - verify and correct link counts...
done
```

**xfs_fsr**	The `xfs_fsr` (file system reorganizer) utility improves the organization of a file on a mounted XFS file system. Give the command `xfs_fsr` followed by the name of the file you want to reorganize.

## CHAPTER SUMMARY

File systems hold directories of files. These structures store user data and system data that are the basis of users' work on the system and the system's existence. Linux supports many types of files, including ordinary files, directories, links, and special files. Special files provide access to operating system features. The kernel uses major and minor device numbers to identify classes of devices and specific devices within each class. Character and block devices represent I/O devices such as hard disks and printers. Inodes, which are identified by inode numbers, are stored on disk and define a file's existence.

When the system comes up, the /etc/fstab file controls which filesystems are mounted and how they are mounted (read-only, read-write, and so on). After a system crash, filesystems are automatically verified and repaired if necessary by fsck. You can use tune2fs to force the system to cause fsck to verify a filesystem periodically when the system boots.

## EXERCISES

- 1. What is the function of the /etc/hosts file? Which services can you use in place of or to supplement the hosts file?
- 2. What does the /etc/resolv.conf file do? What do the nameserver lines in this file do?
- 3. What is an inode? What happens to the inode when you move a file within a filesystem?
- 4. What does the .. entry in a directory point to? What does this entry point to in the root (/) directory?
- 5. What is a device file? Where are device files located?
- 6. What is a FIFO? What does FIFO stand for? What is another name for a FIFO? How does a FIFO work?

## ADVANCED EXERCISES

- 7. Write a line for the /etc/fstab file that mounts the /dev/sdb1 ext4 filesystem on /extra with the following characteristics: The filesystem will not be mounted automatically when the system boots, and anyone can mount and unmount the filesystem.
- 8. Without using rm, how can you delete a file? (Hint: How do you rename a file?)
- 9. After burning an ISO image file named image.iso to a CD on /dev/hdc, how can you verify the copy from the command line?
- 10. Why should /var reside on a separate partition from /usr?
- 11. Create a FIFO. Using the shell, demonstrate that two users can use this FIFO to communicate asynchronously.
- 12. How would you mount an ISO image so you could copy files from it without burning it to a CD?

## 12

## FINDING, DOWNLOADING, AND INSTALLING SOFTWARE

## IN THIS CHAPTER

- JumpStart: Installing and Removing Software Packages Using yum ... 534
- Finding the Package That Holds an Application or File You Need ... 536
- yum: Keeps the System Up-to-Date ... 538
- yum Commands ... 539
- yum.conf: Configures yum ... 541
- BitTorrent: ... 543
- RPM: The RPM Package Manager ... 546
- Keeping Software Up-to-Date ... 552
- curl: Downloads Files Noninteractively ... 553

## OBJECTIVES

After reading this chapter you should be able to:

- Explain the purpose of a software package, a package management system, and a software repository
- List the uses and benefits of yum
- Use yum to list installed and available packages
- Use yum to search for packages containing specific applications or utilities
- Use yum to install and remove a software package
- Use yum to update all software packages on the local system.
- Download large files with BitTorrent
- Use rpm to display information about a package and install software
- List common steps for installing non-RPM software from source

## INTRODUCTION

Linux is based on millions of lines of code and includes thousands of programs. Each of these programs is updated periodically, and most depend on other programs or files to run. The source code for each program must be compiled for each processor architecture and each release of each Linux distribution. With the first releases of Linux, these tasks were done by hand. Over time, this process has been automated. This chapter explains how you can make your life easier by taking advantage of the facilities Fedora/RHEL provides for finding, installing, updating, and removing software.

![](img/243613168ac865b539f12460d966088e_588_0.png)

### Software Package

A *software package*, or simply *package*, is the collection of scripts, programs, files, and directories required to install and run an application, utility, server, or system software. A package also includes a list of other packages the package depends on (*dependencies*). Using software packages makes it easier to install, update, and uninstall software. A package contains either executable files or source code files. Executable files are precompiled for a specific processor architecture and operating system, whereas source files need to be compiled but will run on a wide range of machines and operating systems.

![](img/243613168ac865b539f12460d966088e_588_1.png)

### PMS

A *PMS*, or *package management system*, is a set of utilities that allows you to install, upgrade, remove, and search software packages easily and in a consistent manner. It is based on a local database that holds information about each installed package, including its dependencies and version information.

One of the biggest advantages of a PMS is how easy it makes it to uninstall a package. If you compile from source, a **make install** command typically installs the files, but there is frequently no **make uninstall** command. A PMS keeps track of all the files that belong to a package. These files might be distributed among many directories throughout a system. This tracking allows you to remove all files belonging to a package with a single command. A PMS also enables you to query packages, a great troubleshooting tool that does not come with manual installation. When you manually install a package, you must obtain the source code (again, and in some cases the same version as you installed) to learn which files are a part of the package, what was done during installation, and how to remove the software.

![](img/243613168ac865b539f12460d966088e_588_2.png)

### Software Package Formats

Software packages come in different formats. Fedora/RHEL and SUSE use **RPM** (RPM Package Manager; page 546). Ubuntu and Debian use **dpkg** (Debian package), which was the first Linux packaging system to incorporate dependency information. Other formats include the Gnu Comfigured and Build System (page 550), and compressed **tar**. Formats such as compressed **tar**, which were popular before the introduction of RPM, are used less often today because they require more work on the part of the installer (you) and do not provide the dependency and compatibility checking RPM offers.
