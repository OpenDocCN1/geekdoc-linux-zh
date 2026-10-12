Now we can run `fsck` on the partition. When done,

```
# mount -o rw,remount /home
```

puts it back in service.

If you reboot your system to mount the root file system read-only for maintenance (enter the maintenance mode, s, as described in Chapter 15)

```
# mount -o rw,remount /
```

will remount it read-write and you can continue on. That’s easier than unmounting and remounting the device.

# Converting an Existing ext2 File System to ext3

An existing ext2 file system is easily converted to ext3 to take advantage of the benefits of journaling. After you convert an existing file system, any other operating system—including BeOS, Windows (with the appropriate drivers), and other UNIX systems that have drivers to access ext2 partitions—can access ext3 partitions. To those operating systems (and their drivers), your converted file system still looks just like an ext2 file system.

To begin the conversion to ext3, you use the tune2fs utility to add the journal to an existing ext2 file system. In this example, you are changing /dev/hda2, an already formatted ext2 partition.

```
# tune2fs -j /dev/hda2
```

It does not matter whether hda2 is mounted or unmounted at the time of the migration; if it is mounted, you will see a new file, .journal, in the directory.

Next, edit the line for /dev/hda2 in /etc/fstab and change the value from ext2 to ext3. It will be mounted as an ext3 file system the next time you reboot.

> **NOTE**
> 
> If you have decided to convert your root file system to take advantage of the benefits of the ext3 file system, bear in mind that you cannot run tune2fs -j on it while it is unmounted because you cannot unmount the root file system. Because the file system is mounted when you run tune2fs -j, the .journal file on it will be visible when you finish the migration. When compiling a new kernel, make certain to include ext3 file system support in your new kernel by selecting that choice in your kernel configuration (see Chapter 39, “Kernel and Module Management”). Also, note that you do not need to perform the actions described in the next section if you have just freshly installed.

# Making an Initial Ramdisk

You need to create an inrtd image file to load the ext3 driver and mount the root partition as an ext3 partition. The inrtd file is an initial ramdisk that contains a small kernel