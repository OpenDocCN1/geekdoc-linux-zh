# cpio - Copy File Archives In Out

# Synopsis

```
/usr/bin/cpio -i [bbcdfkmPrStuvV60] [-C bufsize] [-E file]
[-H header] [-I -M message] [-R id] [pattern...]
/usr/bin/cpio -o [aAbcPV@] [-C bufsize] [-H header] -O 0 file
[-M message]
/usr/bin/cpio -p [adlmPuvV60] [-R id] directory
```

Use the cpio command to copy files, special files used to represent peripheral devices attached to a system; and file systems that require multiple tape volumes. cpio provides compatibility for copying files from SunOS 5.x systems to SunOS 4.x systems. Advantages of using the cpio command are that it packs data onto tape more efficiently than the tar command, skips over any bad spots on tape when restoring files, provides options for writing files with different header formats (tar, ustar, crc, odc, bar) for portability between different system types, and creates multiple tape volumes.
cpio command, when used to create an archive, takes a list of files or path names from standard input and writes to output. The output is almost always redirected to a file or to device.
You use the -i (copy in), -o (copy out), or -p (pass) option to choose the actions to perform.

> Note - cpio assumes 4-byte words. When writing to a character device (-o) or reading from a character device (-i), cpio reaches the end of the medium (as the end of a diskette) and you do not use the -0 and -I options, cpio prints the following message: To continue, type device/file name when. To continue, you must replace the device and type the character special name (/dev/rds, for example) and press Return. You may continue by directing cpio to use a different device. For example, if you have two disk drives, you may want to switch between so cpio can proceed while you are changing the disksettes. (Simply pressing Return exits cpio.)

In the Solaris 9 Operating Environment, the UFS, NFS, and TMPFS file systems are enhanced to include extended file attributes. These attributes enable developers to associate specific attributes with a file. For example, a developer of file management application for a windowing system might associate a display icon with a file. You can use the new -e option to copy extended file attributes.

# Copy-In Mode

cpio -i (copy in) extracts files from the standard input, which is assumed to be the product of a previous cpio -o. Only files that match patterns are selected.
Extracted files are conditionally created and copied into the current directory, the permissions of the files are those of the previous cpio -o. Owner and group are the same as the current user unless the current user is superuser. If the user is supervisor, owner and group are the same as those resulting from the previous cpio -o. Note that if cpio -i tries to create a file that already exists and the existing file is the same age or younger (newer), cpio outputs a