```
# mount -t ext2 /dev/hdb1 /home
```

mounts the file system on /dev/hdb1 on /home.

Note that you usually have to be root to mount and unmount file systems.

# # Mounting a File System Automatically

It would be a real chore to have to type mount commands each time you wanted to mount file systems. The file /etc/fstab contains lines describing file systems which should be mounted when the system boots.

# ## Background Material

This file may be named something else on other UNIX systems. On Solaris, for example, it's called /etc/vfstab.

Each line of /etc/fstab looks something like this:

```
# Comment line -- lines starting with # are ignored
# device   mount_point  type   opts        dump fscsk
/dev/hda1  /            ext2   defaults    1      1
/proc      /proc        proc   defaults    0      0
/dev/hdc   /mnt/cdrom   iso9660 ro,nouser,noauto 0  0
```

Each line either is blank, is a comment line (starting with #), or consists of six fields:

+   * The device field specifies the device that is to be mounted.
+   * The mount_point field specifies where the file system is to be mounted. We see that my root file system is held on /dev/hda1.

# ## Background Material

This is a chicken-and-egg problem. How do we know that it holds the root file system until we read /etc/fstab, which is itself on the root file system? In fact, the kernel uses a different mechanism to mount the root file system; it's included in /etc/fstab for the benefit of startup scripts, which check file system integrity.

+   * The type field specifies the file system type. My root file system is ext2, the /proc pseudo-file system is of type proc, and my CD reader usually mounts file systems of type iso9660. This type is fed to mount via the -t option.
+   * The opts field specifies any options to be passed to mount. They are given as a comma-separated list with no spaces between items. Most file systems simply have