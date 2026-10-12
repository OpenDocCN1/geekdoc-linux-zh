
only for the system administrator (because it requires read access to the block device underlying the data to be backed up). To back up the entire contents of your home directory to diskettes, you type the following:

```
$ find $HOME -print0 | cpio --create -0 --format=crc > /dev/fd0
```

The -print0 and -0 options for find and cpio ensure that the names of the files to be backed up are separated by ASCII NULLs, rather than newlines. This ensures that any filenames containing a newline are correctly backed up.

> **Note**
> 
> The only characters that are illegal in UNIX filenames are the slash and the ASCII NULL.

Most of the backup utilities for Linux are written specifically to write their backups to any kind of file; in fact, they were designed for sequentially accessed character devices, such as tape drives. See Chapter 22, “Backup and Restore,” for more information about the various backup programs that are available for Linux.

## Filesystems

When you have more than one item of data, it is necessary to have some method of organizing files on the block device. These methods are called *filesystems*. Linux enables you to choose any organizational method to marshal your files on its storage device. For example, you can use the MS-DOS filesystem on a diskette or the faster ext2 filesystem on your hard disk.

Many different filesystems are supported by Linux; the ext2 filesystem is the most used because it is designed for Linux and is very efficient. Other filesystems are used for compatibility with other systems; for example, it's common to use the msdos and vfat filesystems on diskettes; these are the native filesystems of MS-DOS and Windows 95. Under Red Hat Linux 7, some filesystems are built in to the kernel:

```
$ cat /proc/filesystems
    ext2
nodev proc
    iso9660
nodev devpts
```

Some filesystems are available as loadable modules:

```
$ ls -x /lib/modules/`uname -r`/fs
```

autofs.o          binfmt_aout.o     binfmt_java.o     binfmt_misc.o
coda.o            fat.o             hfs.o             hpfs.o
lockd.o          minix.o           msdos.o           ncpfs.o
nfs.o            nfsd.o            nls_cp437.o       nls_cp737.o
nls_cp775.o      nls_cp850.o       nls_cp862.o       nls_cp865.o
nls_cp867.o      nls_cp869.o       nls_cp861.o       nls_cp866.o
nls_cp863.o      nls_cp864.o       nls_cp865.o       nls_cp869.o
nls_cp874.o      nls_cp922.o       nls_cp936.o
nls_cp949.o      nls_cp950.o       nls_iso8859-1.o   nls_iso8859-14.o
nls_iso8859-15.o nls_iso8859-2.o   nls_iso8859-3.o   nls_iso8859-4.o
nls_iso8859-5.o  nls_iso8859-6.o   nls_iso8859-7.o   nls_iso8859-8.o
nls_iso8859-9.o  nls_koi8-r.o      romfs.o           smbfs.o
sysv.o           ufs.o             umsdos.o          vfat.o

Some of these (nfs, ncpfs, and smbfs) are network filesystems that don’t depend on block devices. Network filesystems are covered in Chapter 16 “NFS: Network Filesystem” and Chapter 17, “Samba.” Other filesystems are supported by Linux but are not provided by the standard kernel.

## The mount Command

Use the mount command to mount a block device onto the filesystem. You need to specify what device contains the filesystem, what type it is, and where in the directory hierarchy to mount it.

A mount command looks like this:

```
mount -t type -o options device mount-point
```

device should either be a block device or if it contains a colon it can be the name of another machine from which to mount a filesystem (see Chapter 16). The mount-point should be an existing directory (or you get an error); the filesystem will appear at this position. (Anything previously in that directory will be hidden.) The filesystem type and options are optional, and the variety and meaning of options depend on the type of filesystem being mounted. If the filesystem you want to mount is specified in the /etc/fstab file, you need to specify only the mount point or the device name; the other details are read from /etc/fstab by mount.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_618_0.png)

When you are browsing the filesystem, it is not always easy to quickly see the difference between an empty device and a mount point on which no device has been mounted. A good way to make this simpler is to create a file called filesystem not mounted in each directory that is to serve as a mount point. You will then immediately see whether or not there is a device mounted on the mount point.

Here is an example of the mount command being used:

```
# ls /mnt/floppy
filesystem not mounted
# mount -t vfat /dev/fd1 /mnt/floppy
mount: block device /dev/fd1 is write-protected, mounting read-only
# ls /mnt/floppy
grub-0.4.tar.gz
# umount /mnt/floppy
# ls /mnt/floppy
filesystem not mounted
```

In this example, I listed the files in my /mnt/floppy mount point. I saw that no diskette was mounted, so I mounted a diskette containing a vfat filesystem at the mount point. I got an informational message telling me that the diskette was write-protected; if the diskette had not been write-protected, there would have been no message. The directory /mnt/floppy already existed. I used ls to see what was on the disk and unmounted it again using the umount command. I then ran ls again, and the response I got was simply the name of a file that I leave in the directory /mnt/floppy on my hard disk to remind me that there currently is nothing mounted there. This hint enables me to distinguish a written diskette from an empty diskette that is mounted. You can also use the df command to see what filesystems are mounted. For example:

```
# mount -t vfat /dev/fd0 /mnt/floppy
# df /mnt/floppy
Filesystem           1k-blocks     Used Available Use% Mounted on
/dev/fd0                1423        0      1423   0% /mnt/floppy
# umount /mnt/floppy
# df /mnt/floppy
Filesystem           1k-blocks     Used Available Use% Mounted on
/dev/hda6              202006   1850753    72493  96% /
```

As you see from the example, when a device is mounted on a mount point, df will output statistics for that device; otherwise it will output statistics about the device upon which the directory resides.

Mounting a vfat diskette as we did earlier causes the Linux kernel to automatically load the vfat driver into the kernel while it is needed. The kernel module handler loads these drivers, and when they become unused after the filesystem is unmounted, they are unloaded to recover the memory that they occupied. See Chapter 27, “Configuring and Building Kernels,” for more information about kernel modules.

### Potential Problems with mount

Any one of several things can cause the mount command to fail, for example:

- **Incorrect device name**—It is possible to specify an incorrect device name (that is, a device file that does not exist or one for which a driver is not available in the kernel or for which the hardware is not present).
- **Unreadable devices**—Devices can be unreadable either because the devices themselves are bad (for example, empty diskette drives or bad media) or because you have insufficient permissions to mount them. Filesystems, other than those sanctioned by the administrator by listing them with the option user in /etc/fstab, are forbidden to ordinary users and require root privilege to mount them.
- **Bad mount point**—Trying to mount a device at a mount point that does not already exist will not work.
- **Other errors**—Still more error conditions are possible but unlikely (for example, exceeding the compiled-in limit to the number of mounted filesystems) or self-explanatory (for example, most usage errors for the mount command itself). There are some more unlikely error messages that chiefly relate to the loopback devices.

When you mount a filesystem, the mount point (the point at which the filesystem is to be mounted) must be a directory. This directory doesn’t have to be empty, but after the filesystem is mounted, anything underneath it is inaccessible. Linux provides a singly rooted filesystem, which is in contrast to those operating systems that give each filesystem a separate drive letter. This is more flexible because the size of data block device (hard disk or whatever) is hidden from programs, and things can be moved around. For example, if you have some software that expects to be installed in /opt/umsp, you can install it in /big-disk/stuff/umsp and make /opt/umsp a symbolic link. There is also no need to edit a myriad of configuration files that are using the wrong drive letter after you install a new disk drive.

Many options govern how a mounted filesystem behaves; for example, it can be mounted read-only. There are options for filesystems such as msdos that don’t have any concept of users. The filesystems enable you to give each file a particular file mode (for security or to allow access by everyone). When you mount an nfs filesystem, there is so much flexibility available that the options have a separate man page (man nfs), although the defaults are perfectly reasonable. The nft filesystem is explained in more detail in Chapter 16.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_620_0.png)
