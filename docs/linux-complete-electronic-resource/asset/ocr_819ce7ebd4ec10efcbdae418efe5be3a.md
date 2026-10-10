# 834 Appendix A

**conv=b[inary] / conv=t[ext] / conv=a[uto]**  The *fat* file system can perform CRLF<>NL (MS-DOS text format to UNIX text format) conversion in the kernel. The following conversion modes are available:

+   **binary**	no translation is performed. This is the default.

+   **text**	CRLF<>NL translation is performed on all files.

+   **auto**	CRLF<>NL translation is performed on all files that don't have a "well-known binary" extension. The list of known extensions can be found at the beginning of *fs/fat/misc.c* (as of 2.0, the list is: exe, com, bin, app, sys, drv, ovl, ovr, obj, lib, dli, dif, arc, zip, lha, lzh, 2oo, taz, z, arj, tz, taz, tzp, tpz, gz, tgz, deb, gif, bmp, tif, gif, jpg, pcx, tfm, vf, gif, pkl, pxi, dvi).

Programs that do computed lseeks won't like in-kernel text conversion. Several people have had their data ruined by this translation. Beware!

For file systems mounted in binary mode, a conversion tool (fromdos/todos) is available.

+   **debug**	Turn on the debug flag. A version string and a list of file system parameters will be printed (these data are also printed if the parameters appear to be inconsistent).

+   **fat=12 / fat=16**	Specify either a 12 bit fat or a 16 bit fat. This overrides the automatic FAT type detection routine. Use with caution!

+   **quiet**	Turn on the quiet flag. Attempts to chown or chmod files do not return errors, although they fail. Use with caution!

+   **sys_immutable, showexec, dots, nodots, dotsOK=[yes, no]**	Various misguided attempts to force Unix or DOS conventions onto a FAT file system.

# MOUNT OPTIONS FOR HPFS

+   **uid=value and gid=value**	Set the owner and group of all files. (Default: the uid and gid of the current process.)

+   **umask=value**	Set the umask (the bitmask of the permissions that are not present). The default is the umask of the current process. The value is given in octal.