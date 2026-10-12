
# Note

Table 18.1 contains options useful for mount in alphabetical order. Unless otherwise indicated, these options are valid for all filesystem types, although asking for asynchronous writes to a CD-ROM is no use. Options applicable only to NFS filesystems are not listed here; refer to the *nfs* command manual page for those.

## TABLE 18.1 mount Options

| Option | Description |
| :--- | :--- |
| async | Write requests for the filesystem normally should wait until the data has reached the hardware; with this option, the program continues immediately instead. This does mean that the system is slightly more prone to data loss in the event of a system crash, but on the other hand, crashes are rare with Linux. This option speeds up NFS filesystems to a startling extent. The opposite of this option is `sync`. |
| ro | Mounts the file system read-only. This is the opposite of the option `rw`. |
| rw | Mounts the file system read/write. This is the opposite of the option `ro`. |
| suid | Allows the set user ID and set group ID file mode bits to take effect. The opposite of this option is `nosuid`. The `nosuid` option is more useful; it is used for the same sorts of reasons that `nodev` is used. |
| sync | All write operations cause the calling program to wait until the data has been committed to the hardware. This mode of operation is slower but a little more reliable than its opposite, asynchronous I/O, which is indicated by the option `async`. |
| user | Allows ordinary users to mount the file system. When there is a `user` option in `/etc/fstab`, ordinary users indicate which file system they want to mount or unmount by giving the device name or mount point; all the other relevant information is taken from the `/etc/fstab` file. For security reasons, `user` implies the `noexec`, `nosuid`, and `nodev` options. |

One of the defaults for file systems is that they are mounted `async`. This matters in that the operating system will return control before it actually reads or writes a file. Many people have erred by pulling a diskette out of the drive too soon, causing a read or write to be aborted and errors to occur.

Options are processed by the `mount` command in the order they appear on the command line (or in `/etc/fstab`). Thus, it is possible to allow users to mount a file system and then run set user ID executables by using the options `user`, `suid` in that order. Using them in reverse order (`suid`, `user`) wouldn't work because the `user` option would turn off the `suid` option again.

There are many other options available, but they are all specific to particular file systems. All the valid options for `mount` are detailed in its manual page. An example is the `umask` flag for the `vfat` and `fat` file systems, which allows you to make all the files on your MS-DOS or Windows partitions readable (or even writable if you prefer) for all the users on your Linux system.

## Mounting with the User Mount Tool

This graphical tool is good for quickly mounting and unmounting file systems. This is especially useful for diskette and CD-ROM file systems. Figure 18.1 shows the user mount tool. You will note that the floppy drive is mounted, but that the CD-ROM is not.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_623_0.png)

The user mount tool reads `/etc/fstab` to get the information for mounting. This means that by default, the floppy drive is of type `ext2`. This setting is great for Linux, but does not allow it to be used in a DOS setting. I have found that by changing the `/etc/fstab` entry for the floppy drive to the type `msdos`, I gain greater flexibility in the use of my diskettes as I switch between systems.

## Setting Up Filesystems

There are several ways of changing the entries in the `/etc/fstab` file. The first is to edit the file manually using your favorite editor. This assumes that you are a flawless typist and know all of the different options. Of course, knowing how to edit the file by hand means you do not have to have the X Window System running. I will also discuss how to administer file systems with the `fsconf` utility (`/sbin/fsconf`) and `linuxconf` (`/sbin/linuxconf`). These utilities can be run in several ways; they both have a GUI interface, a text mode, and a curses-based interface.

## Editing /etc/fstab Manually

The filesystem table `/etc/fstab` is just a text file; it is designed to have a specific format that is readable by humans and not just computers. It is separated into columns by tabs or spaces. You can edit it with your favorite text editor; it doesn't matter which. You must take care, however, if you modify it by hand because removing or corrupting an entry will make the system unable to mount that filesystem the next time it boots. For this reason, I make a point of saving previous versions of this file using the Revision Control System (a very useful program; see the manual page for `rcs`).

A sample `/etc/fstab` looks like this:

```
#
# /etc/fstab
#
# You should be using fstool (control-panel) to edit this!
#
#<device> <mountpoint> <filesystemtype> <options> <dump> <fsckorder>

/dev/hda1 / ext2 defaults 1 1
/dev/hdb5 /home ext2 defaults,rw 1 2
/dev/hda3 /usr ext2 defaults 1 2
/dev/hdb1 /usr/src ext2 defaults 1 3

/dev/hdc /mnt/cdrom iso9660 user,noauto,ro 0 0
/dev/sbpc0 /mnt/pcc iso9660 user,noauto,ro 0 0
/dev/fd1 /mnt/floppy vfat user,noauto 0 0

/proc /proc proc sw
/dev/ha22 none swap sw
```

The first four entries are the ext2 filesystems composing the sample Linux system. When Linux is booted, the root filesystem is mounted first; all the other local (that is, non-network) filesystems are mounted next. Filesystems appear in `/etc/fstab` in the order they are mounted; `/usr` must appear before `/usr/src`, for example, because the mount point for one filesystem exists on the other. The following three filesystems are all removable filesystems (two CD-ROMs and a floppy drive). These have the `noauto` option set so that they are not automatically mounted at boot time. The removable devices have the `user` option set so that I can mount and unmount them without having to use `su` all the time. The CD-ROMs have the filesystem type `iso9660`, which is the standard filesystem for CD-ROMs, and the floppy drive has the filesystem type `vfat` because I often use it for interchanging data with MS-DOS and Windows systems.

The last two filesystems are special: the first (`/proc`) is a special filesystem provided by the kernel as a way of providing information about the system to user programs. The information in the `/proc` filesystem is used to make utilities such as `ps`, `top`, `xload`, `free`, `netstat`, and so on work. Some of the “files” in `/proc` are really enormous (for example, `/proc/kcore`). Don’t worry; no disk space is wasted. All the information in the `/proc` filesystem is generated on-the-fly by the Linux kernel as you read it. You can tell that they are not real files because, for example, root can’t give them away with `chown`.

The final "filesystem" isn't a filesystem at all; it is an entry that indicates a disk partition used as swap space. Swap partitions are used to implement virtual memory. Files can also be used for swap space. The names of the swap files go in the first column where the device name usually goes.

The two numeric columns on the right relate to the operation of the `dump` and `fsck` commands. The `dump` command compares the number in column 5 (the dump interval) with the number of days since that filesystem was last backed up. This way it can inform the system administrator that the filesystem needs to be backed up. Other backup software—for example, Amanda—can also use this field for the same purpose. (Refer to Chapter 22 for more information on Amanda.) Filesystems without a dump interval field are assumed to have a dump interval of 0, denoting "never dump." For more information, see the manual page for `dump`.

The sixth column is the `fsck` pass and indicates which filesystems can be checked in parallel at boot time. The root filesystem is always checked first, but after that, separate drives can be checked simultaneously because Linux is a multitasking operating system. There is no point, however, in checking two filesystems on the same hard drive at the same time because this results in a lot of extra disk head movement and wasted time. All the filesystems that have the same pass number are checked in parallel from 1 upward. Filesystems with a 0 or missing pass number (such as the floppy and CD-ROM drives) are not checked at all.

## Creating New Filesystems

When you install Red Hat Linux, the installation process makes some new filesystems and sets up the system to use them.

Many operating systems don't distinguish between the preparation of the device's surface to receive data (formatting) and the building of new filesystems. Linux does distinguish between the two, principally because only diskettes need formatting and also because Linux offers as many as half a dozen different filesystems that can be created on (any block device). Separately providing the facility of formatting diskettes in each of these programs is poor design and requires you to learn a different way of doing it for each kind of new filesystem. The process of formatting diskettes is dealt with separately. (See the section "Floppy Disk Drivers" later in this chapter for more information.)

Filesystems are initially built by a program that opens the block device and writes some structural data to it so that when the kernel tries to mount the filesystem, the device contains the image of a pristine filesystem. This means that both the kernel and the program used to make the filesystem must agree on the correct filesystem structure.
