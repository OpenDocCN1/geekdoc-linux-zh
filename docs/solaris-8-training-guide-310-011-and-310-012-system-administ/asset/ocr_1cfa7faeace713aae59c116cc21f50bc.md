> NOTE
If fsname and volume are not specified, labelit prints the current values of these labels. Both fsname and volume are limited to six or fewer characters.

# TABLE 7.2

# THE labelit COMMAND

| Parameter | Description |
|---|---|
| special | This name should be the physical disk section (for example, /dev/dsk/c0t0d0s6). |
| fsname | This represents the mount point (for example, root (/), /home, and so on) of the file system. |
| volume | This can be used to represent the physical volume name. |
| -F | This specifies the file system type on which to operate. The file system type should either be specified here or be determinable from the /etc/vfstab entry. If no matching entry is found, the default file system type specified in /etc/default/fs is used. |
| -v | This prints the command line but does not perform an action. |

The following is an example of how to label a disk partition using the labelit command. Type the following:

```
labelit -F ufs /dev/rdsk/c0t0d0s6 disk1 vol1
```

The system responds with this:

```
fsname:  disk1
volume:  vol1
```

# The volcopy Command

The administrator (root) can use the volcopy command to make a copy of a labeled file system. This command works with ufs file systems, but the file system must be labeled with the labelit utility before the volcopy command is issued. To determine if a file system is a ufs file system, issue this command:

```
fstyp  /dev/rdsk/c0t0d0s6
```

The system responds with this:

```
ufs
```

The volcopy command can be used to copy a file system from one disk to another.