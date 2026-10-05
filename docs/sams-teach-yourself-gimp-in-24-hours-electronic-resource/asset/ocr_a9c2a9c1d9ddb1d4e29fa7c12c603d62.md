# Installation and Configuration

simply need to follow the instructions carefully, read the READMEs, and be willing to do a little research if you run into trouble.

The source code on the CD-ROM is available in tar.gz format as well as in RPM format. The source RPMs allow you to compile the source code from scratch, and then build binary RPMs for installation (to keep things nice and tidy, and easy to upgrade/uninstall).

This section describes the basic steps needed to compile and install the GIMP from the source packages—it should be pretty uniform across platforms. However, if you run into trouble compiling GIMP on a non-Linux platform, you should consult the GIMP lists and newsgroups. There have been a few mild issues with different compilers on different platforms, although they are fairly simple to remedy.

# Installing and Compiling from the Source Packages

Installing and compiling the GIMP from the source distribution should work roughly the same in all UNIX-like platforms. To compile the sources, you must do the following as the root user:

+   Compile and install GTK:
cp /mnt/cdrom/gtk/src/gtk-1.0.7.tar.gz /usr/local/src
(or snag it from ftp://ftp.gimp.org/pub/gtk/)
tar -xvf gtk-1.0.7.tar.gz
cd ./gtk-1.0.7
Read the Readme file: vi README.
(Substitute pico, emacs, or whatever text editor you use for vi if necessary.)
./configure
make
make install
Make sure all the appropriate graphics libraries are installed (Updates can be found in /mnt/cdrom/gimp/libs/src. Unpack the them and read the appropriate README files).\nCopy the source package of GIMP from the CD-ROM to a suitable compiling spot:
cp /mnt/cdrom/gimp/src/gimp-1.0.2.tar.gz /usr/local/src
Alternatively, you can grab the latest version of the GIMP
ftp://ftp.gimp.org/pub/gimp/
Decompress the source package.
tar -xvf gimp-1.0.2.tar.gz
cd ./gimp-1.0.2