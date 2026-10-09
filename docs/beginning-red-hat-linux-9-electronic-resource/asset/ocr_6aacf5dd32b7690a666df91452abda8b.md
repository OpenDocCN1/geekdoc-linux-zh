# Managing Drives and Partitions

Now that we have seen several aspects of the file system from an end user’s perspective, we will look at some of the administrative aspects of the file system such as the different drives on a system and its partitions. Apart from the hard disks on a system, there is almost always a floppy disk drive and a CD-ROM drive, both of which are treated as file system drives. In addition, certain other peripheral devices such as digital cameras or removable storage devices may present the storage available on them as file system drives. A drive may be **mounted** – that is, made available for use by the file system. The drive may also be **unmounted**, making it unavailable for the file system to use.

We can list the currently mounted drives on a system using the `df` or `mount` commands. Let us look at the output of the `df` command:

```
$ df -k
File system      1K-blocks    Used Available Use% Mounted on
/dev/hda2        5716172  3426868   1998932  64% /
/dev/hda1        101089    19137     76733  20% /boot
none              94752       0     94752   0% /dev/shm
/dev/fd0           1423      105      1318   8% /mnt/floppy
/dev/cdrom         661728   661728     0  100% /mnt/cdrom
```

The `–k` option to `df` causes it to report partition sizes in kilobytes.

In the listing above, we see that:

+   * The first IDE hard disk `/dev/hda` has two partitions, `/dev/hda1` and `/dev/hda2`
+   * The floppy drive is the `/dev/fd0` drive
+   * The `/dev/cdrom` drive represents a CD-ROM drive.

In addition, there is a drive marked `none` which (in this case) represents a temporary file system (`tmpfs`) necessary for certain shared-memory operations.

With the other drives, besides the space usage numbers on each of them, the thing to note is the Mounted on column. This represents the directory that these file systems are mapped on to. Therefore:

+   * The `/dev/hda2` partition contains a file system that is mapped on to the `/` or the root directory.
+   * The `/dev/hda1` partition contains another file system that is mapped on to the `/boot` directory.

What this means is that each time we execute the `cd /` command or the `cd /etc` command, we are actually accessing a file system on the second partition of the only hard disk on this system. Also, executing `ls -1 /mnt/cdrom` will list the top-level files and subdirectories of the currently mounted CD in the CD-ROM drive.