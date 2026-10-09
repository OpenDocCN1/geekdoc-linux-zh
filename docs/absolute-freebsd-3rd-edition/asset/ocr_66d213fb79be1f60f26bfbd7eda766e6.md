hosts have very few optical drives. If you have one optical drive, it's /dev/cd0. USB devices appear as the next available unit of /dev/da. When you insert a USB device, a message giving the device node and type appears on the console and in /var/log/messages, or you could check camcontrol devlist for the new device.

FreeBSD provides a /media mount point for general removable media mounts. You can create additional mount points as you like—they're just directories. For miscellaneous short-term mounts, FreeBSD offers /mnt.

So, to mount your FAT32 USB device /dev/da0 on /media, run:

```
# mount -t msdosfs /dev/da0 /media
```

Occasionally, you'll find a thumb drive with a partition table. These devices will insist you mount /dev/da0s1 or /dev/da0p1 rather than /dev/da0. The device's formatting dictates this, not anything in FreeBSD. The part show command can help you figure out which partitions are on a device and what filesystem is on each partition.

# ## Ejecting Removable Media

To disconnect removable media from your FreeBSD system, first unmount the filesystem. Your optical drive won't open until you unmount the disk. You can pull a USB flash drive from its port, but doing so while the filesystem is mounted might damage data on the device. Use unmount(8) just as you would for any other filesystem:

```
# unmount /media
```

On many optical drives, camcontrol eject opens the drive tray.

# ## Removable Media and /etc/fstab

You can update /etc/fstab with entries for removable media to make system maintenance a little easier. If a removable filesystem has an entry in /etc/fstab, you can drop both the filesystem and the device name when mounting it. This means that you don't have to remember the exact device name or filesystem to mount the device.