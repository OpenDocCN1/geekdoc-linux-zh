# 9.6 cramfs

```
-s sort directory entries (old option, ignored)
-v be more verbose
-x make explicit holes (requires >= 2.3.39)
dirname root of the directory tree to be compressed
outfile output file

$ mkcramfs .../cramfs.image
warning: gids truncated to 8 bits (this may be a security concern)
$ ls -1 .../cramfs.image
-rw-rw-rw- 1 chris chris 1019904 Sep 19 18:06 .../cramfs.image
```

The mkcramfs command was initially issued without any command line parameters to reproduce the usage message. Because there is no man page for this utility, this is the best way to understand its usage. We subsequently issued the command specifying the current directory, ., as the source of the files for the cramfs file system, and a file called cramfs.image as the destination. Finally, we listed the file just created, and we see a new file called cramfs.image.

Note that if your kernel is configured with cramfs support, you can mount this file system image on your Linux development workstation and examine its contents. Of course, because it is a read-only file system, you cannot modify it. Listing 9-11 demonstrates mounting the cramfs file system on a mount point called /mnt/flash.

# Listing 9-11
Examining the cramfs File System

```
$ mount -o loop cramfs.image /mnt/flash
$ ls -1 /mnt/flash
total 6
drwxr-xr-x 1 root root 704 Dec 31 1969 bin
drwxr-xr-x 1 root root 0 Dec 31 1969 dev
drwxr-xr-x 1 root root 416 Dec 31 1969 etc
drwxr-xr-x 1 root root 0 Dec 31 1969 home
drwxr-xr-x 1 root root 172 Dec 31 1969 lib
drwxr-xr-x 1 root root 0 Dec 31 1969 proc
drwx------ 1 root root 0 Dec 31 1969 root
drwxr-xr-x 1 root root 272 Dec 31 1969 sbin
drwxrwxrwt 1 root root 0 Dec 31 1969 tmp
drwxr-xr-x 1 root root 124 Dec 31 1969 usr
drwxr-xr-x 1 root root 212 Dec 31 1969 var
```