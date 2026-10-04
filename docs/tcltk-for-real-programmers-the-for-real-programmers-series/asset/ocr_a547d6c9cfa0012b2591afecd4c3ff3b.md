# Appendix B. Installing Tcl/Tk Distributions

```
ftp> ...
ftp> get tcl.install.tar
ftp> quit
foo tar -xvf tcl.install.tar
```

# B.3.3 Installing Pre-Compiled Binaries for BSD/OS and Linux

The pre-compiled binaries and libraries files for BSD/OS and Linux are in the bsd_bin and lin_bin directories on the CD-ROM. These have been compiled with /usr/local as the root directory following the technique described in Section B.3.2.

The tar archive is generated from the root directory. These binaries can be unpacked into /usr/local with gunzip and tar pax, and used with no further modifications.

If you need to install these under some other directory tree (for instance, /usr/contrib/), you'll need to set the TCL_LIBRARY and TK_LIBRARY environment variables to point to the installation directories in order for the interpreters to find their initialization files.

The files in these directories are:

+   - tcl76ful.tgz Complete Tcl 7.6 installation.
- tcl76min.tgz Tcl 7.6 installation with no man pages.
- tk42ful.tgz Complete Tk 4.2 installation.
- tk42min.tgz Tk 4.2 installation with no man pages.
- tcl180ful.tgz Complete Tcl 8.0 installation.
- tcl180min.tgz Tcl 8.0 installation with no man pages.
- tk80ful.tgz Complete Tk 8.0 installation.
- tk80min.tgz Tk 8.0 installation with no man pages.
- tcl181ful.tgz Complete Tcl 8.1 installation.
- tcl181min.tgz Tcl 8.1 installation with no man pages.