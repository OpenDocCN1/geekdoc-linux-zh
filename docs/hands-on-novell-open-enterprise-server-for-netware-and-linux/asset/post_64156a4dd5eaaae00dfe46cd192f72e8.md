
# Managing Linux Applications

To support users and manage the Linux server, you need to know how Linux works with applications. In this section, you learn how run levels are used to start the Linux server and how software packages can be added with the RedHat Package Manager (RPM) and YaST.

## Working with Run Levels

Run levels determine the startup environment for a system and can be configured from the command line or in the YaST utility. Run level 5 includes graphical support through the **X-Window** interface, which other software packages, such as the KDE and Gnome desktops, draw on. Table 13-6 lists the run levels defined in SUSE Linux.

**Table 13-6** SUSE Linux run level options

| Run Level | Description |
| :--- | :--- |
| 0 | System wait |
| 1 | Single user mode |
| 2 | Local multiuser without remote network |
| 3 | Full multiuser with network |
| 4 | Free |
| 5 | Full multiuser with network and X-Window |
| 6 | System restart |

The simplest way to manage run levels is with the YaST Runlevel Editor (see Figure 13-13). In the following activity, you have an opportunity to practice using it.

![](img/840007e8f98ea6653e5877e945c27dc6_550_0.png)

**Figure 13-13** The YaST Runlevel Editor

## Activity 13-5: Manage Run Levels in YaST

**Time Required:** 10 minutes

**Objective:** Use YaST to manage SUSE Linux run levels.

**Requirements:** Access to the root password

**Description:** Eric thinks that changing run levels when troubleshooting the Linux system could be useful and wants to know what options are available in YaST. In this activity, you use YaST to work with the available run level options.

1. If necessary, log in to your SUSE Linux server with your user name and password.
2. Start the YaST utility and enter the password for your root account.
3. In the left pane, click the System icon, and then check the Runlevel Editor option in the right pane.
4. Click the Expert Mode option button and record the default run level:

   _________________________
5. Click the Set default runlevel after booting to list arrow, and record the run level options:

   _________________________
6. Click the Back button twice to return to the YaST System menu.
7. Exit YaST, and stay logged in for the next activity.

## RPM Package-Related Operations

Installing applications can require a number of steps, such as determining what support modules an application needs, decompressing software modules, performing the actual installation procedure, and then testing the application. Just as Windows has wizards to help with installation procedures, Linux offers several software package tools to help administrators install applications. The application tool that Linux administrators use most often is RedHat Package Manager (RPM). RPM has the following features that make it an excellent software package manager:

- **Noninteractive, scriptable installations**—Provides a set of tools you can use to perform scriptable installations of software packages.
- **Verification of correct installation**—Includes several methods for verifying installed files so that administrators can verify that software is installed correctly and hasn’t been modified since installation.
- **Dependency tracking**—With this feature, administrators can determine whether additional updates or modules need to be installed on the Linux server before installing the package.
- **Digitally signed packages**—Allows all packaged software to be digitally signed using public key technology, so that you can verify the authenticity of software and help prevent installation of Trojan programs.

To use RPM to install a software package, first copy the package to a temporary work directory in the Linux file system. RPM software packages have a name in the following format: `name-version-release.architecture.rpm`. Each part of the RPM name describes the package component:

- **Name**—Indicates the software packaged in the .rpm file
- **Version**—Version number not required but can be used in the .rpm file
- **Release**—An optional component that specifies the revision of the version number
- **Architecture**—Indicates the computer platform the software package is written for; typical values include the following:
    - **i686**: The package can be used on any Pentium class or higher 32-bit CPU; default value for SUSE Linux.
    - **i686**: The package can be used on any 686-class 32-bit Intel-compatible CPU.
    - **noarch**: The package doesn’t contain binary code.
    - **nosrc**: The package contains code and no source is available.
    - **src**: The package contains items such as the source code, patches, and spec file you need to build a binary package.

After you copy the file to a work directory, you can use the `cd` command to change to the directory and then use the `rpm package_name.rpm` command. You can also install rpm packages from a graphical interface by using YaST. In Appendix B, you have the opportunity to practice using the YaST utility and rpm command to install packages, such as ifolder.

# Managing the File System

In Chapter 12, you learned how a disk is partitioned during Linux installation into boot, swap, and root partitions. The OS uses the boot and swap partitions for starting the computer and swapping memory pages to disk, and the root partition (represented by the / character) is used to store the OS software, applications, and data. In addition, the root partition is used as the starting place for the entire file system structure. All file systems on disk partitions, CDs, and other storage devices (even on other computers) are accessed from the root partition instead of with drive letters, as in the Windows OS. Partitions form disk areas that can be formatted and managed with a file system, as described in the following section. A disk can have up to four partitions, one of which can be an extended partition. A Linux extended partition can be used to create other "logical" partitions, thereby allowing you to have as many partitions as needed on a single disk drive.

## Linux File Systems

A partition sets the physical disk area and size, but a disk partition must be formatted with a file system to be used by the operating system. File systems also provide a means of storing and retrieving data from a disk partition. Common file systems in the Windows world include FAT16, FAT32, and NTFS.

Linux file systems can be classified as traditional or journaling. **Journaling file systems**, such as NTFS and Novell Storage Services (NSS), keep a log of data transactions applied to a disk partition. Keeping a transaction log enables the OS to back up incomplete transactions in the event of a system crash, thereby preserving the integrity of the file system's data. Journaling file systems are more fault tolerant; the traditional FAT and FAT32 often have problems and have to be rebuilt following a system crash. A powerful feature of Novell OES SUSE Linux is its capability to use the NSS file system (discussed in more detail in Chapter 14). Tables 13–7 and 13–8 describe the traditional and journaling file systems supported by SUSE Linux.

**Table 13–7** Traditional file systems supported by SUSE Linux

| File System | Description |
| :--- | :--- |
| minix | The first file system supported by Linux is fairly limited compared to other file systems and is no longer in general use. |
| MS-DOS VFAT | The original DOS/Windows 9x file system with support for long file names can be mounted by Linux systems. |
| ext2 | This inode-based file system most commonly used with Linux has been available for many years and is easily converted to ext3. By design, ext2 is almost as fast as ReiserFS (see Table 13–8) and isn't prone to fragmentation. Because Linux doesn't crash often, the lack of journaling in this file system hasn't been a major problem. |

**Table 13–8** Journaling file systems supported by SUSE Linux

| File System | Description |
| :--- | :--- |
| ext3 | Enhanced journaling version of the ext2 file system. |
| ReiserFS | First included in the official Linux kernel in January 2001, this high-speed system can handle a large number of small files efficiently. |
| NTFS | This Windows NT/Server 2003 file system is designed to be more robust and secure than MS-DOS VFAT. |
| NSS | Novell's main file system uses logical volumes and storage pools to store data on disk partitions. It uses Novell's access rights to provide file system security and can be mounted on SUSE Linux systems by using the Enterprise Volume Management System and installing .rpm files. |

![](img/840007e8f98ea6653e5877e945c27dc6_552_0.png)
