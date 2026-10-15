access permissions, which can be automatically used whenever you mount a file system. You needn't enter this information as arguments to a mount command as you otherwise must. This feature is what allows mount utilities on GNOME or KDE to enable you to mount a file system simply by clicking a window icon. All the mount information is already in the /etc/fstab file. For example, when you add a new hard disk partition to your Linux system, you most likely want to have it automatically mounted on startup, and then unmounted when you shut down. Otherwise, you must mount and unmount the partition explicitly each time you boot up and shut down your system. To have Linux automatically mount the file system on your new hard disk partition, you only need to add its name to the fstab file. You can do this by directly and carefully editing the /etc/fstab file to type in a new entry.

An entry in an fstab file contains several fields, each separated from the next by a space or tab. These are described as the device, mountpoint, file system type, options, dump, and fsck fields, arranged in the sequence shown here:

```
<device> <mountpoint> <filesystemtype> <options> <dump> <fsck>
```

The first field is the name of the file system to be mounted. This entry can be either a device name or an ext2 or ext3 file system label. A device name usually begins with /dev, such as /dev/hda3 for the third hard disk partition. A label is specified by assigning the label name to the tag LABEL, as in LABEL=/ for an ext2 root partition. The next field is the directory in your file structure where you want the file system on this device to be attached. These are empty directories to be used for file systems, such as /dev/floppy. The third field is the type of file system being mounted. Table 30-7 provides a list of all the different types you can mount. The type for a standard Linux hard disk partition is ext3. The next example shows an entry for the main Linux hard disk partition. This entry is mounted at the root directory, /, and has a file type of ext3:

```
/dev/hda3   /   ext3   defaults   0   1
```

The following example shows a LABEL entry for the hard disk partition, where the label name is /:

```
LABEL=/   /   ext3   defaults   0   1
```

# Auto Mounts

The file system type for a floppy may differ depending on the disk you are trying to mount. For example, you may want to read a Windows-formatted floppy disk at one time and a Linux-formatted floppy disk at another time. For this reason, the file system type specified for the floppy device is auto. With this option, the type of file system formatted on the floppy disk is detected automatically, and the appropriate file system type is used.

```
/dev/fd0   /mnt/floppy   auto   defaults,noauto   0   0
```