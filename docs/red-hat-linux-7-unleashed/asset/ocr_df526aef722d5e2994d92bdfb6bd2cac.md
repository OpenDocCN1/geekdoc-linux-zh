# TABLE 28.3 continued

| Program Name | Function |
| --- | --- |
| mdeltree | Recursively deletes files and directories |
| mdir | Lists contents of a floppy |
| mformat | Formats a floppy |
| minfo | Categorizes, prints floppy characteristics |
| mkmmanifest | Restores Linux filenames from floppy |
| mlabel | Labels a floppy |
| mmdd | Creates subdirectory |
| mmount | Mounts a floppy |
| mmove | mv command for floppy files and directories |
| mpartition | Makes a DOS filesystem as a partition |
| mrd | Deletes directories |
| mren | Renames a file |
| mtooltest | Tests mtools package installation |
| mtype | Types (lists) a file |
| mzip | ZIP/JAZ drive utility |

The most often used will be the mformat, mdir, mcopy, and mdel commands. The mformat command formats nearly any type of floppy device. One of this software package's nice features is that you don't have to remember the specific names of floppy devices, such as /dev/fd0, and can use the (possibly) familiar A or B drive designators. This is possible because of mtool's use of the configuration file, /etc/mtools.conf.

Entries for different disk devices are listed in the file. You can edit the file (as root) to configure mtools for your system without having to rebuild the software. (If you need the source, however, you can readily find a copy on your favorite Linux site, or at ftp://ftp.tuX.org/pub/knalf/mtools, along with numerous add-ons and utilities.) If you examine the /etc/mtools.conf file, you'll see entries for different devices and configurations for other operating systems. For example, the floppy device entries look like this:

```
# Linux floppy drives
drive a: file="/dev/fd0" exclusive 1,44m mformat_only
drive b: file="/dev/fd1" exclusive 1,44m format_only
```

These entries allow you to easily format a floppy in drive A without mounting the disk:

```
# mformat a:
```