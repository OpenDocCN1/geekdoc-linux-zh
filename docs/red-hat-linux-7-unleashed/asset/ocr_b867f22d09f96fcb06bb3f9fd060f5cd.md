# mk2fs

The **mk2fs** command is used to make a second extended Linux filesystem on a specified hard drive or other device, such as a floppy disk. This command does not format the new filesystem, but makes it available for use. **mk2fs** can also be used to label a partition and to specify a mount point or directory where the partition can be accessed after it is mounted.

# mkfs

**mkfs** is used to build a Linux filesystem on a device, usually a hard disk partition. The syntax for the command is **mkfs** *filesystem*, where *filesystem* is either the device name (such as `/dev/hda1`) or the mount point (for example, `/`, `usr`, `/home`) for the filesystem.

# mkswap

**mkswap** sets up a Linux swap area on a device (usually a disk partition).

The device is usually of the following form:

```
```
/dev/hda[1-8]
/dev/hdb[1-8]
/dev/sda[1-8]
/dev/sdb[1-8]
```
```

# mlabel

The **mlabel** command, part of the mtools package, is used to label (name) a DOS floppy disk.

# more

**more** is a filter for paging through text one screen at a time. This command can only page down through the text, as opposed to **less**, which can page both up and down though the text.

# mount

**mount** attaches the filesystem specified by *specfile* (which is often a device name) to the directory specified as the parameter. Only the superuser can mount files. If the **mount** command is run without parameters, it lists all currently mounted filesystems. The following is an example of the **mount** command:

```
```
svr01:/home/dpitts$ mount
/dev/hda1 on / type ext2 (rw)
/dev/hda2 on /var/spool/mail type ext2 (rw,usrquota)
/dev/hda3 on /logs type ext2 (rw,usrquota)
/dev/hdc1 on /home type ext2 (rw,usrquota)
none on /proc type proc (rw)
```
```

![](bbox=[0.85, 0.79, 0.97, 0.94])