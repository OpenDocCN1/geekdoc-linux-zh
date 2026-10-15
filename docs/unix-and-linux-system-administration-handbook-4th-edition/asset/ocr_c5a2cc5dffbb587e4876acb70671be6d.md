block is actually saved to disk. Applications can request more predictable behavior for a file, but this option lowers throughput.

The sync system call flushes modified blocks to their permanent homes on disk, possibly making the on-disk filesystem fully consistent for a split second. This periodic save minimizes the amount of data loss that might occur if the machine were to crash with many unsaved blocks. Filesystems can do syncs on their own schedule or leave this up to the OS. Modern filesystems have journaling mechanisms that minimize or eliminate the possibility of structural corruption in the event of a crash, so sync frequency now mostly has to do with how many data blocks might be lost in a crash.

A filesystem’s disk block map is a table of the free blocks it contains. When new files are written, this map is examined to devise an efficient layout scheme. The block usage summary records basic information about the blocks that are already in use. On filesystems that support extents, the information may be significantly more complex than the simple bitmap used by older filesystems.

# Filesystem polymorphism

Filesystems are software packages with multiple components. One part lives in the kernel (or even potentially in user space under Linux; google for FUSE) and implements the nuts and bolts of translating the standard filesystem API into reads and writes of disk blocks. Other parts are user-level commands that initialize new volumes to the standard format, check filesystems for corruption, and perform other format-specific tasks.

Long ago, the standard user-level commands knew about "the filesystem" that the system used, and they simply implemented the appropriate functionality. mkfs created new filesystems, fsck fixed problems, and mount mostly just invoked the appropriate underlying system calls. These days filesystems are more modular, so these commands call filesystem-specific implementations of each utility.

The exact implementation varies. For example, the Linux wrappers look for discrete commands named mkfs.fstype, fsck.fstype, and so on in the normal directories for system commands. (You can run these commands directly, but it’s rarely necessary.) AIX has a central /etc/vfs switch that records metainformation for filesystems (not to be confused with Solaris’s /etc/vfstab, which is equivalent to the fstab or filesystems file on other systems; it’s not needed for ZFS, though).

# mkfs: format filesystems

The general recipe for creating a new filesystem is

```
mkfs [-T fstype] [-o options] rawdevice
```

The default fstype may be hard-coded into the wrapper, or it might be specified in /etc/default/fs. The available options are filesystem specific, but it’s rare that you’ll need to use them. Linux uses -t instead of -T, omits the -o designator, and does not have raw disk device files. AIX uses -V instead of -T.