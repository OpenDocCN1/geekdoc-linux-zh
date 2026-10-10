/opt  Optional (usually large) software packages on Caldera OpenLinux, Netscape, WordPerfect, StarOffice, and KDE are put into /opt.

/dev  This directory contains special device files. These are not real files but rather special entries in the file system that correspond to device drivers for actual hardware.

# Note

Device files are covered in Chapter 8.

/usr  This is a large hierarchy all to itself. Most of your Linux system files live in this directory.

/usr/bin  Most executable files live here.

/usr/sbin  Additional system-administrator programs stay in this directory.

/usr/lib  This directory contains more shared libraries. In addition, many programs put private information or executables here.

# Note

Why mirror /bin, /lib, and /sbin under /usr? Traditionally, UNIX systems used a rather small disk partition as the root partition and mounted a larger partition under /usr. There seems to be a law that large things fail more often than small things, so having a small root partition increases the chances of having a salvageable system in the event of a disk crash. The root partition should contain just enough software to get the system up and running and check or repair the /usr partition.

/usr/X11R6  This rather large directory tree contains everything related to the X Window System.

/usr/dict  This directory contains /usr/dict/words, a list of English words used by spell-checking programs.

/usr/man  Most system manual pages (see the “UNIX Manual Pages: man section”) live here.

/usr/src  Source code can be found in this directory. In particular, /usr/src/linux contains the source code for the Linux kernel.

/usr/share  Similar to /usr/lib, this directory is meant as a repository for architecture-independent information. Thus, even though /usr/lib will often contain