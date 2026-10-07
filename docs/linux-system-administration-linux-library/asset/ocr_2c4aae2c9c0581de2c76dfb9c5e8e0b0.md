# Chapter 18 Troubleshooting Your Linux System

# Id: Unrecognized Option -qmagic

This message means that you should get a newer linker. The linker is in the binutils RPM or is available as a tarball from http://sources.redhat.com/binutils.

# Filesystem Problems or Questions

The filesystem is covered in great detail in Chapter 10. As a Linux system administrator, the more you know about the ext2 filesystem the better. You should get familiar with the inode concept and the filesystem layout, including the intended uses of the directories off /. Here are a few of the most common filesystem-related questions.

# Creating a Filesystem on a Floppy Disk

To create a filesystem on a 3.5-inch, high-density floppy, issue the following command:

```
# /sbin/mke2fs /dev/fd0
```

The system will reply:

```
mke2fs 1.18, 11-Nov-1999 for EXT2 FS 0.5b, 95/08/09
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
184 inodes, 1440 blocks
72 blocks (5.00%) reserved for the super user
First data block=1
1 block group
8192 blocks per group, 8192 fragments per group
184 inodes per group
```

Writing inode tables: done
Writing superblocks and filesystem accounting information: done

# Creating a Windows Filesystem on a Floppy Disk

To format a 3.5-inch, high-density floppy, you can use this command: