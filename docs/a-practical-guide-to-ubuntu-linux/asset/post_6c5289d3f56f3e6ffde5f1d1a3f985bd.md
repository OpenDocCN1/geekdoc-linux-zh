
# BLOCK AND CHARACTER DEVICES

This section describes typical device drivers. Because device drivers can be changed to suit a particular purpose, the descriptions in this section do not pertain to every system.

A block device is an I/O (input/output) device that has the following characteristics:

- Able to perform random access reads
- Has a specific block size
- Handles only single blocks of data at a time
- Accepts only transactions that involve whole blocks of data
- Able to have a filesystem mounted on it
- Has the Linux kernel buffer as its input and output

Block devices commonly found on a Linux system include hard disks, floppy disks, and CDs.

A character device is any device that is not a block device. Examples of character device include printers, terminals, tape drives, and modems.

The device driver for a character device determines how a program reads from and writes to that device. For example, the device driver for a terminal allows a program to read the information you type on the terminal in two ways. First, a program can read single characters from a terminal in *raw* mode—that is, without the driver doing any interpretation of the characters. (This mode has nothing to do with the raw device described in the following section.) Alternatively, a program can read one line at a time. When a program reads one line at a time, the driver handles the erase and kill characters so the program never sees typing mistakes that have been corrected. In this case, the program reads everything from the beginning of a line to the return that ends the number of characters in a line can vary.

# RAW DEVICES

Device drivers for block devices usually have two entry points so they can be used in two ways: as block devices or as character devices. The character device of a block device is called a *raw device*. A raw device is characterized by

- Direct I/O (no buffering through the Linux kernel).
- One-to-one correspondence between system calls and hardware requests.
- Device-dependent restrictions on I/O.

An example of a utility that uses a raw device is *fsck*. It is more efficient for *fsck* to operate on the disk as a raw device rather than being restricted by the fixed size of blocks in the block device interface. Because it has full knowledge of the underlying

| Filesystem | Features |
| --- | --- |
| adfs | Advanced Disc Filing System. Used on Acorn computers. The word *Advanced* differentiated this filesystem from its predecessor DFS, which did not support advanced features as hierarchical filesystems. |
| affs | Amiga Fast Filesystem (FFS). |
| autofs | Automounting filesystem (page 792). |
| cifs | Common Internet Filesystem (page 1141). Formerly the Samba Filesystem (**smbfs**). |
| coda | CODA distributed filesystem (developed at Carnegie Mellon). |
| devpts | A pseudfilesystem for pseudoderminals (page 490). |
| ext2 | A standard filesystem for Ubuntu systems, using the **ext4** extension. |
| ext3 | A journaling (page 1155) extension to the **ext2** filesystem. It greatly improves recovery time from crashes (it takes a less time to run fsck), promoting increased availability. With any filesystem, a journaling filesystem can lose data during a system crash or hardware failure. |
| ext4 | An extension to the **ext3** filesystem. It is backward compatible with **ext2/ext3** filesystems and provides improved performance over **ext3** filesystem. |
| GFS | Global Files. GFS is a journaling, clustering filesystem. It enables a cluster of Linux servers to share a common storage pool. |
| hfs | Hierarchical Filesystem. Used by older Macintosh systems. Newer Macintosh systems use **hfs+**. |
| hpfs | High-Performance Filesystem. The native filesystem for IBM's OS/2. |
| jjfs2 | Journaling Flash Filesystem (jfif). A filesystem for flash memory. |
| iso9660 | The standard filesystem for CDs. |
| minix | Very similar to Linux. The filesystem of a small operating system that was written for educational purposes by Andrew S. Tanenbaum (minix3.org). |

# Table 12-1 Filesystems (continued)

| Filesystem | Features |
|---|---|
| msdos | Filesystem used by DOS and subsequent Microsoft operating systems. It does not use mdos for Windows filesystems; it does not read VFAT attributes. |
| ncpfs | Novell NetWare NCP Protocol Filesystem. Used to mount remote files under NetWare. |
| nfs | Network Filesystem. Developed by Sun Microsystems, this protocol allows a computer to access remote files over a network as if the files were local (page 773). |
| ntfs | NT Filesystem. The native filesystem of Windows NT. See .linux-ntfs.org. |
| proc | An interface to several Linux kernel data structures (page 1144) that behaves like a filesystem (page 497). |
| qnx4 | QNX 4 operating system filesystem. |
| reiserfs | A journaling (page 1155) filesystem, based on balanced-tree algorithms. See ext4 for more journaling filesystems. |
| romfs | A dumb, readily filesystem used mainly for RAM disks (page 1168) during installation. |
| smbfs | Samba Filesystem (deprecated). See .cifs. |
| software RAID | RAID implemented in software. Refer to “RAID” on page 40. |
| sysv | System V UNIX filesystem. |
| ufs | Default filesystem under Sun’s Solaris. |
| sysv | System V UNIX filesystem. |
| ufs | Default filesystem under Sun’s Solaris. |
| umsdos | Filesystem used by DOS and subsequent Microsoft operating systems. It does not use mdos for Windows filesystems; it does not read VFAT attributes. |
| ncpfs | Novell NetWare NCP Protocol Filesystem. Used to mount remote files under NetWare. |
| nfs | Network Filesystem. Developed by Sun Microsystems, this protocol allows a computer to access remote files over a network as if the files were local (page 773). |
| ntfs | NT Filesystem. The native filesystem of Windows NT. See .linux-ntfs.org. |
| proc | An interface to several Linux kernel data structures (page 1144) that behaves like a filesystem (page 497). |
| qnx4 | QNX 4 operating system filesystem. |
| reiserfs | A journaling (page 1155) filesystem, based on balanced-tree algorithms. See ext4 for more journaling filesystems. |
| romfs | A dumb, readily filesystem used mainly for RAM disks (page 1168) during installation. |
| smbfs | Samba Filesystem (deprecated). See .cifs. |
| software RAID | RAID implemented in software. Refer to “RAID” on page 40. |
| sysv | System V UNIX filesystem. |
| ufs | Default filesystem under Sun’s Solaris. |
| umsdos | Filesystem used by DOS and subsequent Microsoft operating systems. It does not use mdos for Windows filesystems; it does not read VFAT attributes. |
| ncpfs | Novell NetWare NCP Protocol Filesystem. Used to mount remote files under NetWare. |
| nfs | Network Filesystem. Developed by Sun Microsystems, this protocol allows a computer to access remote files over a network as if the files were local (page 773). |
| ntfs | NT Filesystem. The native filesystem of Windows NT. See .linux-ntfs.org. |
| proc | An interface to several Linux kernel data structures (page 1144) that behaves like a filesystem (page 497). |
| qnx4 | QNX 4 operating system filesystem. |
| reiserfs | A journaling (page 1155) filesystem, based on balanced-tree algorithms. See ext4 for more journaling filesystems. |
| romfs | A dumb, readily filesystem used mainly for RAM disks (page 1168) during installation. |
| smbfs | Samba Filesystem (deprecated). See .cifs. |
| software RAID | RAID implemented in software. Refer to “RAID” on page 40. |
| sysv | System V UNIX filesystem. |
| ufs | Default filesystem under Sun’s Solaris. |
| umsdos | Filesystem used by DOS and subsequent Microsoft operating systems. It does not use mdos for Windows filesystems; it does not read VFAT attributes. |
| ncpfs | Novell NetWare NCP Protocol Filesystem. Used to mount remote files under NetWare. |
| nfs | Network Filesystem. Developed by Sun Microsystems, this protocol allows a computer to access remote files over a network as if the files were local (page 773). |
| ntfs | NT Filesystem. The native filesystem of Windows NT. See .linux-ntfs.org. |
| proc | An interface to several Linux kernel data structures (page 1144) that behaves like a filesystem (page 497). |
| qnx4 | QNX 4 operating system filesystem. |
| reiserfs | A journaling (page 1155) filesystem, based on balanced-tree algorithms. See ext4 for more journaling filesystems. |
| romfs | A dumb, readily filesystem used mainly for RAM disks (page 1168) during installation. |
| smbfs | Samba Filesystem (deprecated). See .cifs. |
| software RAID | RAID implemented in software. Refer to “RAID” on page 40. |
| sysv | System V UNIX filesystem. |
| ufs | Default filesystem under Sun’s Solaris. |
| umsdos | Filesystem used by DOS and subsequent Microsoft operating systems. It does not use mdos for Windows filesystems; it does not read VFAT attributes. |
| ncpfs | Novell NetWare NCP Protocol Filesystem. Used to mount remote files under NetWare. |
| nfs | Network Filesystem. Developed by Sun Microsystems, this protocol allows a computer to access remote files over a network as if the files were local (page 773). |
| ext4 | standard filesystem. It is backward compatible with **ext2/ext3** filesystems and provides improved performance over **ext3** filesystem. |
| GFS | Global Files. GFS is a journaling, clustering filesystem. It enables a cluster of Linux servers to share a common storage pool. |
| hfs | Hierarchical Filesystem. Used by older Macintosh systems. Newer Macintosh systems use **hfs+**. |
| hpfs | High-Performance Filesystem. The native filesystem for IBM's OS/2. |
| jjfs2 | Journaling Flash Filesystem (jfif). A filesystem for flash memory. |
| iso9660 | The standard filesystem for CDs. |
| minix | Very similar to Linux. The filesystem of a small operating system that was written for educational purposes by Andrew S. Tanenbaum (minix3.org). |
| vfat | standard filesystem. |
| msdos | Filesystem used by DOS and subsequent Microsoft operating systems. It does not use mdos for Windows filesystems; it does not read VFAT attributes. |
| ncpfs | Novell NetWare NCP Protocol Filesystem. Used to mount remote files under NetWare. |
| nfs | Network Filesystem. Developed by Sun Microsystems, this protocol allows a computer to access remote files over a network as if the files were local (page 773). |
| ntfs | NT Filesystem. The native filesystem of Windows NT. See .linux-ntfs.org. |
| proc | An interface to several Linux kernel data structures (page 1144) that behaves like a filesystem (page 497). |
| qnx4 | QNX 4 operating system filesystem. |
| reiserfs | A journaling (page 1155) filesystem, based on balanced-tree algorithms. See ext4 for more journaling filesystems. |
| romfs | A dumb, readily filesystem used mainly for RAM disks (page 1168) during installation. |
| smbfs | Samba Filesystem (deprecated). See .cifs. |
| software RAID | RAID implemented in software. Refer to “RAID” on page 40. |
| sysv | System V UNIX filesystem. |
| ufs | Default filesystem under Sun’s Solaris. |
| xfs | A high-performance journaling filesystem. |

# mount: MOUNTS

The mount utility connects directory hierarchies—filesystems—to the Linux directory. The mount command shows the physical device, the mount point, the type of filesystem, and any options when each filesystem was mounted.

A character device is any device that is not a block device. Examples of character device include printers, terminals, tape drives, and modems.

The device driver for a character device determines how a program reads from and writes to that device. For example, the device driver for a terminal allows a program to read the information you type on the terminal in two ways. First, a program can read single characters from a terminal in *raw* mode—that is, without the driver doing any interpretation of the characters. (This mode has nothing to do with the raw device described in the following section.) Alternatively, a program can read one line at a time. When a program reads one line at a time, the driver handles the erase and kill characters so the program never sees typing mistakes that have been corrected. In this case, the program reads everything from the beginning of a line to the return that ends the number of characters in a line can vary.

# RAW DEVICES

Device drivers for block devices usually have two entry points so they can be used in two ways: as block devices or as character devices. The character device of a block device is called a *raw device*. A raw device is characterized by

- Direct I/O (no buffering through the Linux kernel).
- One-to-one correspondence between system calls and hardware requests.
- Device-dependent restrictions on I/O.

An example of a utility that uses a raw device is *fsck*. It is more efficient for *fsck* to operate on the disk as a raw device rather than being restricted by the fixed size of blocks in the block device interface. Because it has full knowledge of the underlying

# BLOCK AND CHARACTER DEVICES

This section describes typical device drivers. Because device drivers can be changed to suit a particular purpose, the descriptions in this section do not pertain to every system.

A block device is an I/O (input/output) device that has the following characteristics:

- Able to perform random access reads
- Has a specific block size
- Handles only single blocks of data at a time
- Accepts only transactions that involve whole blocks of data
- Able to have a filesystem mounted on it
- Has the Linux kernel buffer as its input and output

Block devices commonly found on a Linux system include hard disks, floppy disks, and CDs.

A character device is any device that is not a block device. Examples of character device include printers, terminals, tape drives, and modems.

The device driver for a character device determines how a program reads from and writes to that device. For example, the device driver for a terminal allows a program to read the information you type on the terminal in two ways. First, a program can read single characters from a terminal in *raw* mode—that is, without the driver doing any interpretation of the characters. (This mode has nothing to do with the raw device described in the following section.) Alternatively, a program can read one line at a time. When a program reads one line at a time, the driver handles the erase and kill characters so the program never sees typing mistakes that have been corrected. In this case, the program reads everything from the beginning of a line to the return that ends the number of characters in a line can vary.

# RAW DEVICES

Device drivers for block devices usually have two entry points so they can be used in two ways: as block devices or as character devices. The character device of a block device is called a *raw device*. A raw device is characterized by

- Direct I/O (no buffering through the Linux kernel).
- One-to-one correspondence between system calls and hardware requests.
- Device-dependent restrictions on I/O.

An example of a utility that uses a raw device is *fsck*. It is more efficient for *fsck* to operate on the disk as a raw device rather than being restricted by the fixed size of blocks in the block device interface. Because it has full knowledge of the underlying

| Filesystem | Features |
| --- | --- |
| adfs | Advanced Disc Filing System. Used on Acorn computers. The word *Advanced* differentiated this filesystem from its predecessor DFS, which did not support advanced features as hierarchical filesystems. |
| affs | Amiga Fast Filesystem (FFS). |
| autofs | Automounting filesystem (page 792). |
| cifs | Common Internet Filesystem (page 1141). Formerly the Samba Filesystem (**smbfs**). |
| coda | CODA distributed filesystem (developed at Carnegie Mellon). |
| devpts | A pseudfilesystem for pseudoderminals (page 490). |
| ext2 | A standard filesystem for Ubuntu systems, using the **ext4** extension. |
| ext3 | A journaling (page 1155) extension to the **ext2** filesystem. It greatly improves recovery time from crashes (it takes a less time to run fsck), promoting increased availability. With any filesystem, a journaling filesystem can lose data during a system crash or hardware failure. |
| ext4 | An extension to the **ext3** filesystem. It is backward compatible with **ext2/ext3** filesystems and provides improved performance over **ext3** filesystem. |
| GFS | Global Files. GFS is a journaling, clustering filesystem. It enables a cluster of Linux servers to share a common storage pool. |
| hfs | Hierarchical Filesystem. Used by older Macintosh systems. Newer Macintosh systems use **hfs+**. |
| hpfs | High-Performance Filesystem. The native filesystem for IBM's OS/2. |
| jjfs2 | Journaling Flash Filesystem (jfif). A filesystem for flash memory. |
| iso9660 | The standard filesystem for CDs. |
| minix | Very similar to Linux. The filesystem of a small operating system that was written for educational purposes by Andrew S. Tanenbaum (minix3.org). |

# Table 12-1 Filesystems (continued)

|---|---|---|
| msdos | Filesystem used by DOS and subsequent Microsoft operating systems. It does not use mdos for Windows filesystems; it does not read VFAT attributes. |
| ncpfs | Novell NetWare NCP Protocol Filesystem. Used to mount remote files under NetWare. |
| nfs | Network Filesystem. Developed by Sun Microsystems, this protocol allows a computer to access remote files over a network as if the files were local (page 773). |
| ntfs | NT Filesystem. The native filesystem of Windows NT. See .linux-ntfs.org. |
| proc | An interface to several Linux kernel data structures (page 1144) that behaves like a filesystem (page 497). |
| qnx4 | QNX 4 operating system filesystem. |
| reiserfs | A journaling (page 1155) filesystem, based on balanced-tree algorithms. See ext4 for more journaling filesystems. |
| romfs | A dumb, readily filesystem used mainly for RAM disks (page 1168) during installation. |
| smbfs | Samba Filesystem (deprecated). See .cifs. |
| software RAID | RAID implemented in software. Refer to “RAID” on page 40. |
| sysv | System V UNIX filesystem. |
| ufs | Default filesystem under Sun’s Solaris. |
| umsdos | Filesystem used by DOS and subsequent Microsoft operating systems. It does not use mdos for Windows filesystems; it does not read VFAT attributes. |
| ncpfs | Novell NetWare NCP Protocol Filesystem. Used to mount remote files under NetWare. |
| nfs | Network Filesystem. Developed by Sun Microsystems, this protocol allows a computer to access remote files over a network as if the files were local (page 773). |
| ntfs | NT Filesystem. The native filesystem of Windows NT. See .linux-ntfs.org. |
| proc | An interface to several Linux kernel data structures (page 1144) that behaves like a filesystem (page 497). |
| qnx4 | QNX 4 operating system filesystem. |
| reiserfs | A journaling (page 1155) filesystem, based on balanced-tree algorithms. See ext4 for more journaling filesystems. |
| romfs | A dumb, readily filesystem used mainly for RAM disks (page 1168) during installation. |
| smbfs | Samba Filesystem (deprecated). See .cifs. |
| software RAID | RAID implemented in software. Refer to “RAID” on page 40. |
| sysv | System V UNIX filesystem. |
| ufs | Default filesystem under Sun’s Solaris. |

# mount: MOUNTS

The mount utility connects directory hierarchies—filesystems—to the Linux directory. The mount command shows the physical device, the mount point, the type of filesystem, and any options when each filesystem was mounted.

```
$ mount
/dev/sda1 / type ext4 (rw,remount-ro)
proc /proc type proc (rw,noexec,nosuisid,nodev)
...
/dev/sda2 /home type ext4
/dev/sda5 /p15 type ext4
/dev/sda6 /p16 type ext4
/dev/sda1 /p01 type ext4
/jam/c /jam/c type cifs (rw,mand)
dog/pg04 /p04 type nfs (rw,addr=192.168.0.12)
/dev/hdb /media/cdrom0 type iso9660 (rw,noexec,nosuisid,nodev,user=sam)
```

The first entry in the example shows the root filesystem, which is mounted on /. The second entry shows the /proc pseudfilesystem (page 497). The next four entries identify disk partitions standard ext4 filesystems. The directory /jam/c has a cifs (Windows) filesystem mounted on it using Samba. You can use Linux utilities and applications to access the Windows files and directories. The line starting with dog shows a mounted, remote NFS filesystem. The last line shows the CD at /dev/hdb mounted on /media/cdrom0.

If the list of filesystems in /etc/mtstab is not correct, see the tip on page 494.
