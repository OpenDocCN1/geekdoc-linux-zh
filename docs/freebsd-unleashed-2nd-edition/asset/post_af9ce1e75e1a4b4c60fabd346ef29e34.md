
## The `umount` Command

One other useful argument to note is the `options` field, in which you can specify any code words (flags) from a large list of code words, separated by commas. Most useful are the ones specifying whether the filesystem is read-only or read/write; it is read/write by default, but you can use the `-ro` or `rdonly` option to make it read-only. See `man mount` for a full list of mount options.

There will also come the time when you have to "unmount" a filesystem; the command for this is `umount` (rather than "unmount"). To unmount the `/home` filesystem, issue the following command:

```
# umount /home
```

You can also use `umount /dev/ad1s1g` to accomplish the same result, or even `umount -a` to unmount everything except for the root filesystem.

Unmounting filesystems is a much simpler procedure than mounting them, with only one major complicating factor: For a filesystem to be unmounted, it cannot be in use. This means that to unmount filesystems such as `/usr` and `/var`, you will probably have to be in single-user mode. For the `/home` partition in the example in the previous section, any connected users will likely be in their home directories, so they will have to be kicked off the system before `/home` can be unmounted. This factor leads to the most common surprise most users find when first experimenting with `mount` and `umount`: You can't be inside a filesystem you're trying to unmount! If you are, you'll get a "Device busy" error message. To be safe, be in the habit of entering `cd /` before you attempt to unmount.

Like `mount`, `umount` has the `-f` option to force an unmount. But again, it's best to avoid using it unless absolutely necessary; filesystem operations have the potential to destabilize the system if done in a messy manner.

### Mounting and Unmounting Filesystems from Other Operating Systems

The techniques you've just learned are all well and good for standard FreeBSD filesystems. But what if you need to mount a disk from a Linux box or from a Windows 98 or NT machine? You can do that. FreeBSD supports the filesystems listed in Table 8.2 (the GENERIC (default) kernel).

**TABLE 8.2** Filesystems Supported in the GENERIC Kernel

| Filesystem | Name |
|---|---|
| FFS | Berkeley Fast Filesystem |
| MFS | Memory Filesystem |
| NFS | Network Filesystem |
| MSDOSFS | MS-DOS Filesystem |
| CD9660 | ISO 9660 (CD-ROM) Filesystem |
| PROCS | Process Filesystem |

There is also support for the filesystems shown in Table 8.3, but they need to be compiled into a custom kernel in order to work (see “Compiling and Installing the Custom Kernel,” in Chapter 16).

**TABLE 8.3** Additional Available Filesystems

| Filesystem | Name |
|---|---|
| FDSC | File Descriptor Filesystem |
| KERNFS | Kernel Filesystem |
| NTFS | NT Filesystem |
| NULLFS | NULL Filesystem |
| NWFS | NetWare Filesystem |
| PORTAL | Portal Filesystem |
| SMBFS | SMB/CIFS Filesystem (Windows) |
| UMAPFS | UID Map Filesystem |
| UNION | Union Filesystem |
| CODA | CODA Filesystem |
| EXT2FS | Ext2 Filesystem (Linux) |

Some of these latter filesystems are more stable than others. As you saw earlier, union filesystems are available as an option, but they are only partially in a working state (and can damage your system). Therefore, it is not recommended that you use them unless absolutely necessary. EXT2FS and NTFS support is also given a caveat about completeness and stability. Filesystems that are not built in to the GENERIC kernel, in general, are not included for a reason.

The ideal circumstance for a filesystem type that isn’t part of the existing kernel is to be available as a kernel module in /modules, as many of the filesystems listed in the preceding tables are. If the filesystem is available as a kernel module, it will be automatically loaded when you try to mount the filesystem. At the time of this writing, these available modules include CODA, PORTAL, NWFS, NULL, NTFS, UNION, and some others that are already compiled into the GENERIC kernel and are provided in /modules for compatibility.

If you’re mounting a filesystem (MSDOSFS, for example) that is supported in the default kernel, or if you decide to accept the risks and plunge ahead with mounting a filesystem that isn’t initially built in, you’ll find that FreeBSD does provide some handy tools for doing the actual mounting. The following tools are available in /sbin (although their names may vary according to your version of FreeBSD):

- mount_cd9660*
- mount_ext2fs*
- mount_fdesc*
- mount_kernfs*
- mount_linprocfs*
- mount_mfs*
- mount_msdosfs*
- mount_nfs*
- mount_ntfs*
- mount_nullfs*
- mount_nwfs*
- mount_portalfs*
- mount_procfs*
- mount_smbfs*
- mount_std*
- mount_umapfs*
- mount_unionfs*

Each of these variations on mount corresponds to one of the supported filessystems and operates in the same way as mount. The idea is that these mount_* tools serve as an extension to the -t option to mount. The -t option recognizes only a couple internal filesystem types; if you give it an unrecognized argument, it will execute the corresponding tool from the previous list. For example, if you use mount -t nfs /mnt, the tool will actually execute mount_nfs /mnt. Knowing this, it is often easier simply to run the latter tool directly.

> **NOTE**
>
> As a further note on the stability and completeness issues regarding the not fully supported filesystem types, you should read the man mount_* pages. Each one gives a good account of what is deficient in that filesystem's support. For example, man mount_ntfs discusses the lack of full write capabilities and support for compressed files, and man mount_union warns about the feature's limited functionality and potential to damage data. Be informed!

### Mounting a Windows/MS-DOS Filesystem

Let's first look at mounting a Windows 98 disk, which will be MSDOSFS for FreeBSD's purposes. The command you use for this operation is mount_msdos. This command can take some special options that we do not need to cover fully here. Examples are -w and -L, which control the locale-based character mapping for the long filenames associated with FAT32/VFAT filesystems. For this example, you can use the default settings, which assume that the ISO 8859-1 encoding will be used and that you will read and write to the filesystem as root:

```
# mount_msdos /dev/ad1s1 /mnt
```

For versions of FreeBSD prior to 5.0, use these settings:

```
# mount_msdos /dev/ad1s1 /mnt
```

Bear in mind that what DOS and Linux systems call partitions are called slices in FreeBSD, to avoid confusing them with traditional BSD partitions (which are subdivisions of slices). Therefore, because your Windows 98 filesystem on /dev/ad1s1 is effectively using a slice rather than a partition, you can address it simply by its slice number rather than specifying additional suffixes, as when mounting standard FreeBSD filesystems, where you use /dev/ad1s1g.

If you're using an extended DOS partition, you may get an "Invalid argument" error. If this happens, note that extended DOS partitions are numbered beginning with 5, so your device name will be `/dev/ad1s5`.

You can perform additional tricks when mounting an MS-DOS filesystem, such as mounting it as a non-root UID/GID, mounting it with a permissions mask for controlling users' access to the filesystem's contents, listing it with long filenames (instead of short filenames), and so forth. Refer to man `mount_msdos` for the full documentation on these options.

> **TIP**
>
> A Windows floppy disk contains filenames that can be in the standard MS-DOS "8.3" short format or in the Windows 95/98 long format, which is derived from metadata in the filesystem. If you mount a Windows floppy disk using `mount_msdos`, FreeBSD attempts to find any of these long filenames on the disk. If it finds any, it uses that format to list and interact with the files. However, if it finds none of these long filenames but does find short ones, it will use the short format. To force `mount_msdos` to use the long format, use the `-l` option. The `-s` option forces the use of the short format.

### Mounting a Linux Filesystem

Most Linux systems use EXT2FS. Because EXT2FS is not built in to the `GENERIC` kernel, this task involves an extra step. (EXT2FS support will eventually be available in a loadable kernel module, but not as of the time of this writing.) Chapter 16 discusses the steps involved in compiling and installing a custom kernel; the line you want to add to your custom kernel configuration file (preferably at the end of the block of options lines) is the following:

```
options          EXT2FS
```

After your system is up and running with the new kernel, you can use the following command:

```
# mount_ext2fs /dev/ad1s1 /mnt
```

Other than the kernel support, `mount_ext2fs` behaves almost identically to standard `mount`, so the surprises should be minimal.

### Using fdisk to Gather Partition Information

You can determine what filesystem you're working with by using the `fdisk` command. Here's an example:

```
# fdisk /dev/ad1
****** Working on device /dev/ad1 ******
parameters extracted from in-core disklabel1 are:
cylinders=1247 heads=255 sectors/track=63 (16065 blks/cy1)
```
