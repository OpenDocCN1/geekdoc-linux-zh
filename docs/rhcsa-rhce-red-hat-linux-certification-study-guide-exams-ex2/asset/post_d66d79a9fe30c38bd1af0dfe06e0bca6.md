
The Red Hat move to ext4 is a testament to its use as a server operating system. One improvement with ext4 means that filesystems can be as large as 1 exabyte (EB). The former maximum filesystem size with ext3 was just 16 terabytes (TB). The ext4 filesystem reduces fragmentation, guarantees space for files, supports faster checks, and more. It even supports file timestamps in nanoseconds. As ext4 has been a part of the Linux kernel since 2008, it is proven technology. Given its speed and reliability, Red Hat even uses ext4 as the default filesystem for partitions dedicated to the /boot directory.

## Filesystem Format Commands

There are several commands that can help you create a Linux filesystem. They're all based on the mkfs command, which works as a front end to filesystem-specific commands such as mkfs.ext2, mkfs.ext3, and mkfs.ext4.

If you want to reformat an existing partition, logical volume, or RAID array, take the following precautions:

- Back up any existing data on the partition.
- Unmount the partition.

There are two ways to apply formatting on a volume. (As noted earlier in this chapter, a volume is a generic name that can describe a partition, a RAID array, or a logical volume.) For example, if you've just created a partition on /dev/sdb5, you can format it to the ext4 filesystem using one of the following commands:

```
# mkfs -t ext4 /dev/sdb5
# mke2fs -t ext4 /dev/sdb5
# mkfs.ext4 /dev/sdb5
```

(The inode numbers for all three files are the same; in other words, they are three different names for the same command.)

You can format partitions, logical volumes, and RAID arrays to other filesystems. The options available in RHEL 6 include:

- **mkfs.cramfs** creates a compressed ROM filesystem.
- **mkfs.ext2** formats a volume to the ext2 filesystem.
- **mkfs.ext3** formats a volume to the RHEL 5 default ext3 filesystem.
- **mkfs.ext4** formats a volume to the RHEL 6 default ext4 filesystem.
- **mkfs.msdos** (or **mkfs.vfat** or **mkdosfs**) formats a partition to the Microsoft-compatible VFAT filesystem; it does not create bootable filesystems.
- **mkfs.xfs** formats a volume to the XFS filesystem developed by the former Silicon Graphics.
- **mkswap** formats a volume to the Linux swap filesystem.

These commands assume that you've configured an appropriate partition in the first place; for example, before the **mkswap** command can be properly applied to a partition, the Linux swap partition ID type must be configured for that partition. If you've created a RAID array or logical volume, as described later in this chapter, similar rules apply.

One advantage of some rebuild distributions is the availability of useful packages not supported by or available from Red Hat. For example, CentOS 6 includes the **ntfsprogs** package, which supports the mounting of **NTFS** partitions.

## Swap Volumes

While Linux can use swap files, the swap space that's used essentially as overflow for RAM is generally configured in properly formatted partitions or logical volumes. They're generally not configured from RAID arrays, as redundancy for RAM is generally not useful. To see the swap space currently configured, run the **cat /proc/swaps** command.

As suggested in the previous section, swap volumes are formatted with the **mkswap** command. But that's not enough. First, to test the new swap volume, it must be activated with the **swapon** command. If the new swap volume is recognized, you'll see it in both the **/proc/swaps** file and the output to the **top** command. Second, you'll need to make sure to configure the new swap volume in the **/etc/fstab** file, as described later in this chapter.

## Filesystem Check Commands

The **fsck** command analyzes the specified filesystem and performs repairs as required. Assume, for example, you're having problems with files in the **/var** directory, which happens to be mounted on **/dev/sda7**. If you want to run **fsck**, unmount that filesystem first. In some cases, you may need to go into single-user mode with the init 1 command before you can unmount a filesystem. To unmount, analyze, and then remount the filesystem noted in this section, run the following commands:

```
# umount /var
# fsck -t ext4 /dev/sda7
# mount /dev/sda7 /var
```

The fsck command also serves as a "front end," depending on the filesystem format. For example, if you're formatting an ext2, ext3, or ext4 filesystem, fsck by itself automatically calls the e2fsck command. In fact, the fsck.ext2, fsck.ext3, fsck.ext4, and e2fsck files are all different names for the same command! They have the same inode number. You can confirm this by applying the ls -i command to all four files, which are part of the /sbin directory.

## Filesystem Conversions

If you're upgrading between versions of Linux, you may also want to upgrade filesystems. It wasn't that long ago that most Linux systems were configured to the ext2 filesystem. In fact, for RHEL 5, ext3 was considered inefficient for many filesystems such as the /boot directory, so many administrators formatted the associated partition to ext2.

Fortunately, if you have a partition formatted to ext2, it's easy to add the journal associated with ext3. And then it's a straightforward command to add the features associated with ext4 formatting. These commands require a temporary remounting of the filesystem in read-only mode. Alternatively, you could just unmount that directory. For example, if the filesystem in question is mounted on the /dev/vda1 partition, you'd run the following commands to convert from ext2 to ext3, where the tune2fs -j command adds a journal.

```
# mount -o remount,ro /dev/vda1
# tune2fs -j /dev/vda1
# mount -o remount,rw /dev/vda1
```

Of course, you'd then have to make appropriate changes to the /etc/fstab configuration file, namely changing the filesystem format column from ext2 to ext3. If necessary, you could convert back with the tune2fs -O ^has_journal command. But any move from ext2 or ext3 to ext4 is one-way. You can't convert back to ext3 or ext2. If you're ready to make the move to ext4, run the following command:

```
# tune2fs -O extent,uninit_bg,dir_index /dev/vda1
```

In fact, if you try to disable some components of the ext4 filesystem, it may break features such as the blkid command described later in this chapter.

If you're converting the volume associated with the top-level root directory (/), it's not possible to even remount that directory in read-only mode. Thus, the process with that directory may require a detour through the rescue mode environment described in Chapter 5.

To confirm the current settings associated with a filesystem, run the following command:

```
# dumpe2fs /dev/vda1 | grep "Filesystem features"
```

You should see the features just described in the output associated with the features of the specified filesystem volume.

## EXERCISE 6-2

### Format, Check, and Mount Different Filesystems

In this exercise, you'll work with the file format and checking commands mkfs and fsck, and review the results with the mount command. This exercise assumes you've completed Exercise 6-1, or at least have unmounted Linux partitions with no data.

- 1. Review the current status of partitions on the drives discussed in Exercise 6-1 with the parted /dev/sda print and fdisk -l /dev/sdb commands.
- 2. Format the partition created the first drive with the mkfs.ext2 /dev/sda1 command. Review the current status of the volume with the dumpe2fs /dev/sda1 | grep "Filesystem features" command. What features do you see in the output? Save the output, temporarily. One way to do so is open a new command line console. Check the system with the fsck.ext2 /dev/sda1 command.
- 3. Mount the newly formatted partition with mount /dev/sda1 /mnt command. Review the output with the mount command, by itself. If the mount and format worked, you'll see the following output:
  `/dev/sda1 on /mnt type ext2 (rw)`
- 4. Unmount the formatted partition with the umount /mnt command.
- 5. Run the tune2fs -j /dev/sda1 command and rerun the dumpe2fs command from the previous step. What's the difference between the output now, and the output when the partition was formatted to the ext2 filesystem?
