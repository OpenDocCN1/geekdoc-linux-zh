
the partitions that are attached to them. An example: given a partition that holds the following directories:

```
videos/ cd-images/ pictures/
```

We want to attach this partition in the filesystem in a directory called /opt/media. In order to do this, the system administrator has to make sure that the directory /opt/media exists on the system. Preferably, it should be an empty directory. How this is done is explained later on in this chapter. Then, using the **mount** command, the administrator can attach the partition to the system. When you look at the content of the formerly empty directory /opt/media, it will contain the files and directories that are on the mounted medium (hard disk or partition of a hard disk, CD, DVD, flash card, USB or other storage device).

During system startup, all the partitions are thus mounted, as described in the file /etc/fstab. Some partitions are not mounted by default, for instance if they are not constantly connected to the system, such like the storage used by your digital camera. If well configured, the device will be mounted as soon as the system notices that it is connected, or it can be user-mountable, i.e. you don’t need to be a system administrator to attach and detach the device to and from the system. There is an example in Section 9.3.

On a running system, information about the partitions and their mount points can be displayed using the df command (which stands for disk full or disk free). In Linux, df is the GNU version, and supports the -h or human readable option which greatly improves readability. Note that commercial UNIX machines commonly have their own versions of **df** and many other commands. Their behavior is usually the same, though GNU versions of common tools often have more and better features.

The df command only displays information about active non-swap partitions. These can include partitions from other networked systems, like in the example below where the home directories are mounted from a file server on the network, a situation often encountered in corporate environments.

```
Freddy:~> df -h
Filesystem Size Used Avail Use% Mounted on
/dev/hda8 496M 183M 288M 39% /
/dev/hda4 8.4M 109M 8% /boot
/dev/hda5 19G 15G 2.7G 85% /opt
/dev/hda6 7.0G 5.4G 1.2G 81% /usr
/dev/hda7 3.7G 2.7G 867M 77% /var
fs1:/home 8.9G 3.7G 4.7G 44% //automount/fs1/root/home
```

## 3.1.3 More file system layout

### 3.1.3.1 Visual

For convenience, the Linux file system is usually thought of in a tree structure. On a standard Linux system you will find the layout generally follows the scheme presented below.

![](img/996aa590a5237ef824c7c29efdbb64f8_61_0.png)

This is a layout from a RedHat system. Depending on the system admin, the operating system and the mission of the UNIX machine, the structure may vary, and directories may be left out or added at will. The names are not even required; they are only a convention.

The tree of the file system starts at the trunk or *slash*, indicated by a forward slash (/). This directory, containing all underlying directories and files, is also called the *root* directory or “the root” of the file system.

Directories that are only one level below the root directory are often preceded by a slash, to indicate their position and prevent confusion with other directories that could have the same name. When starting with a new system, it is always a good idea to take a look in the root directory. Let’s see what you could run into:

```
emmy:~$ cd /
emmy:/> ls
bin/   dev/  home/   lib/    misc/  opt/   root/  tmp/  var/
boot/  etc/  initrd/ lost+found/  mnt/  proc/  sbin/  usr/
```

| Directory | Content |
| :--- | :--- |
| /bin | Common programs, shared by the system, the system administrator and the users. |
| /boot | The startup files and the kernel, vmlinuz. In some recent distributions also grub data. Grub is the GRand Unified Boot loader and is an attempt to get rid of the many different boot-loaders we know today. |
| /dev | Contains references to all the CPU peripheral hardware, which are represented as files with special properties. |
| /etc | Most important system configuration files are in /etc, this directory contains data similar to those in the Control Panel in Windows |
| /home | Home directories of the common users. |
| /initrd | (on some distributions) Information for booting. Do not remove! |
| /lib | Library files, includes files for all kinds of programs needed by the system and the users. |
| /lost+found | Every partition has a lost+found in its upper directory. Files that were saved during failures are here. |
| /misc | For miscellaneous purposes. |
| /mnt | Standard mount point for external file systems, e.g. a CD-ROM or a digital camera. |
| /net | Standard mount point for entire remote file systems |
| /opt | Typically contains extra and third party software. |
| /proc | A virtual file system containing information about system resources. More information about the meaning of the files in proc is obtained by entering the command man proc in a terminal window. The file proc.txt discusses the virtual file system in detail. |
| /root | The administrative user's home directory. Mind the difference between /, the root directory and /root, the home directory of the root user. |
| /sbin | Programs for use by the system and the system administrator. |
| /tmp | Temporary space for use by the system, cleaned upon reboot, so don't use this for saving any work! |
| /usr | Programs, libraries, documentation etc. for all user-related programs. |
| /var | Storage for all variable files and temporary files created by users, such as log files, the mail queue, the print spooler area, space for temporary storage of files downloaded from the Internet, or to keep an image of a CD before burning it. |

Table 3.2. Subdirectories of the root directory

How can you find out which partition a directory is on? Using the df command with a dot (.) as an option shows the partition the current directory belongs to, and informs about the amount of space used on this partition:

```
sandra:/lib> df -h .
Filesystem  Size Used Avail Use% Mounted on
/dev/hda7    980M 163M 767M 18% /
```

As a general rule, every directory under the root directory is on the root partition, unless it has a separate entry in the full listing from df (or df -h with no other options).

Read more in man hier.

### 3.1.3.2 The file system in reality

For most users and for most common system administration tasks, it is enough to accept that files and directories are ordered in a tree-like structure. The computer, however, doesn't understand a thing about trees or tree-structures.

Every partition has its own file system. By imagining all those file systems together, we can form an idea of the tree-structure of the entire system, but it is not as simple as that. In a file system, a file is represented by an inode, a kind of serial number containing information about the actual data that makes up the file: to whom this file belongs, and where is it located on the hard disk.

# Chapter 3: About files and the file system

Every partition has its own set of inodes; throughout a system with multiple partitions, files with the same inode number can exist.

Each inode describes a data structure on the hard disk, storing the properties of a file, including the physical location of the file data. When a hard disk is initialized to accept data storage, usually during the initial system installation process or when adding extra disks to an existing system, a fixed number of inodes per partition is created. This number will be the maximum amount of files, of all types (including directories, special files, links etc.) that can exist at the same time on the partition. We typically count on having 1 inode per 2 to 8 kilobytes of storage.

At the time a new file is created, it gets a free inode. In that inode is the following information:

- Owner and group owner of the file.
- File type (regular, directory, ...)
- Permissions on the file Section 3.4.1
- Date and time of creation, last read and change.
- Date and time this information has been changed in the inode.
- Number of links to this file (see later in this chapter).
- File size
- An address defining the actual location of the file data.

The only information not included in an inode, is the file name and directory. These are stored in the special directory files. By comparing file names and inode numbers, the system can make up a tree-structure that the user understands. Users can display inode numbers using the *-i* option to ls. The inodes have their own separate space on the disk.

## 3.2 Orientation in the file system

### 3.2.1 The path

When you want the system to execute a command, you almost never have to give the full path to that command. For example, we know that the ls command is in the /bin directory (check with **which -a ls**), yet we don't have to enter the command **/bin/ls** for the computer to list the content of the current directory.

The PATH environment variable takes care of this. This variable lists those directories in the system where executable files can be found, and thus saves the user a lot of
