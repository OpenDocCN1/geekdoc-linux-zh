Mount it as follows:

```
```
# mount -o loop /tmp/intrd-2.6.7-1.478.img /mnt/image
```
```

and browse the directory to your heart's content.

Not every system has an **initrd.img** file. It is typically used to load device drivers for file systems (such as Reiser) or hardware (such as the Promise RAID IDE controller) that must be in place before the system can continue booting. Some floppy-disc-based Linux distributions use **initrd.img** to load a minimal operating system that can then uncompress and load the working file system from the floppy.

You can also mount **.iso** images in the same way, but remember that they are always read-only because of the nature of the underlying **iso9660** file system; you can write to the other images unless you explicitly mount them as read-only. If you want to read and write to the files in an ISO file system, you must first copy the files to a device that is mounted read-write, make your changes, and then use **mkisofs** to create a new **.iso** image. This is a common “gotcha” for many users.

# ## Relevant Fedora and Linux Commands

You use these commands when managing file systems in Fedora:

+   * **df**—Shows free disk space
+   * **du**—Displays disk usage
+   * **dumpt**—An ext2 file system backup utility
+   * **dump2fs**—Shows information about an ext2 file system
+   * **efisadm**—Administers an LVM/ext2 file system
+   * **e2image**—Creates an image file of ext2 file system data
+   * **fdisk**—The standard Linux partition table editor
+   * **fsck**—Checks or repairs a file system
+   * **lsraid**—Displays information about Linux RAID devices
+   * **mformat**—Formats a DOS floppy disk; part of the Mtools suite of tools
+   * **mkfs**—Creates various file systems and acts as a wrapper for the actual programs that do the work
+   * **mkisofs**—Creates a CD-ROM file system in **iso9660** format
+   * **mkreiserfs**—Creates a Linux reiserfs file system
+   * **mkswap**—Prepares a Linux swap device
+   * **mount**—Mounts a supported file system
+   * **parted**—The GNU partition editor and resizing utility
+   * **reiserfsck**—Checks a Linux reiserfs file system
+   * **resize_reiserfs**—Resizes a Linux reiserfs file system
+   * **sbmount**—Mounts an smbfs file system
+   * **stat**—Shows file or file system status
+   * **swapon**—Displays swap usage or start using system swap device