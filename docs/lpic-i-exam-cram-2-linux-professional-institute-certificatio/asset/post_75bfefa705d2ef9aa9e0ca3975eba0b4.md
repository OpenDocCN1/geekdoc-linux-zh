
This causes the system to completely ignore the mount count and never initiates a file system check routinely. This is desired on an ext3 file system, which never marks the file system as dirty or corrupted because the journal is where the state of the file system is stored.

In addition to the mount count, error checking can be altered so the system will do one of three things when an error is detected by the kernel for the file system:

- **continue**—Continues normally
- **remount -ro**—Remounts the file system read-only, ready to *fsck*
- **panic**—Causes the kernel to panic, which stops the system (not recommended unless you're a system tester)

The reserved percentage (space available only to the root user) associated with the root user can also be associated with a system group with the **-g** option, such as

```
tune2fs -g admins /dev/sdb5
```

## Debugging File Systems

The **debugfs** command is useful for debugging and fiddling with the file systems on your machine. It's also extremely easy to delete or corrupt a portion or all of the file system, so extreme caution is recommended.

> **CAUTION** In fact, you'll have to read the man page for **debugfs** to even see how to damage the file system. It's not mounted read-write by default, probably due to the fact that users can find the command. You've been warned.

The **debugfs** tool is interactive, with a command-line shell environment you can get help with by typing **?** and pressing **Enter**.

For example, you can enter the tool simply by typing

```
debugfs /dev/sdb5
```

Then type **?** and press **Enter** to see a menu of commands available to you. Interesting and informative commands include

- **open**—Opens a file system for debugging
- **features**—Shows the file system's feature set
- **stats**—Shows the statistics for the file system and is similar to the dumefs -h output
- **ls**—Shows the directory, which by default is the root (/)
- **pwd**—Shows the working directory
- **undelete**—Undeletes a file (used immediately after the deletion in successful cases)
- **logdump**—Shows the contents of the journal (if in a journal-led file system)
- **quit**—Quits the tool

## Mounting and Unmounting

In the final section of this chapter, we will discuss mounting and unmounting file systems, the options available, and how this subject is used for the exam.

## The File System Table

For a file system to be used by normal users, that file system must either be mounted by the root user or be put in the /etc/fstab file with the correct options that allow users that privilege. When a proper entry exists in the /etc/fstab, a user only needs to issue the mount command with the full path of a mount point or device to accomplish the mount.

File systems should be set up in /etc/fstab, one per line. Entries that are mounted are reflected in /etc/mtab, which is maintained by the system as a description of the mounted file systems. This information (or most of it) is also in the /proc/mounts file.

Type the mount command to see the current list of file systems. Here’s an example:

```
mount
/dev/sda2 on / type ext3 (rw)
none on /proc type proc (rw)
usbdevfs on /proc/bus/usb type usbdevfs (rw)
/dev/sda1 on /boot type ext3 (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
none on /dev/shm type tmpfs (rw)
/dev/sdb8 on /home/data type ext3 (rw)
```

This output can be compared with the output from the /proc/mounts file:

```
cat /proc/mounts
rootfs / rootfs rw 0 0
/dev/root / ext3 rw 0 0 /
/proc /proc proc rw 0 0
usbdevfs /proc/bus/usb usbdevfs rw 0 0
/dev/sda1 /boot ext3 rw 0 0
none /dev/pts devpts rw 0 0
none /dev/shm tmpfs rw 0 0
/dev/sdc8 /home/data ext3 rw 0 0
```

Either command works, but the mount command includes options and other useful information.

The file system table (/etc/fstab) should consist of one line per file system, with a device, a mount point, a file system type, options, and dump/check orders. This file (WHR) should be modifiable only by the root user; otherwise, any user could put a removable device or disk in the system and mount it, potentially copying data to a rogue device.

Here's an example of a live /etc/fstab file:

```
LABEL=/                ext3    defaults    1  1
LABEL=/boot    /boot ext3    defaults    1  2
LABEL=/data    /data ext3    defaults    1  2
none /proc    proc    defaults    0  0
none /dev/shm tmpfs defaults    0  0
/dev/md0/1       /dev/cdroms ext2    defaults    0  0
/dev/md3    swap    swap    defaults    0  0
/dev/fe     mnt/floppy auto    noauto,USER    0  0
/dev/cdrom    mnt/cdrom iso9660 noauto,USER,ro 0  0
```

The column contents (from left to right) are as follows:

- **Device**—This is any device: local dev files, NFS shares, or partition labels
- **Mount point**—This is any directory, empty or otherwise.
- **File system type**—This is a valid file system type.
- **Options**—Options are separated by a comma. The defaults option is made up of rw, suid, sw, exec, auto, nouser, and async.
- **Dump**—If this value is 0 (zero), the dump command doesn't act on it; otherwise, a 1 indicates that the file system should be dumped on demand.
- **fsck**—This causes the file system with a 1 to be checked first and then those with a 2 and so on to be checked next.

The **auto** option in the file system column for the floppy probes the superblock for the device to attempt identification of the file system type. This works for nearly any other file system type, including `ext2`, `ext3`, `iso9660`, `vfat`, and `ntfs` to name a few.

Notice also the mutually exclusive `user` and `users` options in the floppy and CD-ROM entries' options column. These enable either exclusive or nonexclusive mounting for users on that device.

For example, if the `user` option is present for the system's CD-ROM and the daytime user Sally mounts her favorite Spice Girls release into the drive and plays it, only user Sally (and the root user) can unmount that CD-ROM.

This is unacceptable to Steven the night shift operator, who simply must have his *Tenacious D* CD-ROM to help the night pass. Steven should request that the root user switch that option with the `users` option, which allows any user to mount the device and any other user to unmount it.

## Manually Mounting File Systems

If a file system isn't configured in the `/etc/fstab` file, it can be mounted manually following this convention:

```
mount -t type -o option device mountpoint
```

The following example of a manual mount includes the type, the option, the device, and a mount point:

```
mount -t iso9660 -o exec /dev/cdrom /mnt/cdrom
```

With this `mount` command, the system's CD-ROM is mounted, allowing user access.

Mounting options that are important include

- **-a**—Mounts all file systems listed in `/etc/fstab`
- **-f**—Fakes the mounting of file systems
- **-r**—Mounts the file system read-only
- **-w**—Mounts the file system in write mode
- **-n**—Mounts without updating `/etc/mtab`
- **-L**—Mounts a file system with a given label, instead of using the device filename

## Automatically Mounting File Systems

All file systems that are in the `/etc/fstab` and don’t have the noauto option set are mounted when the system is booted. This is equivalent to issuing a mount -a command as the root user.

![](img/49f4f38f3aec011238fa50f89e643db3_166_0.png)

> The noauto option is necessary for floppies and CD-ROMs because access errors would occur if an empty removable media drive were to be affected by the mount system call. This option is also useful for rarely needed or user-specific file systems, allowing a script or user to invoke the mount as desired.

## Unmounting File Systems

The unmounting command name is umount, and it works similarly to the mount command, acting on the label, mount point, or device that’s listed in the /etc/fstab entry.

For example, to unmount the /mnt/cdrom, use either of the following:

```
umount /mnt/cdrom
umount /dev/cdrom
```

The most important fact about the umount command is that it doesn’t let you unmount any device currently in use, including a device that has a user accessing it via a file manager, a shell session, or a file in use on that device.

## Space Utilization

There are several methods of determining the space used by data on your system. It’s important to know when to use which command because each acts differently and displays different information.

![](img/49f4f38f3aec011238fa50f89e643db3_166_1.png)

> The LP1 exams test whether you can parse the question and whether you know what the various utilities produce as output. If you’ve not used the options for the du and df commands, some questions (particularly fill-in-the-blank ones) will be unanswerable.

## Using du

To see the space used by a set of files or a file tree, you use the du command. This command is configurable to show file and directory sizes, including summarization and human-readable output (KB, MB, and GB).
