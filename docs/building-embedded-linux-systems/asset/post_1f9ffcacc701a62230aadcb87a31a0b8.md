
8160 inodes, 32574 blocks
1628 blocks (5.00%) reserved for the super user
First data block=1
4 block groups
8192 blocks per group, 8192 fragments per group
2040 inodes per group
Superblock backups stored on blocks:
8193, 24577

Writing inode tables: done
Writing superblocks and filesystem accounting information: done

Now, mount the partition and copy the filesystem data to it:

```
# mkdir /mnt/doc
# mount -t ext2 /dev/nftfa1 /mnt/doc
# cp -a rootfs/* /mnt/doc
```

If you cannot access the storage device from your host machine (such as over NFS), you have two options:

- Mount an NFS root filesystem on the target, and then copy the contents of the root filesystem onto your storage device. Using an NFS filesystem is described in Chapter 9.
- Generate a binary image file of the filesystem data, and copy it onto the storage device using an external device, such as a JTAG connector or a flash programmer.

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_261_0.png)

Yet a third option is to create an empty file of the required filesystem image size, format it using `mke2fs` with the `-f` flag, and then loopback mount it using `mount` with the `-o loop` option. However, using `genext2fs` is much better, so we mention this option only for the sake of completeness.

To generate the binary image file containing the filesystem, use the `genext2fs` program. As its name suggests, `genext2fs` generates an image file containing an Ext2 filesystem that you can copy later to the target storage device. An additional advantage of using `genext2fs` over mounting the storage device on the host (as suggested previously) is that you don't require root permissions to create the image. Therefore, it is both safer and easier, and we recommend it.

`genext2fs` can be downloaded from the project website at `http://genext2fs.sourceforge.net`, the latest version at the time of this writing is 1.4.1. The build and installation procedure is straightforward:

```
$ tar zxvf genext2fs-1.4.1.tar.gz
$ cd genext2fs-1.4.1
$ ./configure
$ make
$ make check
$ make install
```

Using *genext2fs* is also quite straightforward:

```
$ genext2fs -b 1024 -d src -D device_table.txt -e 0 flashdisk.img
```

This command will create a file called *flashdisk.img* in the current directory, 1024 KB in size, that will contain an image of an Ext2 filesystem with all the files and directories from the *src* directory. The *-e* option zeroes out all the unallocated space on the filesystem.

The file *device_table.txt*, which is passed as a parameter to the *-D* option, contains a list of regular and special files and directories that either need to be added to the filesystem image (in addition to the files and directories present in the *src* directory) or need to have their ownership or permission changed. Each line in this file is of the form:

```
name type mode uid gid
major minor start inc
  count
```

In each line, *name* is a relative or absolute path to the filename. *type* is one of the following:

- *f* A regular file
- *d* A directory
- *c* A character device file
- *b* A block device file
- *p* A FIFO or named pipe

*mode* is the file permission, and *uid* and *gid* are the user ID and group ID (respectively) that own the file or directory.

The rest of the entries (*major*, *minor*, etc.) apply only to device files. *major* and *minor* are the device file major and minor numbers. *start*, *inc*, and *count* can be used to create multiple device files in a single command, where a serial number is appended to the device file name, starting from *start* and incremented by *inc* for each of the *count* device files created. The minor number can also be incremented in the same fashion.

The following is an example device table file, written by Erik Andersen and taken from the *genext2fs* manpage:

```
# name type mode uid gid major minor start inc count

/dev/    d  755  0   0     -     -   -    -    -
/dev/mem c  640  0   0     1    1   0    0    -
/dev/tty c  666  0   0     5    0   0    0    -
/dev/tty c  666  0   0     4    0   0    1    6
/dev/loop b 640 0 0 7 0 0 1 2
/dev/hda b 640 0 0 3 0 0 0 -
/dev/hda b 640 0 0 3 1 1 1 16
/dev/log s 666 0 0 - - - - -
```

This device table creates the `/dev` directory and the device nodes `/dev/mem` (major 1, minor 1), and also `/dev/tty`, `/dev/tty[0-5]`, `/dev/loop[0-1]`, `/dev/hda`, `/dev/hda[1-15]`, and `/dev/log socket`.

Many other options for genext2fs are described in the command’s manpage; we recommend reading it.

## The third extended filesystem (Ext3)

The third extended filesystem is an extension of the second extended filesystem that adds reliability, via journaling, to Ext2’s writability and persistence.

By default, Ext3 will operate in ordered mode, meaning it will journal only filesystem metadata, and only after all data updates have been written directly to storage. This behavior is usually a good compromise that protects the filesystem metadata but does not slow down writes by having any file data updates go through the filesystem journal. You can change the behavior, at the cost of significantly slowing down writes, with the data=journal mount option.

Another recommended mount option is noatime, which will disable the default behavior of updating the last access time on files stored in the filesystem. This breaks the filesystem’s POSIX compatibility, but can greatly improve the lifetime of flash devices, as well as often providing better I/O throughput to the system.

Here is an example showing both options used to mount an Ext3 filesystem from the first partition of a CompactFlash in IDE mode (once again, the command would be similar for any block device):

```
# mount -t ext3 /dev/hda1 /media/cf -o noatime,data=journal
```

Ext3 is recommended for use with CompactFlash devices in IDE mode, provided that their hardware provides wear level control (most do). It is also recommended for NAND or NOR flashes via FTL/NFTL translation layers.

An Ext3 filesystem can be created using exactly the same methods described in the previous section for Ext2, as they both share a common storage device format. The first time an Ext2 filesystem is mounted as an Ext3 filesystem, the filesystem driver will automatically create a journal entry and start using it. You can, however, create the journal entry in advance when using the mke2fs program, by supplying it with the -j option.

## Cramfs

Linus Torvalds wrote Cramfs as a filesystem with a bare-minimum feature set. It is a very simple, and sometimes simplistic, compressed and read-only filesystem aimed at embedded systems.

Cramfs can be used with any block device and is recommended for use in the following situations:

- As a read-only filesystem on NOR and NAND flash via the “raw” MTD block device emulation, in the common situation where updates of the filesystem image are rare
- With NAND or NOR flash via FTL or NFTL translation layers
- On CompactFlash in IDE mode
- As a RAM disk image

Apart from being read-only, Cramfs has the following limitations:

- The maximum size of a file is 16 MB.
- There are no current (.) or parent (..) directory entries.
- The user-ID field for files is 16 bits wide, and the group-ID field is 8 bits wide. Normal filesystems usually support either 16- or 32-bit uids and gids. On Cramfs, gids are truncated to the lower 8 bits. In other words, you can have at most 255 groups on a root filesystem built on Cramfs.
- All file timestamps are set to the Epoch (00:00:00 GMT, January 1, 1970). The timestamps may be updated at runtime, but the updated values will last only as long as the inode is cached in memory. Once the file is reloaded, its timestamp will revert to the Epoch.
- Only kernels using 4096-byte page sizes (the value of `PAGE_CACHE_SIZE` must be 4096) can read Cramfs images.
- All files, whether they are linked or not, have a link count* of 1. Even when multiple filesystem entries point to the same file, that file has a link count of only 1. This is fine for most operations, however, because no files can actually be deleted from Cramfs.

The limited number of gids is not a problem as long as your target’s root filesystem contains no group with a gid above 255. For instance, if your target is a single-user system, you don’t need to worry about this limitation. If your system must support a multiuser environment, make sure the gids of all files and directories are below 255.

> \* See Chapter 5 in Running Linux by Matthias Dalheimer and Matt Welsh (O’Reilly) for a discussion of uids and gids.

> † Typically, filesystems maintain a count of the number of links made toward a file, and when this count reaches 0, the file is deleted.
