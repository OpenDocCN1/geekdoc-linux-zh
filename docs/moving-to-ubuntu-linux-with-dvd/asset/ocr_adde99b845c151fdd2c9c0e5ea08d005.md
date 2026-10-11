If something in that list should prove interesting and you would like to know more about the package, try the `--print-avail` flag. In this example, I try to discover something about the mysterious mtools package:

```
dpkg --print-avail mtools
Package: mtools
Priority: standard
Section: otherosfs
Installed-Size: 468
Maintainer: Luis Bustamante <luberbu@fluidsignal.com>
Architecture: i386
Version: 3.9.9-2.1ubuntu1
Depends: libc6 (>= 2.3.2.ds1-4)
Suggests: floppyy
Size: 195994
Description: Tools for manipulating MSDOS files
```

The preceding information only prints information about an installed package. As with many things in the Linux world (and life in general), there is more than one way to do this. You could also use the other indispensable command-line tool, apt-get—to be specific, apt-cache, one of apt-get’s related utilities:

```
apt-cache show mtools
```

The results of this command are identical to those of the preceding dpkg example.

# Finding out a Package’s Current Release Level

To find out the version of a package that is already installed on your system, use the -l flag. In the following example, I query the system to find out what version of bash (the Bourne Again Shell) I am working with:

```
dpkg -l bash
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Installed/Config-files/Unpacked/Failed-config/
| Half-installed
| Err?=none/Hold/Reinst-required/X=both-problems
(Status,Err: uppercase=bad)
```