system files. Other filesystems present on hard disks inside the computer can also be mounted to various mount point directories underneath the / directory at boot time, as well as via entries in the filesystem table (/etc/fstab) discussed in the following sections.

The mount command is used to mount devices to mount point directories, and the umount command is used to unmount devices from mount point directories; both of these commands are discussed throughout the remainder of this chapter.

# Working with Floppy Disks

Traditionally, it was commonplace to use floppy disk removable media to store small files, such as spreadsheets, that needed to be transferred from computer to computer. Today, floppy disks are not available on all systems, but we will examine them here as they are an easy way to practice and learn the commands that are commonly used to work with filesystems and they are emulated in virtualization software.

Recall that each disk device must be formatted with a filesystem prior to being used to store files. To do this, you can use the mkfs (make filesystem) command and specify the filesystem type using the -t switch and the device file representing the floppy disk device. To format the floppy disk inside the first floppy disk drive in the computer with the ext2 filesystem, place a floppy disk in the floppy disk drive and type the following command:

```
[root@server1 ~]# mkfs -t ext2 /dev/fd0
mke2fs 1.42.8 (20-Jun-2013)
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
Stride=0 blocks, Stripe width=0 blocks
184 inodes, 1440 blocks
72 blocks (5.00%) reserved for the super user
First data block=1
Maximum filesystem blocks=1572864
1 block group
8192 blocks per group, 8192 fragments per group
184 inodes per group
Allocating group tables: done
Writing inode tables: done
Writing superblocks and filesystem accounting information: done
[root@server1 ~]#
```

Alternatively, you can specify a different filesystem after the -t option, such as the DOS FAT filesystem. This results in a different output from the mkfs command, as shown in the following example:

```
[root@server1 ~]# mkfs -t msdos /dev/fd0
mkfs.msdos 3.0.23 (2013-10-15)
[root@server1 ~]#
```