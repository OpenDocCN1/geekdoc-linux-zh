
# 834 Appendix A

## MOUNT OPTIONS FOR FAT

**conv=b[inary] / conv=t[ext] / conv=a[uto]** The *fat* file system can perform CRLF<>NL (MS-DOS text format to UNIX text format) conversion in the kernel. The following conversion modes are available:

- **binary**: no translation is performed. This is the default.
- **text**: CRLF<>NL translation is performed on all files.
- **auto**: CRLF<>NL translation is performed on all files that don't have a "well-known binary" extension. The list of known extensions can be found at the beginning of *fs/fat/misc.c* (as of 2.0, the list is: exe, com, bin, app, sys, drv, ovl, ovr, obj, lib, dli, dif, arc, zip, lha, lzh, 2oo, taz, z, arj, tz, taz, tzp, tpz, gz, tgz, deb, gif, bmp, tif, gif, jpg, pcx, tfm, vf, gif, pkl, pxi, dvi).

Programs that do computed lseeks won't like in-kernel text conversion. Several people have had their data ruined by this translation. Beware!

For file systems mounted in binary mode, a conversion tool (fromdos/todos) is available.

- **debug**: Turn on the debug flag. A version string and a list of file system parameters will be printed (these data are also printed if the parameters appear to be inconsistent).
- **fat=12 / fat=16**: Specify either a 12 bit fat or a 16 bit fat. This overrides the automatic FAT type detection routine. Use with caution!
- **quiet**: Turn on the quiet flag. Attempts to chown or chmod files do not return errors, although they fail. Use with caution!
- **sys_immutable, showexec, dots, nodots, dotsOK=[yes, no]**: Various misguided attempts to force Unix or DOS conventions onto a FAT file system.

## MOUNT OPTIONS FOR HPFS

- **uid=value and gid=value**: Set the owner and group of all files. (Default: the uid and gid of the current process.)
- **umask=value**: Set the umask (the bitmask of the permissions that are not present). The default is the umask of the current process. The value is given in octal.
- **case=lower / case=asis**: Convert all file names to lowercase, or leave them. (Default: case=lower.)
- **conv=binary / conv=text / conv=auto**: For conv=text, delete some random CRs (in particular, all followed by NL) when reading a file. For conv=auto, choose more or less at randomly between conv=binary and conv=text. For conv=binary, just read what is in the file. This is the default.
- **nocheck**: Do not abort mounting when certain consistency checks fail.

## MOUNT OPTIONS FOR ISO9660

Normal iso9660 filenames appear in a 8.3 format (i.e., DOS-like restrictions on filename length), and in addition all characters are in uppercase. Also there is no field for file ownership, protection, number of links, provision for block/character devices, etc.

Rock Ridge is an extension to iso9660 that provides all of these Unix-like features. Basically there are extensions to each directory record that supply all of the additional information, and when Rock Ridge is in use, the filesystem is indistinguishable from a normal Unix file system (except that it is read-only, of course).

- **norock**: Disable the use of RockRidge extensions, even if available. Cf. map.
- **check=r[elaxed] / check=s[trict]**: With check=relaxed, a filename is first converted to lowercase before doing the lookup. This is probably only meaningful together with norock and map=normal. (Default: check=strict.)
- **uid=value and gid=value**: Give all files in the file system the indicated user or group id, possibly overriding the information found in the Rock Ridge extensions. (Default: uid=0, gid=0.)
- **map=n[ormal] / map=o[ff]**: For non-Rock Ridge volumes, normal name translation maps upper- to lowercase ASCII, drops a trailing ";1", and converts ";" to ".". With map=off no name translation is done. See norock. (Default: map=normal.)
- **mode=value**: For non-Rock Ridge volumes, give all files the indicated mode. (Default: read permission for everybody.) Since Linux 2.1.37 one no longer needs to specify the mode in decimal. (Octal is indicated by a leading 0.)
- **unhide**: Also show hidden and associated files.
- **block=[512|1024|2048]**: Set the block size to the indicated value. (Default: block=1024.)
- **conv=[auto|b|binary|m|text|t|txt]**: (Default: conv=binary.) Since Linux 1.3.54 this option has no effect. (And non-binary settings used to be very dangerous, often leading to silent data corruption.)
- **cruft**: If the high byte of the file length contains other garbage, set this mount option to ignore the high order bits of the file length. This implies that a file cannot be larger than 16Mb. The cruft option is set automatically if the entire CDROM has a weird size (negative, or more than 800MB). It is also set when volume sequence numbers other than 0 or 1 are seen.

## MOUNT OPTIONS FOR MINIX

None.

## MOUNT OPTIONS FOR MS-DOS

See mount options for FAT. If the msdos file system detects an inconsistency, it reports an error and sets the file system read-only. The file system can be made writeable again by remounting it.

## MOUNT OPTIONS FOR NCP

Just like nfs, the ncp implementation expects a binary argument (a struct ncp_mount_data) to the mount system call. This argument is constructed by ncpmount(8) and the current version of mount (2.6) does not know anything about ncp.

## MOUNT OPTIONS FOR NFS

Instead of a textual option string, parsed by the kernel, the nfs filesystem expects a binary argument of type struct nfs_mount_data. The program mount itself parses the following options of the form ‘tag=value’, and puts them in the structure mentioned: size=n, wsize=n, timeo=n, retrans=n, acregmin=n, acregmax=n, acdirmin=n, acdirmax=n, actimeo=n, retry=n, port=n, mountport=n, mounthost=name, mountprog=n, mountvers=n, nfsprog=n, nfsvers=n, namlen=n. The option add=n is accepted but ignored. Also the following Boolean options, possibly preceded by no are recognized: bg, fg, soft, hard, intr, posix, cto, ac, tcp, udp, lock. For details, see nfs(5).

Especially useful options include:

- **rsize=8192, wsize=8192**: This will make your nfs connection much faster than with the default buffer size of 1024.
- **hard**: The program accessing a file on a NFS mounted file system will hang when the server crashes. The process cannot be interrupted or killed unless you also specify intr. When the NFS server is back online the program will continue undisturbed from where it was. This is probably what you want.
- **soft**: This option allows the kernel to time out if the nfs server is not responding for some time. The time can be specified with timeo=time. This option might be useful if your nfs server sometimes doesn't respond or will be rebooted while some process tries to get a file from the server. Usually it just causes lots of trouble.
- **nolock**: Do not use locking. Do not start locked.

## MOUNT OPTIONS FOR PROC

**uid=value and gid=value**: These options are recognized, but have no effect as far as I can see.

## MOUNT OPTIONS FOR ROMFS

None.

## MOUNT OPTIONS FOR SMBFS

Just like nfs, the smb implementation expects a binary argument (a struct smb_mounter_data) to the mount system call. This argument is constructed by smbmount(8) and the current version of mount (2.6c) does not know anything about smb.

## MOUNT OPTIONS FOR SYSV

None.

## MOUNT OPTIONS FOR UFS

None.

## MOUNT OPTIONS FOR UMSDOS

See mount options for ms-dos. The **dotsOK** option is explicitly killed by umsdos.

## MOUNT OPTIONS FOR VFAT

First of all, the mount options for *fat* are recognized. The **dotsOK** option is explicitly killed by *vfat*. Furthermore, there are:

- **uni_xlate**: Translate unhandled Unicode characters to special escaped sequences. This lets you backup and restore filenames that are created with any Unicode characters. Without this option, a `?` is used when no translation is possible. The escape character is `':'` because it is otherwise illegal on the vfat filesystem. The escape sequence that gets used, where *u* is the unicode character, is: `':'`, (u & 0x3f), ((u>>6) & 0x3f), (u>>12).
- **posix**: Allow two files with names that only differ in case.
- **nonumtail**: First try to make a short name without sequence number, before trying *name*`~`*num.ext*.

## MOUNT OPTIONS FOR XENIX

None.

## MOUNT OPTIONS FOR XIAFS

None. Although nothing is wrong with xiafs, it is not used much, and is not maintained. Probably one shouldn't use it. Since Linux version 2.1.21 xiafs is no longer part of the kernel source.

## THE LOOP DEVICE

One further possible type is a mount via the loop device. For example, the command

```
mount /tmp/fdimage /mnt -t msdos -o loop=/dev/loop3,blocksize=1024
```

will set up the loop device */dev/loop3* to correspond to the file */tmp/fdimage*, and then mount this device on */mnt*. This type of mount knows about three options, namely **loop**, **offset** and **encryption**, that are really options to *losetup*(8). If no explicit loop device is mentioned (but just an option `-o loop` is given), then *mount* will try to find some unused loop device and use that.
