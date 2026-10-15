```
See /var/sadm/patch/118191-01/log for details

Patch packages installed:
SUNWgtar

root@unixhost> cd /
root@unixhost> find . -newer /tmp/timemark.ek -print > gtar118191.files
root@unixhost> more gtar118191.files

.
./var/sadm
./var/sadm/install
./var/sadm/install/logs
./var/sadm/install/contents
./var/sadm/install/.lockfile
./var/sadm/pkg
./var/sadm/pkg/SUNWgtar
./var/sadm/pkg/SUNWgtar/install
./var/sadm/pkg/SUNWgtar/save
./var/sadm/pkg/SUNWgtar/save/118191-01
./var/sadm/pkg/SUNWgtar/save/118191-01/undo.Z
./var/sadm/pkg/pkginfo
./var/sadm/patch
./var/sadm/patch/118191-01
./var/sadm/patch/118191-01/log
./usr/sfw/bin
./usr/sfw/bin/gtar
./usr/sfw/libexec
./usr/sfw/libexec/grmt
...
```

The example shows the installation of a patch on a Solaris system. Before applying the patch, the file /tmp/timemark.ek was created using the command touch. This file is used as a template for the find command, using the -newer option. This way all files newer than /tmp/timemark.ek are written to a list for later examination. This technique should work on almost every *NIX-based system. If you are using some kind of GUI or window manager like gnome, make sure to create the marker file just before applying the patch; otherwise, all files created by the GUI (temporary or others) will be recorded in the list as well.