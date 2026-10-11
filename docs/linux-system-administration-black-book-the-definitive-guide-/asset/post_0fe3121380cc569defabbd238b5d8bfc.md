
![](img/e612d46dba3c9205aa19fee9eb8dd0a4_91_0.png)

Figure 3.1 A device with an unmapped ext2 file system.

Individual data blocks are organized into block groups within the file system. File system integrity is a primary reason for using groups of blocks instead of just one large set of blocks. If all the data blocks exist in a mass, then damage in one critical area harms everything. Block groups not only break the data blocks into neighborhoods, they also provide for information resiliency and redundancy.

## Mapping The ext2 File System

Linux must be able to sort out which data blocks contain which files or file segments. If data continues onto another block, there is also the issue of how many there are in total, and in what order the data blocks should be read. All this information is contained within a file system object called an inode, which stores the following facts about a file or object:

- The type of object defined by the inode. Object types are: devices (block or character), directories, pipes, files, or symbolic links.
- The item’s permissions.
- The owner and group for the item.
- How large the item is, listed in bytes.
- When the item was created.
- When the item was last changed.
- Pointers to where the item is physically located on the device. If this item is a file that takes up more than one data block, then the location of all the blocks and the order in which they should be accessed is listed.

An inode is named with a number that is unique within the partition or device it resides on. There is no requirement that particular inodes must go into particular block groups. However, block groups always contain the same blocks, even if the information within them changes. Figure 3.2 shows an example of how an inode might relate to a file system.

For mapping purposes, only block group 0's information is important. This factor exists because every block group has a copy of every other block group's information.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_92_0.png)

As long as block group 0 is not damaged, all is fine. If it is damaged, the file system repair programs can glean the data from the other block groups.

## The Superblock

A special block contains information about the overall file system, rather than its components. This segment is called the *superblock* and is available for you to look at with the **dumpe2fs** command. Some of the data contained within the superblock includes:

- How many total inodes and blocks are on the file system.
- How many blocks are not in use.
- How many inodes are not in use.
- How large an individual data block is. This value is typically 1,024 bytes.
- How many blocks make up a block group.
- How many times the file system has been mounted.
- How many times the file system can be mounted before a file system check is forced.
- Which block group this copy of the superblock is stored in.

Every block group contains a copy of the superblock for redundancy purposes. As with block group data, the copy of the superblock in block group 0 is the only one that is used in a healthy file system.

## Making Sense Of The Linux File System

As a system administrator, it is important to understand the file system at a far deeper level than the average user needs to. Users only really need to know some of the basics, such as how to add to their own home directories, and often they do not entirely understand the intricacies of permissions. If a system administrator does not understand such things, the entire machine may either have compromised security or be hampered in its day-to-day functioning.

### The File System Hierarchy Standard

There seems to be an unending march of new flavors of Unix. Not only do new Linux distributions come out on a regular basis, but there is also FreeBSD and a number of commercial Unix variants. Companies that want to put out software that works on Unix and its cousins have found it increasingly difficult to develop code that easily installs across Unix flavors and even across Linux variants.

The first response to this issue resulted in the Linux File System Standard (FSSTND), completed in 1994. This standard lays out the directories that should exist in a Linux file system and how they should be utilized. The goal was to make it possible for developers to write for Linux in general without having to worry about which distribution the software would go onto, and hence strengthen the Linux operating system as a market force. In some ways this goal was reached, as there is general agreement over where many types of files should go. In other ways, however, it was not. For example, almost all distributions have different ways of managing their boot time networking information. As long as the differences remain minimal and can be dealt with by reading environment variables or looking in known locations, then the spirit of the goal is still intact.

> **TIP:** For more on the FSSTND, see www.pathname.com/fhs/1.2/fssstd-toc.html.

A natural outgrowth of the FSSTND was to look at making it easier for developers to target their applications to more than one flavor of Unix at a time. From this desire grew the File System Hierarchy Standard (FHS). This standard aims to serve more than the Linux community. All of Unix is encompassed within it, as far as where particular types of data and binaries should reside on any Unix file system. Table 3.1 explains where you should find particular types of files according to the FHS.

### Table 3.1 Unix file system layout according to the FHS.

| Location | Contains |
| :------- | :----------------------------------------------- |
| bin | Binaries that are necessary for the basic running of the system, as well as system rescue |
| boot | Unchanging files required to boot the machine before the kernel takes over |
| dev | Device driver files |
| etc | Configuration files, plus files that only apply to the host in question |
| home | User home directories |
| lib | Libraries, shared libraries, and kernel modules |
| mnt | Mount point for those file system devices you only mount temporarily |
| opt | Add-on packages that are otherwise not necessary for the system to function |
| root | The superuser's home directory |
| sbin | Binaries used for system administration purposes |
| tmp | Space for programs that need to create temporary files |
| usr | A read-only hierarchy containing files that can be shared among machines, except for the X subdirectories contained within |
| var | Data files that regularly change. This portion of the file system is important to back up regularly, because it sees a lot of use and is subject to wear and tear. |

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_94_0.png)

**TIP:** For more on the FHS, see www.pathname.com/fhs.

## Demystifying Permissions

File permissions are of utmost importance for a system administrator. If they are incorrectly set, they can wreak havoc with your system. Even worse, a tendency to be lax with permissions on a system that is accessible from the Internet or has a lot of users is dangerous on the security front.

### What *Permissions Are*

Permissions control who has read, write, and execution access on file system items (files, directories, and more). This control is broken down into different segments of the user population in order to offer a more refined approach to who can get to what.

### How *Permissions Are Broken Down*

File system permissions are broken down into three sets of three. In order, these sets refer to the owner's permissions, the group's permissions, and everyone else's permissions. Each set of three is structured identically, though the contents may differ. The individual parts are bits, and so are either on or off. The first bit determines whether the person can read the file or look in the directory, the second identifies whether the person can write to the file or directory, and the third specifies whether the person can execute the item. When a bit is on, it is represented by its appropriate letter:

- r for read
- w for write
- x for executable

When it is off, it is a dash. So for a binary where the owner has full access, everyone in the group has read and execution access, and all other users have only read access, the permissions would be rwxr-xr-.

### Permissions By Numbers

It can be cumbersome to have to type out all nine characters of a permission set when you want to make changes quickly. There is another way of writing permissions that involves calculating the bit value of each triad.

Once again, break down the permissions into three sets of three, and consider the sets individually. Having one of the permission bits on adds to the value of the set:

- Read permission adds four
- Write permission adds two
- Execution permission adds one
