![](bbox=[0.13, 0.12, 0.24, 0.22])

Usually, you don't have to do anything but type the commands to build the
software, but you must install the software-development tools on your
system. In Fedora Core, you must install the Development Tools and the
GNOME Software Development packages. In Debian, to build and run XMMS,
you must also install the X Software Development package because it's an X
application.

After you've installed XMMS, try running it from the GNOME or KDE desktop
by typing **xmms** in a terminal window. From the XMMS window, press L to get
the Load File dialog box. Select an MP3 file to play. Your PC must have a sound
card, and the sound card must be configured correctly for XMMS to work.

To summarize, here's an overview of the steps you follow to download,
unpack, build, and install a typical software package:

+   1.  Use a Web browser to download the source code, usually in the form
+       of a .tar.gz file, from the anonymous FTP site or Web site.

+   2.  Unpack the file with a `tar zxvf filename` command. (If the com-pressed tar file has a .bz2 extension, that means the file is compressed
+       with bzip2 and you can unpack that file with a `tar jxvf filename`
+       command.)

+   3.  Change the directory to the new subdirectory where the software is
+       unpacked, with a command such as `cd software_dir`.

+   4.  Read any README or INSTALL files to get a handle on any specific
+       instructions you must follow to build and install the software.

+   5.  The details of building the software may differ slightly from one soft-ware package to another, but typically you type the following com-mands to build and install the software:

```
./configure
make
make install
```

+   6.  Read any other documentation that comes with the software to find
+       out how to use the software and whether you must configure the soft-ware further before using it.

# ## Installing SRPMs

![](bbox=[0.12, 0.82, 0.24, 0.95])

If you have the source CDs for Fedora Core (you can download the source
CD images from one of the sites listed at `http://fedora.redhat.com/download/mirrors.html`), you can install the source files and build vari-ous applications directly from the source files. Fedora Core source-code
RPM files are generally known as SRPMs (short for source RPMs).