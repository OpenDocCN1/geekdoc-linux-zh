the basis of several other filesystem implementations, including Linux’s ext series, Solaris’s UFS, and IBM’s JFS.

Early systems bundled the filesystem implementation into the kernel, but it soon became apparent that support for multiple filesystem types was an important design goal. UNIX systems developed a well-defined kernel interface that allowed multiple types of filesystems to be active at once. The filesystem interface also abstracted the underlying hardware, so filesystems see approximately the same interface to storage devices as do other UNIX programs that access the disks through device files in /dev.

Support for multiple filesystem types was initially motivated by the need to support NFS and filesystems for removable media. But once the floodgates were opened, the "what if" era began; many different groups started to work on improved filesystems. Some were system specific, and others (such as ReiserFS) were not tied to any particular OS.

Given that you may have a choice of filesystems, should you investigate the various alternatives and choose the "best" one? Unless you’re setting up a data disk for a very specific application, no. In nearly all situations, it’s better to stick with the system’s defaults. That’s what the system’s documentation and administrative tools probably assume.

Only a few features are truly non-negotiable:

+   - Good performance
+   - Tolerance for crashes and power outages without filesystem corruption
+   - The ability to handle disks and filesystems large enough for your needs

Fortunately, modern systems’ default filesystems already cover these bases. Any improvement you might see from changing filesystems will be marginal and context dependent at best.

The next sections discuss the default filesystems on Linux, HP-UX, and AIX. The ZFS filesystem used by Solaris is administered differently and merits an entire section of its own; that section starts on page 264.

# Linux filesystems: the ext family

![](bbox=[0.18, 0.0012, 0.25, 0.00135])

The "second extended filesystem," ext2, was for a long time the mainstream Linux standard. It was designed and implemented primarily by Rémy Card, Theodore Ts’o, and Stephen Tweedie. Although the code for ext2 was written specifically for Linux, it is functionally similar to the Berkeley Fast File System.

Ext3 adds journaling capability to the existing ext2 code, a conceptually simple modification that increases reliability enormously. Even more interestingly, the ext3 extensions were implemented without changing the fundamental structure of ext2. In fact, you can still mount an ext3 filesystem as an ext2 filesystem—it just won’t have journaling enabled.