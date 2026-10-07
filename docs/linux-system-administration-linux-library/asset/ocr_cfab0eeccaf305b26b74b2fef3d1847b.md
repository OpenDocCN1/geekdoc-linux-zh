# Disk Access without a Filesystem

It's possible to access a floppy disk without using a filesystem per se. This is commonly done by writing a tar file directly to a floppy disk. Suppose you want to transfer a directory, somidir, between systems. You can do so by issuing the following command on the source system:

```
$ tar -cvf/fd0 somidir
```

This command copies the contents of somidir to a tar file on the floppy disk. You can reverse the process on the target system by issuing this command:

```
$ tar -xvf /dev/fd0
```

Of course, you can also transfer tar files in a similar way by mounting a disk with a filesystem and then using an appropriate tar file on the disk (as /mnt/floppy/somidir.tar) rather than the device file (/dev/fd0). Why use direct access, it's most useful when transferring files between versions of Unix that don't share an common filesystem. You can be sure that a tar file written without a file-system can be read by any Unix-like OS, because tar is so widely available. Support for any given filesystem is not so universal, although FAT filesystem support is extremely common on modern Unix.

One unusual shortcut for access to floppy disks is the Mtools package. It's a set of programs that allow access to FAT floppy disks (or, in principle, other removable media formatted with FAT) without explicitly mentioning them. Mtools includes a series of commands named after DOS disk-access commands. These include mkdir (to create a directory), mcopy (to copy a file), mdel (to delete a file), and mformat (to create a FAT file on a system). These commands use a DOS-style drive letter in place of Linux's device identifier. For instance, to copy a file to a floppy, you would type mcopy filename:: Mtools is a very useful method for copying a few files or from a FAT floppy, but if you want to give programs direct access to files on a floppy, you must mount it normally. Mtools comes with most Linux distributions. You can read more about it at http://mtools.linux/

A package similar to Mtools, called HFS Utilities, exists for accessing Macintosh floppies (http://www.mars.org/home/proj/hfs/). These utilities use an h prefix to the DOS-style commands, as in hdir and hformat. The package also includes a GUI front-end.