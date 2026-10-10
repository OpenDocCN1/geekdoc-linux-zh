
From Figure 9-2, we can see that the bulk of the file sizes are well below approximately 10KB. The spike at 4096 represents directories. Directory entries (also files themselves) are exactly 4096 bytes in length, and there are many of them. The spike above 40,000 bytes is an artifact of the measurement. It is a count of the number of files greater than approximately 40KB, the end of the measurement quantum. It is interesting to note that the vast majority of files are very small.

Small file sizes present a unique challenge to the Flash file system designer. Because Flash memory must be erased one entire block at a time, and the size of a Flash block is often many multiples of the smaller file sizes, Flash is subject to time-consuming block rewriting. For example, assume that a 128KB block of Flash is being used to hold a couple dozen files of 4096 bytes or less. Now assume that one of those files needs to be modified. This causes the Flash file system to invalidate the entire 128KB block and rewrite every file in the block to a newly erased block. This can be a time-consuming process.

Because Flash writes can be time-consuming (much slower than hard disk writes), this increases the window where data corruption can occur due to sudden loss of power. Unexpected power loss is a common occurrence in embedded systems. For instance, if power is lost during the rewrite of the 128KB data block referenced in the previous paragraph, all of the couple dozen files could potentially be lost.

Enter JFFS2. These issues just discussed and other problems have been largely reduced or eliminated by the design of the second-generation Journaling Flash File System, or JFFS2. The original JFFS was designed by Axis Communications AB of Sweden and was targeted specifically at the commonly available Flash memory devices at the time. The JFFS has knowledge of the Flash architecture and, more important, architectural limitations imposed by the devices.

Another problem with Flash file systems is that Flash memory has a limited lifetime. Typical Flash memory devices are specified for a minimum of 100,000 write cycles, and, more recently, 1,000,000-cycle devices have become common. This specification is applicable to each block of the Flash device. This unusual limitation imposes the requirement to spread the writes evenly across the blocks of a Flash memory device. JFFS2 uses a technique called wear leveling to accomplish this function.

Building a JFFS2 image is relatively straightforward. As always, you must ensure that your kernel has support for JFFS2 and that your development workstation contains a compatible version of the `mkfs.jffs2` utility. JFFS2 images are built from a directory that contains the desired files on the file system image. Listing 9-8 shows a typical directory structure for a Flash device designed to be used as a root file system.

### Listing 9-8
Directory Layout for JFFS2 File System

```
$ ls -l
total 44
drwxr-xr-x  2 root root 4096 Aug 14 11:27 bin
drwxr-xr-x  2 root root 4096 Aug 14 11:27 dev
drwxr-xr-x  2 root root 4096 Aug 14 11:27 etc
drwxr-xr-x  2 root root 4096 Aug 14 11:27 home
drwxr-xr-x  2 root root 4096 Aug 14 11:27 lib
drwxr-xr-x  2 root root 4096 Aug 14 11:27 proc
drwxr-xr-x  2 root root 4096 Aug 14 11:27 root
drwxr-xr-x  2 root root 4096 Aug 14 11:27 sbin
drwxr-xr-x  2 root root 4096 Aug 14 11:27 tmp
drwxr-xr-x  2 root root 4096 Aug 14 11:27 usr
drwxr-xr-x  2 root root 4096 Aug 14 11:27 var
$
```

When suitably populated with runtime files, this directory layout can be used as a template for the `mkfs.jffs2` command. The `mkfs.jffs2` command produces a properly formatted JFFS2 file system image from a directory tree such as that in Listing 9-8. Command line parameters are used to pass `mkfs.jffs2` the directory location as well as the name of the output file to receive the JFFS2 image. The default is to create the JFFS2 image from the current directory. Listing 9-9 shows the command for building the JFFS2 image.

### Listing 9-9
`mkfs.jffs2` Command Example

```
# mkfs.jffs2 -d ./jffs2-image-dir -o jffs2.bin
# ls -l
total 4772
-rw-r--r--  1 root root 1098640 Sep 17 22:03 jffs2.bin
drwxr-xr-x 13 root root    4096 Sep 17 22:02 jffs2-image-dir
#
```

The directory structure and files from Listing 9-8 are in the `jffs2-image-dir` directory in our example. We arbitrarily execute the `mkfs.jffs2` command from the directory above our file system image. Using the `-d` flag, we tell the `mkfs.jffs2` command where the file system template is located. We use the `-o` flag to name the output file to which the resulting JFFS2 image is written. The resulting image, `jffs2.bin`, is used in Chapter 10, “MTD Subsystem,” when we examine the JFFS2 file together with the MTD subsystem.

It should be pointed out that any Flash-based file system that supports write operations is subject to conditions that can lead to premature failure of the underlying Flash device. For example, enabling system loggers (syslogd and klogd) configured to write their data to Flash-based file systems can easily overwhelm a Flash device with continuous writes. Some categories of program errors can also lead to continuous writes. Care must be taken to limit Flash writes to values within the life-time of Flash devices.

## 9.6 cramfs

From the READ_ME file in the cramfs project, the goal of cramfs is to “cram a file system into a small ROM.” The cramfs file system is very useful for embedded systems that contain a small ROM or FLASH memory that holds static data and programs. Borrowing again from the cramfs README file, “cramfs is designed to be simple and small, and compress things well.”

The cramfs file system is read only. It is created with a command line utility called mkcramfs. If you don’t have it on your development workstation, you can download it from the link at the end of this chapter. As with JFFS2, mkcramfs builds a file system image from a directory specified on the command line. Listing 9-10 details the procedure for building a cramfs image. We use the same file system structure from Listing 9-8 that we used to build the JFFS2 image.

### Listing 9-10
`mkcramfs` Command Example

```
# mkcramfs
usage: mkcramfs [-h] [-v] [-b blksize] [-e edition] [-i file] [-n name] dirName outfile
  -h print this help
  -E make all warnings errors (non-zero exit status)
  -b blksize use this blocksize, must equal page size
  -e edition use edition number (part of fsid)
  -i file insert a file image into the filesystem (requires >= 2.4.0)
  -n name set name of cramfs filesystem
  -p pad by 512 bytes for boot code
  -s sort directory entries (old option, ignored)
  -v be more verbose
  -x make explicit holes (requires >= 2.3.39)
  dirName root of the directory tree to be compressed
  outfile output file

$ mkcramfs .../cramfs.image
warning: gids truncated to 8 bits (this may be a security concern)
$ ls -l .../cramfs.image
-rw-rw-rw- 1 chris chris 1019904 Sep 19 18:06 .../cramfs.image
```

The `mkcramfs` command was initially issued without any command line parameters to reproduce the usage message. Because there is no man page for this utility, this is the best way to understand its usage. We subsequently issued the command specifying the current directory, ` .`, as the source of the files for the cramfs file system, and a file called `cramfs.image` as the destination. Finally, we listed the file just created, and we see a new file called `cramfs.image`.

Note that if your kernel is configured with cramfs support, you can mount this file system image on your Linux development workstation and examine its contents. Of course, because it is a read-only file system, you cannot modify it. Listing 9-11 demonstrates mounting the cramfs file system on a mount point called `/mnt/flash`.

### Listing 9-11
Examining the cramfs File System

```
$ mount -o loop cramfs.image /mnt/flash
$ ls -l /mnt/flash
total 6
drwxr-xr-x 1 root root  704 Dec 31  1969 bin
drwxr-xr-x 1 root root    0 Dec 31  1969 dev
drwxr-xr-x 1 root root  416 Dec 31  1969 etc
drwxr-xr-x 1 root root    0 Dec 31  1969 home
drwxr-xr-x 1 root root  172 Dec 31  1969 lib
drwxr-xr-x 1 root root    0 Dec 31  1969 proc
drwx------ 1 root root    0 Dec 31  1969 root
drwxr-xr-x 1 root root  272 Dec 31  1969 sbin
drwxrwxrwt 1 root root    0 Dec 31  1969 tmp
drwxr-xr-x 1 root root  124 Dec 31  1969 usr
drwxr-xr-x 1 root root  212 Dec 31  1969 var
```
