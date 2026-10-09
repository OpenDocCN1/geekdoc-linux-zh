When listing removable media in /etc/fstab, be sure to include the noauto flag. Otherwise, whenever you don't have the removable media in place, your boot will stop in single-user mode because a filesystem is missing.

Here's an /etc/fstab's entry for an optical drive:

/dev/cd0 /cdrom cd9660 ro,noauto 0 0

While I'm sure you've already memorized the meaning of every column in /etc/fstab, we'll remind you that this entry means, "Mount /dev/cd0 on /cdrom, using the ISO 9660 filesystem. Mount it as read-only, and don't mount it automatically at boot."

Here's a similar entry for a thumb drive. I use the large option to support filesystems larger than 128GB, as discussed in mount_msdosfs(8).

①/dev/da0 /media msdosfs rw,noauto,large 0 0

FreeBSD doesn't provide these by default, but I find having them to be much easier on systems where I use removable media regularly. Confirm that your next available da device is /dev/da0 ①, as trying to mount a hard drive that's already mounted won't work.

# ## Formatting FAT32 Media

Thumb drives use the FAT32 filesystem but always come preformatted. As thumb drives have a limited number of reads and writes directly proportional to their cheapness, do not reformat them capriciously.¹ Only reformat thumb drives when their filesystem becomes corrupt. Use newfs_msdos(8) to create a FAT32 filesystem.

```
# newfs_msdos /dev/da0
```

You'll get a couple lines of output, and you have a new filesystem.

# ## Creating Optical Media