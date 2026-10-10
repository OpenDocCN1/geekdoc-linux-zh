+   * ufs — This file system is popular on Sun Microsystems operating systems (that is, Solaris and SunOS).
+   * xenix — This was added to be compatible with Xenix file systems (one of the first PC versions of UNIX). The system is obsolete and will probably be removed eventually.
+   * xfs — This is a journaling file system that is useful in high-performance environments. It includes full 64-bit addressing. An xfs file system can scale up to systems that include multiple terabytes of data that transfer data at multiple gigabytes per second.
+   * jfs — This file system is based on the JFS file system IBM used for OS/2 Warp. It became an open source project in 2000. JFS is most suited for enterprise systems. Like XFS, JFS is tuned for large file systems and high-performance environments.
+   * xiafs — This file system supports long filenames and larger inodes than file systems such as minux.
+   * squashfs — This is a compressed file system, where files are uncompressed on the fly as they are requested. It is often used with live CDs, including all official Fedora Live CDs.
+   * fuse — Fuse behaves like a user-space remote file system. A local user can use ssh tools to mount a remote file system locally, without the remote file system being made available, purely on the basis of the permissions of the user you login as. A very cool way to mount a remote file system without administrative intervention on the remote side.
+   * coherent — This is the file system type used with Coherent or System V files. Like the xenix file system type, it will be removed at some time in the future.

> NOTE: Work on a new ext4 file system has begun. You can read about it on the Ext4 wiki at the kernel.org site: http://ext4.wiki.kernel.org.

# Using the fstab file to define mountable file systems

The hard disks on your local computer and the remote file systems you use every day are probably set up to mount automatically when you boot Linux. The definitions for which of these file systems are mounted are contained in an /etc/fstab file. Here’s an example of an /etc/fstab file:

```
/dev/VolGroup00/LogVol00 /					ext3			defaults				1 1
LABEL=/boot			/boot				ext3			defaults				1 2
/dev/devepts			/dev/pts			devpts		gid=5,mode=620			0 0
/dev/shm			/dev/shm			tmpfs		defaults				0 0
/dev/proc			/proc				proc		defaults				0 0
/dev/sys			/sys				sysfs		defaults				0 0
/dev/VolGroup00/LogVol01 swap				swap		defaults				0 0
/dev/sda1			/mnt/win			vfat		noauto				0 0
```