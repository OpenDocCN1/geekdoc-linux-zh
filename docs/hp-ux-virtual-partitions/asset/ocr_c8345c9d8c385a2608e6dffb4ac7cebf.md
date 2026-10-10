+   *   -m    The minor number of the device is supplied.
+   *   -r    Create a character, also known as a raw device file. The default is to create a block file.
+   *   -v    Use verbose output, which prints the name of each special file as it is created.

We will now create the device files for a disk drive. Both a block and a character device file are required. The $0x005000$ in the example corresponds to the address of 5 on the disk drive. This number, used in both the block and character device files, is unique for every disk drive created.

We can now create a block device file for a disk at SCSI address 5 using the following `mksf` command:

(on Series 700)

```
$ /sbin/mksf -v -C disk -m 0x005000 /dev/dsk/c0t5d0
making /dev/dsk/c0t5d0 b 31 0x005000
```

Similarly, we can now create a character device file for a disk at SCSI address 5 using form two of `mksf`:

(on Series 700)

```
$ /sbin/mksf -v -r -C disk -m 0x005000 /dev/dsk/c0t5d0
making /dev/rdsk/c0t5d0 c 188 0x005000
```