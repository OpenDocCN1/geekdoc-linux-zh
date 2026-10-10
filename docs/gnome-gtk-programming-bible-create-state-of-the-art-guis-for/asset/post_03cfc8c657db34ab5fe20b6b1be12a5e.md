
They each supply a method for guaranteeing that an application closes down cleanly.

This chapter is the conclusion of the third, and final, part of the book. The following appendices serve two purposes. Appendices A and B explain where and how to load and install the software. Appendices C through G are some cross-reference listings that can be quite handy when programming GNOME.

## What’s on the CD-ROM

This appendix describes the contents of the CD-ROM accompanying this book. This is a complete set of the libraries and utilities you will need to create GNOME applications. Also, all the examples from the book are included.

> **Note**
>
> This is all open software so it is being continuously updated. There are later versions of the software than those on the CD-ROM. However, if you are relatively new to GNOME and GTK+, it will be simpler and safer to use the software on the CD-ROM. As software moves from one version to another, incompatibilities pop up here and there, but the CD-ROM versions all work together.

If you prefer to get the latest versions of everything, the URLs are listed in Appendix B. Also, if you use the software supplied on the CD-ROM, Appendix B supplies the information you will want if you decide to upgrade your installation to a later version.

### CD Contents

The files on the CD-ROM are divided into the three directories listed in Table A-1.

| Directory | Contains |
| --- | --- |
| examples | The source code of the examples in the book. Each chapter has its own subdirectory. |
| gnome/base | The source code of the base GNOME/GTK+ development libraries. |
| gnome/core | The source code of the core GNOME/GTK+ development libraries. |
| tools | This contains the compiler, autoconf, and automake. |

### Examples

The examples from the book—located in the examples directory on the CD-ROM—are organized according to the chapter in which they appear in the book. There are no executables included because different Linux platforms require different formats for binary executables. Each directory can be copied to a hard drive and compiled. Also, if you want to compile them all, simply copy the entire tree to your hard drive and use the Makefile in the root directory.

> There is a Web site for the book, and the example code is available there also. If you find something wrong, or something that should be changed, in one of the examples, please check this Web site for updates:
>
> http://www.belugalake.com/book/gnomebible

### GNOME

The files in the gnome and tools directories are of the type often referred to as tarballs. These are tar files that have been compressed with the gzip utility. They all contain the source and Makefiles that can be used to compile and install the files on your system. You can install the GNOME files anywhere you would like. My personal preference is to create a directory in /usr/local like this:

```bash
mkdir /usr/local/gnome
```

Next, make the new directory your current directory:

```bash
cd /usr/local/gnome
```

Then, assuming your CD-ROM drive is `/mnt/cdrom`, each of the files can be installed in its own subdirectory. For example, to install the GTK+ library, enter this command:

```bash
tar -xzvf /mnt/cdrom/gnome/base/gtk+-1.2.6.tar.gz
```

The `tar` command will (x) extract the files and store them in a local directory named `gtk+-1.2.6`. The (v) verbose option specifies that every file and directory name should be displayed. The file will first be (z) gunzipped and then untarred. The (f) input file is the one named on the command line.

There are three steps to compiling and installing each of the packages. The first step is to establish the configuration for your system. This is mostly automatic because there is a shell script that detects the necessary information and creates the makefiles. Once the makefiles are created, you will still need to compile and install the software. This is done with these three commands:

```bash
configure
make
make install
```

The first command creates the makefiles, the second compiles the source into object code, and the third stores binary files in the appropriate locations.

> You will be better off if you get to know the process. There are README and INSTALL files in each of the source directory, and you should read them. This is especially true if you have some sort of special Linux installation. After you have read through two or three of these, the process should become clear.

### Tools

The tools supplied on the CD-ROM are also tarballs including the source code. They install in much the same way as the GNOME software, but you will probably want to pay more attention to the README and INSTALL files. In particular, `gcc` has a number of options that allow you to configure it for your preferences.

## Setting Up for Software Development

There are a number of software components you need to install before you can write a GNOME/GTK+ application. If you have a relatively recent Linux CD, you certainly have a lot of what you need—and you may have it all. The following checklist helps you to make sure you have it all.

> **Note**
> Like everything else in the world of open source, things are subject to change. The names and URLs listed here may change. Also, a newer version of something may operate differently and have slightly different requirements than those outlined here.

### Linux

If you do not have Linux, you probably will purchase a CD. A commercial CD has the advantages of containing most of the items you need, being easier to install than a downloaded version, and providing telephone support to get you started.

If, however, you want to get a copy over the Internet, then you should be careful which version you choose. Mainly, you don't want to get an experimental version. A Linux version number indicates whether it is a stable or developmental version. Unless you are working on the Linux kernel itself, use a stable version. If the second digit following the version number is even (2.0, 2.2, and so on), it is a stable version. There may be a third number in the version number (like 2.2.8) that indicates bug fixes. To get the latest version of the kernel, get the highest even-numbered version.

The following are some of the more popular Linux distributions:

- Caldera http://www.caldera.com
- Corel http://linux.corel.com
- Debian http://www.debian.org/
- LinuxPro http://www.wgs.com
- Red Hat http://www.redhat.com
- Slackware http://www.slackware.com
- StormLinux http://stormlinux.com
- SuSE http://www.suse.com
- TurboLinux http://www.turbolinux.com

While any one of these can run GNOME successfully and can be used as a GNOME development platform, Red Hat Linux seems the most committed to a GNOME environment.

### gcc (egcs)

This is the C compiler that you need to compile your programs. In April of 1999, because of future plans, the Free Software Foundation appointed the *egcs Steering Committee* to maintain gcc. At that time, the name was changed from gcc to egcs. But the executable of the program is still named gcc because it has to work with all the existing make files.

There certainly will be a version of the gcc compiler included in your Linux distribution. But new features are added from time to time, so you need to make sure you have a version that is as current as your GNOME software. You can get the latest version from any number of locations on the Internet. The home page is:

http://www.gnu.ai.mit.edu/software/gcc/gcc.html

### XFree86

This is the low-level windowing software used by GTK+ and GDK. All Linux distributions include this software, and install it during normal installation. This is very stable software, but there are occasional releases (as of this writing, the latest version is X11R6.4). If you find that you need to get a new version (or need to find out more information about it), the XFree86 home page is:

http://www.xfree86.org
