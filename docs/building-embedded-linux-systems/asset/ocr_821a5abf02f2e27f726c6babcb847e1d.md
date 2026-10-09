# Filesystem Types

Linux supports over 50 different filesystem types, but only a small subset are normally used in embedded Linux systems. The following sections will classify these popular filesystems according to the characteristics described in the previous sections and provide details about each filesystem’s creation.

# The second extended filesystem (Ext2)

The second extended filesystem is writable and persistent, built for use with block devices. It does not provide any power-down reliability or compression (unlike its follow-on, the Ext3 filesystem, described in the next section). The filesystem is very fast and supports up to 16 or 32 TB of storage.

Ext2 is one of the earliest filesystems to be used with Linux and is still a very suitable choice when used with any of the following:

+   - RAM disks in read/write mode
+   - CompactFlash devices in IDE mode
+   - NAND or NOR flash in read-only (or mostly read-only) mode, implemented either via MTD subsystem raw block device emulation or with an FTL/NFTL translation layer

We don’t recommend using Ext2 when you have to write persistent data to the storage device in production, because this filesystem doesn’t offer power-down reliability.

Creating an Ext2 filesystem and populating it is quite simple. First, you need to format the storage partition. You can do this using the mke2fs command from the e2fsprogs package, available at http://e2fsprogs.sourceforge.net.

![](bbox=[0.17, 0.63, 0.23, 0.7])

Because the Ext2 and Ext3 filesystems are commonly used in Linux desktop and server systems as well, this command is very likely already installed on your development machine.

The following example formats a NAND flash using the NFTL translation layer to present a block device to Ext2. Note, however, that any block device would have worked just the same. The example assumes that you are issuing these commands from your project’s $[PJ_ROOT] directory. It also assumes that the DOC device is accessible on your host as /dev/nftla and you want to create an Ext2 filesystem on the first partition of that device:

```
# mke2fs /dev/nftl1
mke2fs 1.18, 11-Nov-1999 for Ext2 FS 0.5b, 95/08/09
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
```