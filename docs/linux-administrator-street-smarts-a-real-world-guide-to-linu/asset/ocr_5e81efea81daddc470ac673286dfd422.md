but an ordinary directory. Thus, the command to create a mount point is the same as the command to create a directory: `mkdir`. To create the `/home2` mount point, type this command:

```
# mkdir /home2
```

The basic form of the `mount` command is fairly simple: Type the command name followed by the device file for the filesystem and the mount point:

```
# mount /dev/sda1 /home2
```

Once this is done, you can verify that it’s been mounted in several ways. One is to check the mount point for files:

```
# ls /home2
10st+f+ound
```

Of course, a freshly minted filesystem will contain no files. This example shows one file (actually, a directory): `10st+f+ound`. Ext2fs and ext3fs use this directory to store files that have been recovered in disk maintenance operations. Most other filesystems don’t use this directory or create it only when it’s needed. Of course, if you mount a filesystem that you know already contains files, you should see them.

Another check of the filesystem’s presence is to use `df`. You can specify the mount point or device filename to limit the output of this command:

```
# df /home2
Filesystem 1K-blocks Used Available Use% Mounted on
/dev/sda1 75733 4127 67696 6% /home2
```

This output reveals that the filesystem has been successfully mounted. You might consider it odd that `df` claims that 6 percent of the filesystem is in use. Most of this space is consumed by the filesystem’s journal—recall that in Task 4.4, a journaling ext3 filesystem was specified. Some journaling filesystems consume even more space. For instance, using ReiserFS on this partition would result in 42 percent use at mount time. These figures are a consequence of the small size of the sample partition, though; on partitions of reasonable size (measured in the gigabytes), the journal size isn’t a major concern.

If a filesystem is described in `/etc/fstab`, you can use a shorthand notation in which you specify only the mount point or only the device filename, not both:

```
# mount /home2
```

Even ordinary users can issue this form of the `mount` command under certain circumstances, as described in the next task.

# Additional mount Options

The `mount` command supports a number of options that modify its behavior. The most important of these is `-t`, which accepts a filesystem type code:

```
# mount -t ext3 /dev/sda1 /home2
```