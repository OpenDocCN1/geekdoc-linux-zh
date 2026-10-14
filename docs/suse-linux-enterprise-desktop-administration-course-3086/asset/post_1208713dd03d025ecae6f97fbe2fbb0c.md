
**Novell Customer Center**  An online service that allows access to SUSE Linux updates.

**Novell Customer Center Configuration**  A YaST module used to configure the options and account information used by the Novell Customer Center.

**Online Update**  A YaST module that allows you to install software patches and update your software to the newest versions.

**Package Label**  The information stored within an RPM package that lists general package information.

**Red Hat Package Manager (RPM)**  A format used to distribute software packages on most Linux systems.

**rpm command**  A command used to install, remove, and find information on RPM software packages.

**rug command**  A command used to manage the software update services in SUSE Linux.

**Software Management**  A YaST module that is used to install and manage software packages in SUSE Linux.

**Software Updater**  A desktop utility that can be used to quickly update your SUSE Linux software using Online Update.

## Review Questions
- 1. What must you configure before updating your system with YaST Online Update?
- 2. You want to install a new software application that is not available on your SUSE Linux installation DVD. What can you do to install this new software application? (Choose all that apply.)
  - Download and install the program RPM file for your architecture
  - Request a new installation DVD from the Novell Customer Center
  - Select an alternate installation source in the Software Management module of YaST
  - Use the rpm command to install the software from your installation DVD
- 3. You attempt to run the Software Updater utility in your desktop environment, but you receive the following error message: Could not perform requested action. What is the likely cause of this error message?
- 4. Which of the following is a valid RPM package for version 3.1.6 of the sample program compiled for the i686 architecture?
  - sample-3.1.6-i686.rpm
  - rpm.sample-i686.3.1.6
  - sample-i686(3.1.6).rpm
  - rpm(sample-3.1.6-i686)
- 5. How large can you expect an RPM database to be if the size of your /usr directory is 10GB?
- 6. Which option to the `rpm` command can be used to uninstall an RPM package?
  - a. `u`
  - b. `e`
  - c. `r`
  - d. `x`
- 7. What command will list the files in the installed bash RPM package? ____________________
- 8. Which of the following commands will install an RPM package? (Choose all that apply.)
  - a. `rpm -U packagename`
  - b. `rpm -i packagename`
  - c. `rpm -e packagename`
  - d. `yast -i packagename`

## Discovery Exercises
![](img/9129877170834ca9d5fdac5319bf5f12_201_0.png)

### Installing RPM Software Packages
Use the Internet to find an RPM package that has been compiled for use on SUSE Linux. (Some common Internet resources include http://rpmfind.net/linux/RPM/ and http://rpm.pbone.com.) Next, use the appropriate command to verify that the package has not already been installed. Following this, download the RPM package, install it on your system, and use the appropriate commands to view the files installed and version information. When finished, use the appropriate commands to remove the software package from your system.

### Installing Software Packages from Source
Although most software packages for SUSE Linux are available in RPM format, you can also download and install software from source code that is freely available on the Internet. Use the Internet to find the source code for a program that you do not have installed on your system (the best Internet resources for source code is http://sourceforge.net/). Following this, download the source code (with a .tar.gz or .tgz extension) and extract it using the command `tar --zxvf filename`. Enter the directory that was created and run the following commands to compile and install the software on your system:

```bash
./configure
make
make install
```

Although these steps will work for most source code programs, additional steps might be required. Read the README and INSTALL files in the source code directory to learn more about how to compile and install the program that you have downloaded. When finished, execute your program.

## Configuring Online Update
Provided that you have a valid Novell Customer Center subscription, configure your SUSE Linux server to download the latest updates from the Internet. What updates were applied?

## The Debian Package Manager
Although the Red Hat Package Manager (RPM) is the default package manager used on most Linux systems, an alternative package manager is available and used by default on Linux distributions such as Debian and Ubuntu. Using the Internet, research the features of the Debian Package Manager as compared with the Red Hat Package Manager. Summarize your findings in a short memo.

![](img/9129877170834ca9d5fdac5319bf5f12_204_0.png)

## Manage Directories and Files
**In this section, you learn about the structure of the Linux file system and the most important file operation commands for working at the command line.**

### Objectives
- Objective 1—Understand the File System Hierarchy Standard (FHS)
- Objective 2—Identify File Types in the Linux System
- Objective 3—Change Directories and List Directory Contents
- Objective 4—Create and View Files
- Objective 5—Work with Files and Directories
- Objective 6—Find Files on Linux

## Objective 1—Understand the File System Hierarchy Standard (FHS)
The file system concept of Linux (and, in general, of all UNIX systems) is considerably different than that of other operating systems.

A filename in Linux can be up to 255 characters long. It can contain any number of special characters (“_” or “%”, for example).

Certain special characters (the dollar sign “$”, the semicolon “;”, or the space, for example) have a specific meaning for the command interpreter bash (Bourne Again Shell). If you want to use one of these characters in a filename, you must put a “\\” (backslash) in front of the character to mask (switch off) its special meaning for the bash.

You can also use umlauts, letters with diacritical marks, or other country-specific characters. But if you exchange data with people in other countries using different settings, they can have problems because these characters are not present on their keyboards.

Linux differentiates between uppercase and lowercase letters. For example, Invoice, invoice, and INVOICE identify three different files.

To understand the concept of the Linux file system, you need to know the following:
- The Hierarchical Structure of the File System
- FHS (File System Hierarchy Standard)
- Root Directory (/)
- Essential Binaries for Use by All Users (/bin)
- Boot Directory (/boot)
- Other Partitions (/data)
- Device Files (/dev)
- Configuration Files (/etc)
- User Directories (/home)
- Libraries (/lib)
- Mountpoints for Removable Media (/media/*)
- Application Directory (/opt)
- Home Directory of the Administrator (/root)
- System Binaries (/sbin)
- Data Directories for Services (/srv)
- Temporary Area (/tmp)
- The Hierarchy Below (/usr)
- Variable Files (/var)
- Windows Partitions (/windows)
- Process Files (`/proc`)
- System Information Directory (`/sys`)
- Mountpoint for Temporarily Mounted File Systems (`/mnt`)
- Directories for Mounting Other File Systems

## The Hierarchical Structure of the File System
The file system concept of Linux involves a hierarchical file system that can be depicted in the form of a tree.

This tree is not limited to a local partition. It can stretch over several partitions, which can be located on different computers in a network. It begins at the root, from where the name for the system administrator comes, and branches out like the branches of a tree.

Figure 7-1 is an extract from a typical file system tree.

![](img/9129877170834ca9d5fdac5319bf5f12_206_0.png)

**Figure 7-1**

A file in this directory tree is uniquely defined by its path. A path refers to the directory names that lead to this file.

The separation character between individual directory names is the slash (“/”). The path can be specified in two ways:
- As a *relative path* starting from the current directory
- As an *absolute path* starting from the root of the entire file system tree

The absolute path always begins with a slash (“/”), the symbol for the root directory.
