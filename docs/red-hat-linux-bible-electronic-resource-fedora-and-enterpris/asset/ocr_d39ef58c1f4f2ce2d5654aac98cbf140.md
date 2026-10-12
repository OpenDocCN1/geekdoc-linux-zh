| Key | Value |
|---|---|
| Version | : 2.8 | Vendor: | Red Hat, Inc. |
| Release | : 5 | Build Date: | Tue 18 Feb 2003 11:08:21 PM PST |
| Install Date: | Sat 09 Aug 2003 02:15:35 PM PST |  |  |
| Build Host | : daffy.perf.redhat.com |  |  |
| Group | : Applications/System Source | RPM: | dosfstools-2.8-6.src.rpm |
| Size | : 73278 | License: | GPL |
| Signature | : (none) |  |  |
| Packager | : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla> |  |  |
| Summary | : Utilities for making and checking MS-DOS FAT filessystems on Linux. |  |  |
| Description |  |  |  |
|  | The dosfstools package includes the mkdosfs and dosfsck utilities, which respectively make and check MS-DOS FAT filesystems on hard drives or on floppies. |  |  |

To find out about a package's contents, you can use the -l (list) option with your query. The following example shows the complete path names of files contained in the xpiolot package:

```
# rpm -ql dosfstools | more
/sbin/dosfsck
/sbin/fsck.msdos
/sbin/fsck.vfat
/sbin/mkdosfs
/sbin/mkfs.msdos
/sbin/mkfs.vfat
/usr/share/man/man8/dosfsck.8.gz
```

Would you like to know how to use the components in a package? Using the -d option with a query will display the documentation (man pages, README files, HOWTOs, and so on) that is included with the package. If you are having trouble getting your X Window System running properly, you can use the following command line to find documents that may help:

```
# rpm -qd XFree86 | more
/usr/X11R6/man/man1/XFree86.1x.gz
/usr/X11R6/man/man1/Xmark.1x.gz
/usr/X11R6/man/man1/Xserver.1x.gz
/usr/X11R6/man/man1/appres.1x.gz
/usr/X11R6/man/man1/atobm.1x.gz
/usr/X11R6/man/man1/bdfptofc.f.1x.gz
```

Many packages have configuration files associated with them. To see what configuration files are associated with a particular package, use the -c option with a query. For example, this is what you would type to find configuration files that are used with the ppp package: