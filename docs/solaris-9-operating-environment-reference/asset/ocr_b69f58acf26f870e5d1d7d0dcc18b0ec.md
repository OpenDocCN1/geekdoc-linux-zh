# pkgparam 1057

```
TZ='Australia/West'
PATH='/sbin:/usr/sbin:/usr/bin:/usr/sadm/sadm/install/bin'
OMBASE='/usr/sadm/sysadm'
ARCH='sparc'
PKG=SUNWthj
NAME='HotJava Browser for Solaris'
VERSION='1.0.1,REV=1998.02.03'
PRONAME='HotJava'
PRODVERS='1.0.1'
SUNW_PKGTYPE='usr'
MAXINST=1000
CATEGORY='system'
DESC='HotJava Browser for Solaris'
VENDOR='Sun Microsystems, Inc.'
HOTJAVA='Please contact your local service provider'
EMAIL=''
HOTJAVA='dt/appconfig/hotjava'
PSTAMP='pavoni980201313227'
PKGINST='SUNWthj'
PKGSAV='/var/sadm/pkg/SUNWthj/save'
INSTDATE='Feb 15 1999 09:33'
castle
```

If you specify no parameters on the command line, values for all parameters associated with the package are shown.

# Options

+   -d device Specify the device on which a pkginst is stored. device can be a directory path name or identifiers for tape, diskette, or removable disk (for example., /var/tmp, /dev/diskette, and /dev/disk/cld0s0). You can use the special spool to represent the default installation spool directory (/var/sp/pkg/).

+   -f filename Read filename for parameter values. filename should be in the same format as a pkginfo(4) file. For example, you might create such a file during package development and use it for testing.

+   -R root-path Define the full path name of a subdirectory to use as the root-path. Relocate all files, including package system information files, to a directory tree starting in the specified root-path.

+   -v Display the name of paramand and its value.

# Operands

+   pkginst Define a specific package instance for which to display parameter values.

+   param Define a specific parameter whose value should be displayed.