
Obviously, the space available on the MTD storage device must be equal to or larger than the JFFS2 image you are placing on it. With the MTD device erased, copy the JFFS2 image to the MTD partition. For NOR flashes, you can use the dd command:

```
# dd if=images/rootfs-jffs2-summed.img of=/dev/mtd5 bs=1024
```

For NAND flashes, you must use the mtdwrite command, which takes into consideration bad blocks that are part of a NAND flash:

```
# mtdwrite -j /dev/mtd5 rootfs-jffs2-summed.img
```

Now, mount the copied filesystem to take a look at it:

```
# mount -t jffs2 /dev/mtdblock5 /mnt
# mount
...
/dev/mtdblock5 on /mnt type jffs2 (rw)
# ls mnt
bin   etc   linuxrc  sbin  usr
dev   lib   proc     tmp   var
# umount mnt
```

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_272_0.png)

The previous example shows the mtdblock device corresponding to the MTD partition that is used as the mount device, /dev/mtdblock5, in this case. Using the device name is not strictly needed, or even recommended. Instead, you can use the MTD minor number (e.g., mtd2) or even the MTD partition name (e.g., mtd5.my_root_fs) instead of the mtdblock device file name.

Unfortunately, the version of the mount command that ships with BusyBox does not work with these more straightforward formats, and because the BusyBox version of this command is used in almost all embedded Linux systems, we chose to provide the example as-is.

Also, note that you cannot use the minor number or the MTD partition-type-based naming format for specifying an MTD partition as a root filesystem on the kernel command line.

Unlike disk filesystems, JFFS2 cannot be mounted on loopback using the mount -o loop for you to view its content. Instead, it must be mounted from a real MTD device, as done previously. If you have no real MTD device on your host, such as CFI flash, you could use the virtual memory MTD device presented in Chapter 3. You could also use the jffs2reader command, introduced in the previous chapter, to view the image’s content.

If your target had previously been using an NFS-mounted root filesystem, you are now ready to boot it using the JFFS2 filesystem as its root filesystem.

## YAFFS2

Yet Another Flash Filing System, version 2 (YAFFS2) is a writable, persistent, power-down-reliable filesystem for NAND and NOR flash devices. It is widely used with Linux and RTOSes in consumer devices. It provides wear levelling and is optimized for use with NAND flash devices. YAFFS2 is dual-licensed under the GPL, but a separate license with different terms is available for a fee. The YAFFS2 website can be found at http://www.yaffs.net.

YAFFS2 is not part of the mainline Linux kernel tree and therefore requires you to obtain the sources from the project CVS repository and patch the target kernel source. The latest kernel version supported at the time of this writing is 2.6.25, according to the YAFFS2 website. Here is the procedure to patch your kernel source with YAFFS2 support:

```
$ export CVSROOT=:pserver:anonymous@cvs.aleph1.co.uk:/home/aleph1/cvs
$ cvs logon
(Just press the Return key if you are asked for a password)
$ cvs checkout yaffs2
$ cd yaffs2
$ ./patch-kex.sh $(PRJROOT)/kernel
```

Now rebuild the target kernel image. Do not forget to configure the kernel, turning on CONFIG_YAFFS_FS and related options!

After the target kernel is ready, build and install the YAFFS2 tools used to create filesystem images:

```
$ cd yaffs2/utils
$ make
$ cp mkyaffs2image /usr/bin/
```

Creating a YAFFS2 filesystem image file is quite straightforward:

```
$ mkyaffs2image $(PROJROOT)/rootfs yaffs2.img
```

This creates the filesystem image file yaffs2.img with the content of the $(PROJROOT)/rootfs directory. The convert option may also be specified on the command line in order to create cross-endian filesystem images.

You can use the same methods described in the previous section on JFFS2 to install the filesystem image on the target device flash.

## Tmpfs

Tmpfs is a filesystem stored in virtual memory. As such, it is writable but not persistent: its content is not saved across reboots. Because it can grow and shrink according to its content, it is quite useful for storing temporary files. One common use for it is to mount directories that do not require permanent storage, such as /tmp.

Tmpfs is unique in that it uses the Linux page and dentry caches for storing the file data and metadata. The Linux page cache is the kernel’s internal data structure where the kernel copies and caches pages of the data that is read, written, or executed from filesystems on physical storage devices so that code running on the CPU can interact with the pages. The Linux memory cache is a similar construct that caches information about directory entries in mounted filesystems. Please do not get confused by the use of the term “cache” here, as there is no backing store involved when Tmpfs uses these caches. Instead, the objects in the caches are the only copies of the data in the system.

A similar and related filesystem, called Ramfs, is also available. Just like Tmpfs, it is writable but not persistent, and uses the Linux page and dentry caches for storage.

In fact, Ramfs is an earlier and simpler version of the same code from which Tmpfs was derived. The two biggest differences between them, as far as functionality goes, is that data stored on a Tmpfs filesystem can be swapped to disk, whereas data in Ramfs cannot. Because swap is hardly ever used in embedded systems, this difference is of no importance. The second difference is that you can’t limit a Ramfs filesystem’s size, and therefore you can’t limit its memory use, but you can with Tmpfs.

In Linux kernel version 1.6.19, another functional difference has cropped up between Tmpfs and Ramfs: files on a Tmpfs filesystem can now be exported via the internal Linux NFS server, whereas no such support is available to Ramfs filesystems.

Tmpfs should always be preferred to Ramfs, except for very special circumstances.

To use Tmpfs, enable the “Virtual memory filesystem support (former shm fs)” item in the “Filesystems” submenu of the kernel configuration menu.

With kernel support for Tmpfs enabled, you can mount a Tmpfs filesystem on /tmp, which will use up to 4 MB of RAM; for example:

```
# mount -t tmpfs none /tmp -o size=4m
```

Alternatively, you can add a line in your /etc/fstab file and modify your /etc/init.d/rcS file to mount Tmpfs at boot time. If you do not provide a size limit, the filesystem will grow in accordance with its content up to half of the available RAM. If maximum filesystem size is exceeded, file operations requiring more storage space will fail with an appropriate error.

In contrast with most other mount commands, Tmpfs does not require a device or file to be mounted. Hence the use of none as the device in the previous example. mount ignores the name of the device for Tmpfs, and replacing none with any other name would have no effect on the command.

## Writing a Filesystem Image to Flash Using an NFS-Mounted Root Filesystem

Although Chapter 9 will discuss the setup and configuration of the NFS server on the host for providing a root filesystem to a target, let’s take a look at how this configuration can be useful at this stage.

Exporting a root filesystem from the host to the target over NFS during early development stages simplifies the development process by allowing quick modification of the files the target used. Later, the target needs to have a filesystem stored in its flash in order to be self-hosting. Although some bootloaders can be used to copy images to flash, you can also use the MTD utilities running on the target to copy files available on the NFS-mounted root filesystem. To do so, copy the designated filesystem image to the directory on the host containing the NFS-mounted target root filesystem, boot the target, and use MTD commands on the target to copy the filesystem image to flash.

To copy an initial RAM disk image to your target’s flash, for example:

1. Configure your target to mount its root filesystem from a directory exported by your host using NFS.
2. On your host, copy the filesystem image to the directory exported to your target. Though the filesystem image is not physically on your target, it will be visible on its root filesystem once the kernel mounts it using NFS at startup.
3. Boot your target and use the MTD utilities on your target to copy the filesystem image from the NFS-mounted root filesystem to the appropriate flash device entry in your target’s /dev directory.

## Placing a Disk Filesystem on a RAM Disk

RAM disks, as their name indicates, live in RAM and act like block devices. The kernel can support many active RAM disks simultaneously. Because they act like block devices, any disk filesystem can be used with them. But because their content lasts only until the system is rebooted, RAM disks are usually reserved for compressed images of disk filesystems, such as Ext2 filesystems. These images are known as compressed RAM disk images.

One instance where the use of such compressed RAM disk images is particularly attractive for embedded Linux systems is during system initialization. Specifically, the kernel can extract an initial RAM disk (initrd) image from a storage device for use as its root filesystem.

At startup, the kernel verifies whether its boot options indicate the presence of an initrd. If so, it extracts the filesystem image, whether or not it is compressed, from the designated storage media into a RAM disk, and mounts it as its root filesystem. Up to kernel version 2.6, the initrd mechanism was, in fact, the simplest method to provide a kernel
