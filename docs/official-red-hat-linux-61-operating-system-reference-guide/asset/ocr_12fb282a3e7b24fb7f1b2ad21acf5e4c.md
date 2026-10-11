route, shutdown, swapoff, swapon, update

# The /usr Directory

The /usr directory is for files that can be shared across a whole site. The /usr directory usually has its own partition, and it should be mountable read-only. The following directories should be subdirectories of /usr:

```
/usr
├─ X11R6
├─ bin
├─ dict
├─ doc
├─ etc
├─ games
├─ include
├─ info
├─ lib
├─ libexec
├─ local
├─ man
├─ sbin
├─ share
└─ src
```

The X11R6 directory is for the X Window System (XFree86 on Red Hat Linux), bin is for executables, doc is for random, non-man-page documentation, etc is for site-wide configuration files, include is for C header files, info is for GNU info files, lib is for libraries, man is for man pages, sbin is for system administration binar ies (those that do not belong in /sbin), and src is for source code.

# The /usr/local Directory

The FHS says:

> "The /usr/local hierarchy is for use by the system administrator when installing software locally. It needs to be safe from being overwritten when the system software is updated. It may be used for programs and data that are shareable amongst a group of machines, but not found in /usr."