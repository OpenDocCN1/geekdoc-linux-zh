# 434 Part III: Administering Fedora and RHEL

boot prompt when you install Fedora to reiserfs partitions. Also, SELinux doesn't
recurs file systems.)

+   - ufs — This file system is popular on Sun Microsystems operating systems (that is,
Solaris and SunOS).

+   - xenix — This was added to be compatible with Xenix file systems (one of the first PC
versions of UNIX). The system is obsolete and will probably be removed eventually.

+   - xfs — This is a journaling file system that is useful in high-performance environments. It
includes full 64-bit addressing. An xfs file system can scale to systems that include
multiple terabytes of data transfer at multiple gigabytes per second.

+   - jfs — This file system is based on the JFS file system IBM for OS/2 Warp. It
came an open source project in 2000. JFS is most suited for enterprise systems. Like
XFS, JFS is tuned for file systems and high-performance environments.

+   - xiafs — This file system supports long filenames and larger inodes than file systems
such as nix.

+   - squashfs — This is a compressed file system, where files are uncompressed on the fly
they requested. It is often used with live CDs, including all Fedora Live CDs.
- fuse — Behave like a user-space remote file system. A local user can use ssh tools
available, purely on the basis of the permissions of the user login. A very cool
way to mount a remote file system without administrative intervention on the remote
side.

Two new file system types were added starting in Fedora 9: ext4 file systems and encrypted
file systems. Although both are still considered experimental, tools are available in Fedora 10
to create and use these new file system types.

The ext4 file system is the latest version of the ext system (ext3 being the current
standard). An ext4 file system can be mounted as an ext3 file system. If you want to
use new ext4 features (called extents), mount as an ext4 device (mount -t ext4dev). See
Ext4 FAQ for information on creating and working with ext4 file systems:

```
http://ext4.wiki.kernel.org/index.php/Frequently_Asked_Questions
```

How-to document help you get started with ext4 file systems:

```
http://ext4.wiki.kernel.org/index.php/Ext4_How
```

You can convert an ext3 file system to ext4 by using a command like the following:

```
# tune2fs -O extents -E test_fs /dev/dev
```

And, you can adjust the inode setting, for example from 128 to 256, to improve efficiency with
a command like the following:

```
# tune2fs -I 256 /dev/dev
```