# CHAPTER 8

# The FreeBSD Filesystem

To understand how FreeBSD operates, it is essential to have a clear idea of how the system manages files as well as the critical differences between FreeBSD’s method and those of other operating systems.

FreeBSD uses the BSD Fast Filesystem (FFS). It is a common misconception that modern BSD Unixes use UFS (Universal or Unix Filesystem, depending on who you ask). In fact, many of the tools discussed in this chapter (such as mount) refer to UFS as the default filesystem type. This isn’t the case. FFS is colloquially called UFS by many, and you can do the same—as long as you remember that the “true” UFS was used only in very early BSD-style Unixes and has been replaced by FFS in FreeBSD.

FFS is the filesystem type commonly used in FreeBSD, OpenBSD, NetBSD, and others, including Mac OS X (whose foundation, called Darwin, is based on FreeBSD and the core BSD distribution). Linux typically uses Ext2FS, Windows NT uses NTFS, and Windows 95/98/Me use VFAT. This information will be useful to know later in this chapter when we discuss mounting filesystems from other operating systems.

> **NOTE**
> A fuller reference and discussion of the filesystem types used in the computing world can be found at `http://www.penguin.cz/~mh1/fs/`.

# ## The FreeBSD Directory Structure

If you have used any Unix or Unix-like operating system, FreeBSD’s directory structure will undoubtedly look familiar to you (see Figure 8.1).

# **IN THIS CHAPTER**

+   * The FreeBSD Directory Structure
+   * Monitoring Filesystem Usage
+   * Mounting and Unmounting FreeBSD Filesystems
+   * Mounting and Unmounting Filesystems from Other Operating Systems
+   * Mounting and Unmounting CD-ROM and Floppy-Based Filesystems
+   * Understanding the /etc/fstab File
+   * Checking and Repairing Filesystems with fsck
+   * Setting and Enforcing User Filesystem Quotas