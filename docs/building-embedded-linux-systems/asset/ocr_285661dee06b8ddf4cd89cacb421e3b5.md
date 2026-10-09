The major number of the node

The minor number of the node

Here is a simple example:

```
dir /dev 755 0 0
nod /dev/console 644 0 0 c 5 1
nod /dev/loop0 644 0 0 b 7 0
dir /bin 755 1000 1000
slink /bin/sh busybox 777 0 0
file /bin/busybox initrafs/busybox 755 0 0
dir /proc 755 0 0
dir /sys 755 0 0
dir /mnt 755 0 0
file /init initramsf/init.sh 755 0 0
```

The Linux kernel build does not rely on any external utility to create or extract the CPIO created; the code to do this is self-contained. However, should you want to create an lntmams CPIO archive yourself, run the `cpio` utility as follows:

```
$ cd ${PRODJOIR}/rootfs
$ find . | cpio -o -H newc | gzip > ${PRODJOIR}/initrums.cpio.gz
```

For completeness, the following commands may be used to extract an already existing GZIP-compressed CPIO archive:

```
$ gunzip initrums.cpio.gz
$ cpio -1 -d -H newc -F initrums_data.cpio --no-absolute-filenames
```

> The `cpio` manpage contains some bad advice that will break your Initrams archive if you follow it. It says: "A typical way to generate the list of filenames is with the `find` command; you should give `find` the -depth option to minimize problems with permissions on directories that are unwritable or unsearchable." This will not work while creating an Inltrams archive, because the Linux kernel CPIO extractor will refuse to create files in a directory that does not exist. Therefore, directory entries must precede the files that go in those directories. The example shown in this section will produce a correct CPIO archive.

![](bbox=[0.15, 0.57, 0.24, 0.61])

If the kernel is compiled with Initial RAM disk support (Inltrd), an external compressed CPIO archive can also be used by the Linux kernel in place of a RAM disk. The kernel will detect that the type of the Iinird is an Initrams archive and not a filesystem image, and will extract the content of the archive into the Roots prior to attempting to locate the `init` program (which by default is located in `/sbin/init`. The files in this external archive will overwrite any file in the initial built-in archive in the kernel image file. Because Inlrums uses the Linux dentry and page caches to store the file and metadata content of the filesystem, an lntrums can make much more efficient use of system