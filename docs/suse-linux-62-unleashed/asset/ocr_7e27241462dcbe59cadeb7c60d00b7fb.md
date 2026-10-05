# Editing /etc/fstab Manually

The filesystem table /etc/fstab is a text file; it is designed to have a specific format that is readable by humans and not just computers. It is separated into columns by tabs or spaces. (It doesn't matter which you use.) You can edit it with your favorite text editor; it doesn't matter which. You must take care, however, if you modify it by hand removing or corrupting an entry will make the system unable to mount that filesystem the next time it boots. For this reason, I make a point of saving previous versions of this file using the Revision Control System (a very useful program; see the manual page for rcs).

A sample /etc/fstab looks like the following:

```
/dev/hda6      swap            defaults 0 0
/dev/hda1               ext2             1 1

/dev/hdc       cdrom           iso9660        ro,noauto,user 0 0
/dev/fd0       /floppy         auto            noauto,user 0 0
none            proc            defaults 0 0
# End of YaST-generated fstab lines
```

The first line is for the Linux swap partition, which uses /dev/hda6 for virtual memory. The second line shows that this system has a single root filesystem, residing on the /dev/sda partition. Following this is the table entry for the system's CD-ROM drive, /dev/hdc, which will be mounted at /cdrom. When Linux is booted, the root filesystem is mounted first; all the local (that is, non-network) filesystems are mounted next. Filesystems appear in /etc/fstab in the order they are mounted. If you split your Linux system across various partitions, /usr must appear before /usr/src, for example, because the mount point for CD-ROM and floppy are removable, and they have the noauto option so that they are not automatically mounted at boot. They also have the user option set so that anyone can mount and unmount them having to use su. As you can see, the CD-ROM filesystem type iso9660, which is standard, while the floppy drive has the filesystem type vfat (useful for interchanging data with MS-DOS and Windows systems).

The last filesystem is unique; it (/proc) is a special filesystem provided by the kernel as a way of providing information about the system to user programs. The information in /proc filesystem is used by utilities like ps, top, xlabel, netstat, and so on. Some of the "files" in /proc are real enormous (for example, /proc/kcore). Don't worry, disk space is wasted. All the information in the /proc filesystem is generated on-the-fly by the Linux kernel as you read it. You can tell them they are not real files because, for example, root can't give them away with clown.