As a general rule, local disk slices should be included in the /etc/vfstab file so that they automatically mount at bootup.

Unmounting a file system removes it from the file system mount point. Some file system administration tasks cannot be performed on mounted file systems. You should unmount a file system when

+   - It is no longer needed.
- You check and repair it by using the fsck command.
- You are about to do a complete backup of it.

# Displaying Mounted File Systems

Whenever you mount or unmount a file system, the /etc/mnttab (mount table) file is modified to show the list of currently mounted file systems.

In previous Solaris releases, /etc/mnttab was a text-based file that stored information about mounted file systems. The downside of being a file was that it could get out of sync with the actual state of mounted file systems. With /etc/mnttab implemented as a file system, the information on mounted file systems and mount options can be more accurately kept in the kernel. Therefore, this file now will always reflect the in-kernel mount table. The /etc/mnttab is now a MNTFS file system that provides read-only information directly from the kernel about mounted file systems for the local system. The kernel maintains the list in order of mount time. That is, the first mounted file system is first in the list, and the most recently mounted file system is last.

You can display the contents of the mount table by using the cat or more commands, but you cannot edit them as you would the /etc/vfstab file. Here is an example of a mount table file:

```
/dev/dsk/c0t3d0s0          ufs   rw,suid  693186371
/dev/dsk/c0t1d0s6  /usr   ufs   rw,suid  693186371
/proc           /proc  -proc rw,suid  693186371
swap            /tmp   tmpfs rw,dev=0  693186373
```