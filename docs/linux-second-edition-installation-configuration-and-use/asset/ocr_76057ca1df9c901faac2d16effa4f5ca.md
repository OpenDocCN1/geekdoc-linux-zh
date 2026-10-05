# Leafnode

This is a small news server which is particularly suited for private news archives that can be read via modem in offline mode. The following command is used for installation:

```
# rpm -i /cdrom/contrib/leafnode-1.9.2-1.1386.rpm
```

# LyX

LyX is a WYSIWYG interface for LaTeX. The xforms package provides a library that LyX is built on.

```
# rpm -i /cdrom/contrib/xforms-0.88-2.i1386.rpm
# rpm -i /cdrom/contrib/lyx-1.0.1-2.i1386.rpm
```

# KLyX

KLyX is the KDE version of LyX. Installation is somewhat complicated:

```
# cp /cdrom/contrib/libstdc++-0.2.9 /usr/lib
# ldconfig
# rpm -i --nodeps /cdrom/contrib/klyx-0.9.9-1.i686.rpm
# cp -rs /opt/kde/bin/* /usr/bin/
# cp -rs /opt/kde/share/* /usr/share/
```

Some remarks about the above: KLyX:9.9 presumes the library libstdc++-2.9.0. Although RedHat 6.0 supplies the libstdc++-2.9 package, this package provides only version 2.8 of the required library (you can easily verify this by means of rpm -q --provides libstdc++. It is unlikely that confusion of versions was intentional).

To install the required libstdc++ without using the RPM package management, the missing file is simply copied into the /usr/lib directory. ldconfig makes that this library is found.

The --nodeps in the following rpm command forces the installation of klyx although libstdc++-2.9 is still unknown in the RMP database.
The next problem is that under RedHat 6.0 all KDE files are found in the /usr/share directory. The KLyXPackage, however, is installed into /opt/kde/share instead. (This directory is the default directory which was taken over by many distributions but not by RedHat). To make KLyX find required files, appropriate links are created by means of the two cp -ls commands.

> The KLyX package on CD-ROM 2 is optimized for i686 processors (Pentium Pro, Pentium II, and compatible processors). Installation and execution on older processors is not possible.
An i386 binary which would run on all i386-compatible processors (although not as fast as the more advanced models) was unfortunately unavailable in RedHat's contrib directory. By the time you have this book, KLyX 1.0 will probably be completed - then, at the latest, you should find an appropriate i386 package in contrib directory. Maybe RedHat will even decide to incorporate the program into the 6.0 Powertools, which were also unavailable at the time of writing.