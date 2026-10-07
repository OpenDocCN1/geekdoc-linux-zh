```
/dev/hda1    *    1    255    2048256    83    Linux
/dev/hda2    256    2491    17960670    5    Extended
/dev/hda5    256    893    5124703+    83    Linux
/dev/hda6    894    1021    1028128+    83    Linux
/dev/hda7    1022    1054    265041    82    Linux swap
/dev/hda8    1055    1819    6144831    83    Linux
```

# fsck

```
fsck [options] [-t fstype] filesystem
```

The fsck (filesystem check) command is used to check and repair a filesystem. This command is run at bootup by the rc.sysinit process with the -a option, which tells it to check each filesystem listed in /etc/fstab unless the sixth field for that filesystem in the /etc/fstab is zero. If it detects a problem, it will report that there was an "unexpected inconsistency." You will have the option of entering the root password to do maintenance or dropping to single-user mode, where you can run fsck manually and fix the problem. When you run it manually, fsck will evaluate the problem and fix it (although some data will most likely be lost), and make the system bootable again.

# tune2fs

```
tune2fs [options] device
```

The tune2fs command is used to fine-tune the characteristics of a filesystem. You can change the number of times the filesystem may be remounted before a filesystem check is forced, the maximum time that can elapse before it must be checked, the error behavior of the filesystem, and so on. Attempting to adjust parameters on a filesystem that is mounted as read/write will damage the filesystem! More on the usage of tune2fs is found in Chapter 16.

# mkdir

```
mkdir [options] director(y/ies)
```

The mkdir (make directory) command creates one or more directories with the names specified. If a fully qualified path is given, the directories will be created there; otherwise, they will be created in the current directory. We will discuss the mkdir command in Chapter 7. Here is an example of how it would be used to create a directory under user's home directory:

```
mkdir /home/user/new_dir
```

# mke2fs

```
mke2fs [options] device [blocks-count]
```

The mke2fs command is used to create a Linux filesystem on the specified device. The blocks-count argument sets the number of blocks on the device, although it may be omitted to allow mke2fs to set the filesystem size.

# mount

```
mount [options] [mountpoint] [device_node] [-t filesystem_type]
```

The mount command attaches the filesystem referenced as device_node to the mount point specified as mountpoint. If the filesystem is listed in the /etc/fstab file, either the mountpoint or the