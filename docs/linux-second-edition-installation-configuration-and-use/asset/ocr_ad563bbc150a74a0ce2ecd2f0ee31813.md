# The updates directory

If after completion of a new distribution problems or gaps appear in individual packages, RedHat usually makes corrected packages available on its FTP server after a short time. The updates directory contains all the updates available by end of May, 1999. Information on the errors corrected by these updates can be found in the file updates/README.

To replace an already installed package with a more recent version, you use rpm with the --upgrade option. However, this does not work straight away. Thus, for example, installation of Netscape Communicator 4.6 packages the package netscape-common-4.6. This package can, however, not be updated because this would violate the package dependencies with the still previous Netscape version. The update function only when you update both packages with one single command.

```
# --upgrade netscape-communicator-4.6-1.i386.rpm
error: failed dependencies:
netscape-common = 4.6 is needed by netscape-communicator-4.6-1
# --upgrade netscape-common-4.6-1.i386.rpm
error: failed dependencies:
netscape-common = 4.5 is needed by netscape-communicator-4.5-3
# --upgrade netscape-common-4.6-1.i386.rpm \\
netscape-communicator-4.6-1.i386.rpm
```

# NFS

For the first time, RedHat 6.0 uses knfsd package as an NFS server which resorts directly to the new: NFS functions in kernel 2.2. Although the brief info promises better performance, this is obtained at the cost of considerable compatibility problems which particular occur with computers running a different operating system. By the end of May 1999, no updates were available which would diminish these problems. However, by the time you hold in your hands you will probably find an improved version on RedHat's web server.

http://www.redhat.com/corp/support/errata/rh60-errata-general.html

# KDE

Unfortunately, the final version 1.1.1 is not supplied with RedHat 6.0, the beta version 1.1.Ipre2. In Linux Weekly and some newsgroups there have been reports about stability problems with this KDE version. At the time of pressing the CD, no update was available. (By the way, the author has not experienced any difficulties during operation of KDE.)

# The contrib directory

The contrib directory contains some packages which officially do not belong to RedHat 6.0 but are treated in this book: leafnode, LyX and xemacs, and xv. These package come from the contrib directory of the RedHat FTP server.