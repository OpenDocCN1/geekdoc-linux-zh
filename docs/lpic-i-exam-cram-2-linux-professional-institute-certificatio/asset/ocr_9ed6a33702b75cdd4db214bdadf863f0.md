# The mksfs Command

The mksfs command is somewhat unique: It’s the front end for many programs for creating file systems on Linux. The mksfs command, when used with the -t fstyp option, calls the mksfs.fstyp program to make the actual file system. Here’s an example:

```
mksfs -t ext2 /dev/sda5
```

This command executes the mksfs program, supplying the type of ext2, which in turn executes the mksfs.ext2 program against the target partition, creating an Ext2 file system.

The long commands, (called file system builders) can be invoked directly, saving some time and confusion, as shown here:

```
mksfs.ext2 /dev/sda5
```

Specifying options works with whichever method you choose, so let’s focus on the shortcuts that exist for the various mksfs-specific programs:

| Command | FS Builder | Shortcut |
|---|---|---|
| mksfs | mksfs.ext2 | mke2fs |
| mksfs.ext3 | mke2fs |
| mksfs.jfs | (no shortcut) |
| mksfs.reiserfs | (no shortcut) |
| mksfs.msdos | mkdosfs |
| mksfs.vfat | mkdosfs |
| mksfs.cramfs | mkcramfs |

Other file system creation mk tools are available on the system. Here is a sample list of the important ones:

+   - mkisofs—Creates ISO file systems and is used for CD creation
+   - mknod—Creates special files (dev files, named pipes, and so on)
+   - mkraid—Creates raid sets from separate disks
+   - mkswap—Makes a partition or file into swap space for use as part of virtual memory

# File System Creation Options

Creating file systems can either be quick and default or take some time and involve a good number of options. Several examples of quick and default