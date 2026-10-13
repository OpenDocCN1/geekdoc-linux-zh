The Red Hat move to ext4 is a testament to its use as a server operating system. One improvement with ext4 means that filesystems can be as large as 1 exabyte (EB). The former maximum filesystem size with ext3 was just 16 terabytes (TB). The ext4 filesystem reduces fragmentation, guarantees space for files, supports faster checks, and more. It even supports file timestamps in nanoseconds. As ext4 has been a part of the Linux kernel since 2008, it is proven technology. Given its speed and reliability, Red Hat even uses ext4 as the default filesystem for partitions dedicated to the /boot directory.

# Filesystem Format Commands

There are several commands that can help you create a Linux filesystem. They're all based on the mkfs command, which works as a front end to filesystem-specific commands such as mkfs.ext2, mkfs.ext3, and mkfs.ext4.

If you want to reformat an existing partition, logical volume, or RAID array, take the following precautions:

+   - Back up any existing data on the partition.
+   - Unmount the partition.

There are two ways to apply formatting on a volume. (As noted earlier in this chapter, a volume is a generic name that can describe a partition, a RAID array, or a logical volume.) For example, if you've just created a partition on /dev/sdb5, you can format it to the ext4 filesystem using one of the following commands:

```
# mkfs -t ext4 /dev/sdb5
# mke2fs -t ext4 /dev/sdb5
# mkfs.ext4 /dev/sdb5
```

You can format partitions, logical volumes, and RAID arrays to other filesystems. The options available in RHEL 6 include:

+   - **mkfs.cramfs** creates a compressed ROM filesystem.
+   - **mkfs.ext2** formats a volume to the ext2 filesystem.
+   - **mkfs.ext3** formats a volume to the RHEL 5 default ext3 filesystem.
+   - **mkfs.ext4** formats a volume to the RHEL 6 default ext4 filesystem.
+   - **mkfs.msdos** (or **mkfs.vfat** or **mkdosfs**) formats a partition to the Microsoft-compatible VFAT filesystem; it does not create bootable filesystems.