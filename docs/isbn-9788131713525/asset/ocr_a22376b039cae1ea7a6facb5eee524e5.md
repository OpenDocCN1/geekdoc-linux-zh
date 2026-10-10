The second subtlety is the use of the read-only (ro) command-line switch on the mount command. It is perfectly acceptable to mount an ext2 image from Flash using the MTD block emulation driver for read-only purposes. However, there is no support for writing to an ext2 device using the mt dblock driver. This is because ext2 has no knowledge of Flash erase blocks. For write access to a Flash-based file system, we need to use a file system with Flash knowledge, such as JFFS2.

# ## 10.4.1 JFFS2 Root File System

Creating a JFFS2 root file system is a straightforward process. In addition to compression, JFFS2 supports wear leveling, a feature designed to increase Flash lifetime by fairly distributing the write cycles across the blocks of the device. As pointed out in Chapter 9, Flash memory is subject to a limited number of write cycles. Wear leveling should be considered a mandatory feature in any Flash-based file system you employ. As mentioned elsewhere in this book, you should consider Flash memory as a write-occasional medium. Specifically, you should avoid allowing any processes that require frequent writes to target the Flash file system. Be especially aware of any logging programs, such as syslog.

We can build a JFFS2 image on our development workstation using the ext2 image we used on our Redboot RootFS partition. The compression benefits will be immediately obvious. The image we used in the previous RootFS example was an ext2 file system image. Here is the listing in long (-1) format:

```
$ ls -l rootfs.ext2
-rw-r--r--    1 root root  6291456 Nov 19 16:21 rootfs.ext2
```

Now let's convert this file system image to JFFS2 using the mkfs.jffs2 utility found in the MTD package. Listing 10-15 shows the command and results.

# Listing 10-15
**Converting RootFS to JFFS2**

```
$ mount -o loop rootfs.ext2 /mnt/flash/
$ mkfs.jffs2 -r /mnt/flash -e 128 -b -o rootfs.jffs2
$ ls -l rootfs.jffs2
-rw-r--r--    1 root root  2401512 Nov 20 10:08 rootfs.jffs2
$
```

First we mount the ext2 file system image on a loopback device on an arbitrary mount point on our development workstation. Next we invoke the MTD utility