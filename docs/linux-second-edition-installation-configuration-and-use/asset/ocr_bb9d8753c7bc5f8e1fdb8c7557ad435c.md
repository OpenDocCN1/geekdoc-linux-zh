# dd [options]

dd transfers data between different storage media (hard disk, diskette, and so on), and if required, carries out a data conversion. The command can be used to exchange data data between different computer architectures.

dd can not copy single files, but also accesses devices directly. This can be used to copy entire hard disks (or partitions), modify the boot sector of a hard disk, and so on. There is no need to create a file system on the hard disk or diskette.

When dd is used without options, it reads the data from the standard input (keyboard, terminated by Ctrl+Z) and writes to the standard output (screen). Please note that the options of dd must be specified without preceding minus signs!

```
conv=mode
```

converts the data during the copying process. There exist various settings for mode, such as case (upper case into lower case letters), ucase (lower case into upper case), swap (swaps 2 bytes at a time), and so on.

```
bs=n
```

specifies the block size for input and output files. (The block size determines how many bytes are read or written at once.)

```
count=n
```

copies n blocks (not all data).

```
ibs=n
```

specifies the block size of the source file.

```
if=source.file
```

specifies the source file (instead of the standard input).

```
obs=n
```

specifies the block size of the target file.

```
of=target.file
```

specifies the target file (instead of the standard output).

# Examples

```
user dd if=/dev/hda of=/boot/bootsector.bak bs=512 count=1
```

transfers the boot sector of the first IDE hard disk into the backup file sector.bak.

```
user dd if=/vmlinux of=/dev/fd0
```

copies the kernel directly into the first sectors of the diskette, which can then be used as a boot diskette.

```
df [options]
```

df provides information about the points in the directory tree where hard disks (partitions) or other drives are mounted and how much free storage is available on each.