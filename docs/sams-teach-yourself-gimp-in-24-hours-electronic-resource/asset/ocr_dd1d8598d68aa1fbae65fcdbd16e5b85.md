# Installation and Configuration

```
rpm -bb gimp-1.0.2-1.spec
rpm -bb gimp-data-extras-1.0.2-1.spec
rpm -bb gimp-plugins-unstable.spec
```

This compiles the source and packages the binaries into tidy RPM packages for you. For forearmed: the GIMP consists of over 300,000 lines of code, so expect this compilation to take a while, depending on your machine. After it finishes, you can then install these RPMs just like you would any other.

```
cd /usr/src/redhat/RPMS
rpm -Uvh gimp-1.0.2.i386.rpm
rpm -Uvh gimp-devel-1.0.2.i386.rpm
rpm -Uvh gimp-data-extras-1.0.2.i386.rpm
rpm -Uvh gimp-plugins-unstable.-1.0.2.i386.rpm
```

# Source Installation Troubleshooter

+   Q keep getting errors about not finding libgtk.
A First of all, make sure you have GTK installed! Then, make sure it is in your search path. Add the line /usr/local/lib to /etc/ld.so.conf with your favorite text editor, and then run ldconfig.
Q keep getting glibconfig.h - not found errors.
A Make sure that the header files glib.h and glibconfig.h are in their proper places. On systems, glibconfig.h should go in /usr/(local)/lib/glib/include, and glib.h in /usr/(local)/include/
GIMP won't compile correctly on Solaris, HP-UX, and so on.
A Every platform has its own quirks. For non-Linux platform specific issues, it is best to consult newsgroups and Web sites for answers. The GIMP Developer’s FAQ—http://www.rru.com/-meo/gimp/faq-dev.html—has a lot of really good, solid answers for these kind of issues.

# Summary

Hopefully, installation has proceeded smoothly and without incident. Again, if you do run into snags, there are a lot of people out there willing and able to help. If this is the case, you will likely find that the answers are frequently quite simple. Fortunately, GIMP is, for the most part, well behaved for installation.