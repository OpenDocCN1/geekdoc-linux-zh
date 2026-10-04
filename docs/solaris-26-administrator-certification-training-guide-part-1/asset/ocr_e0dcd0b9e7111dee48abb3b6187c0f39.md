# Using the Command Line to Mount File Systems

File systems can be mounted from the command line by using the mount command. The following commands are used from the command line to mount and unmount file systems:

| mount | Mounts specified file systems and remote resources |
| mountall | Mounts all file systems specified in a file system table (vfstab) |
| umount | Unmounts specified file systems and remote resources |
| umountall | Unmounts all file systems specified in a file system table |

CD-ROMs containing file systems are automatically mounted when the CD-ROM is inserted. Disks containing file systems are mounted by running the volcheck command.

As a general rule, local disk slices should be included in the /etc/vfstab file so they automatically mount at bootup.

Unmounting a file system removes it from the file system mount point. Some file system administration tasks cannot be performed on mounted file systems. You should unmount a file system when

+   - It is no longer needed
- You check and repair it by using the `fsck` command
- You are about to do a complete backup of it

> NOTE. File systems are automatically unmounted as part of the system shutdown procedure.

# Displaying Mounted File Systems

Whenever you mount or unmount a file system, the /etc/mnttab (mount table) file is modified to show the list of currently mounted file systems. You can display the contents of the mount table by using the cat or more commands, but you cannot edit it as you would the /etc/vfstab file. Here is an example of a mount table file:

```
/dev/dsk/c0t3d0s0   /   ufs   rw,suid 693186371
/dev/dsk/c0t1d0s6   /usr   ufs   rw,suid 693186371
/proc   /proc   proc   rw,suid 693186371
swap   /tmp   tmpfs   ,dev=0 693186373
```

You can also view a mounted file system by typing /etc/mount from the command line. The system displays the following:

```
/ on /dev/dsk/c0t3d0s0 read/write/setuid/largefiles on ...
/usr on /dev/dsk/c0t3d0s6 read/write/setuid/largefiles on ...
/proc on /proc read/write/setuid on Fri May 16 11:39:05 1997
```