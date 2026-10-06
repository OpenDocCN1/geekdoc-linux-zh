
## Part II: Using Fedora RHEL

| Format | Extension | Description |
|---|---|---|
| tar and gzip file | .tgz | A common practice for naming files that are tar archives that were compressed with gzip is to use the .tgz extension. |
| bzip2 | .bz2 | File was compressed with the bzip2 program. |
| Tar/compressed | .tar .xz | File archived with tar and compressed with the UNIX compress command. |
| Linux Software Map | .lsm | File contains the content of an archive. |
| Debian Binary Package | .deb | File is a binary package used by the Debian distribution. (See descriptions of how to convert Debian to Red Hat formats later in this chapter.) |
| RPM Package Management | .rpm | File is a binary package used by Fedora. Format also available to other Linux distributions. |

## Table 5-2: Linux Document Formats

| Format | Extension | Description |
|---|---|---|
| Hypertext Markup Language | .html .htm | File is in hypertex format for reading by a Web browser program (such as Mozilla). |
| PostScript | .ps | File is in PostScript format for outputting on a PostScript printer. |
| SGML | .sgml | File is in SGML, a standard document format. SGML is often used to produce documents that can be later converted to a variety of formats. |
| DVI | .dvi | File is in DVI, the output format of the LaTeX processing tools. Convert these files to PostScript or Hewlett-Packard's PCL using the dvips and dvjij commands. |
| Plain text | | Files in Fedora without a suffix are sometimes plaintext files (in ASCII format). (A note of caution: All the commands in Linux, as those in /usr/bin and /usr/sbin, have no extension. If you have a file with no extension on it, it's best to use the file command before proceeding with any operation. In fact, using file on a previously untested file can prevent problems. A .txt file full of malicious things to the system.) |

## Chapter 5: Accessing and Running Applications

If you are not sure what format a file is, use the file command as follows:

```
$ file filename
```

This command tells you if it is a GNU tar file, RPM, gzip, or other file format. (This is a good technique if a file was renamed and lost its extension).

If you would like to convert a software package from one of the formats described above, you can use the alien (http://freshmeat.net/projects/alien). Although alien is not considered stable enough to use with system packages, it can be a good tool for trying out some software packages on your Fedora system.

## Building and installing from source code

If no binary version of the package you want is available, or if you just want to tailor a package to your needs, you can always install the package from source code. To begin, you get the source code (SRPM) version of any packages from the Fedora software repository (Appendix A for details). You can modify the source code and rebuild to suit your needs.

Software packages that are not available in RPM format are typically available in the form of a tarball (a bunch of files grouped together a single file formatted by the tar utility) that has been compressed (typically by the gzip utility). Although the exact instructions for installing an application from a source code archive vary, many packages that are in the .bz2, .tar.bz2, .tgz, .gz and .tar formats follow the basic procedure.

> TIP: Before you install from source, you will need to install a variety of software development packages. If you have the disk space, I recommend that you install all software development packages that are recommended during Fedora installation.

The following is a minimal list of C-programming software development tools:

- gcc — Contains the gcc (GNU C compiler) compiler.
- make — Contains the make command for building the binaries from Makefiles.
- glibc — Contains important shared libraries, the C library, and the standard math library.
- glibc-devel — Contains standard header files to create executables.
- kernel-devel — Contains the Linux kernel source code and is needed to rebuild the kernel.
- rpm-build — Contains the rpmbuild utility for building the RPM package from source code.
- libc — Libraries needed for programs that were based on libc 5, older applications can run on glibc (libc 6) systems. If you use C++, there are many of packages to get, especially libstdc++ and libstdc++-devel.

## Installing software in SRPM format

To install a source package from the Fedora source directory, do the following:

1. Refer to Appendix A for information on obtaining Fedora source code.
2. Download the package you want to the current directory.
3. Install the source code package using the following command:

```
# rpm -iv packagename*.rpm
```

(Replace packagename with the name of the package you are installing.) Starting with Fedora 10, the source is installed by default in a directory called (/usr/src/rpmsbuild/SOURCES) in your home directory. Spec files are copied to rpmbuild/SPECS. Prior to Fedora 10, the default was /usr/src/redhat/SOURCES and /usr/src/redhat/SPECS.

4. Change to the SPECS directory as follows:

```
# cd ~/rpmbuild/SPECS
```

5. Unpack the source code as follows (note that you may need to install the rpm-build package):

```
# rpmbuild -bp packagename*.spec
```

6. The package's source code is installed to rpmbuild/BUILD/package, where package is the name of the software package.

7. You can now make changes to files in the package's BUILD directory. Read the README, Makefile, and other documentation files how to build the individual package. The --rebuild option to rpmbuild can be used to rebuild the rpm without installing it first. The resulting binary will be in rpmbuild/RPMS/arch, where arch is replaced by i386 or architecture you are building.

## Installing software in tar.gz or tar.bz2 formats

Here are some generic instructions you can use to install any Linux packages that are in gzip or tar format:

1. Get the source code from the Internet or from a CD and copy it into an empty directory (preferably using a name that identifies the package).
2. To check the contents of your tar archive before extracting it to your hard drive, use the following command:

```
# tar tvf package.gz
```

> NOTE: Use the command xjf if the file is compressed using bzip2.

3. Assuming the file is compressed using gzip, decompress the file using the following command:

```
# gunzip package.gz
```

The result is that file is uncompressed and .gz is removed from package (for example, package.tar). If your package ends in .bz2, use bzip2 command instead of gunzip.

4. From the resulting tar archive, run the tar command as follows:

```
# tar xvf package.tar
```

This command extracts the files from archive and copies them to a subdirectory of the current directory. Using tar xvf package.gz you can do steps 2 and 3 in one step. For a compressed bzip2 file, run xjf package.bz2.

5. Change directories to the subdirectory created in Step 3.
6. Look for a file INSTALL or README. One of these files will give you instructions on how to proceed with the installation. In general, the make command is used to install the package. Here are a few things to look for in the current directory:

If there is a configure.in file, try running:

```
# ./configure --prefix=/usr/local
# make all
```

If there is a configure file, try running:

```
# ./configure && make all
```

If there is a Makefile, try running:

```
# make all
```

After the program is built and installed, you might have to do additional configuration. You should consult the man pages or the HOWTOs that come with the software for information how to proceed.

## Using Fedora or RHEL to Run Applications

> TIP: With some tar.gz files that include an RPM spec file, you could run rpm -ba file.gz and the rpm command will build an RPM from that tarball. To try this procedure, I downloaded the package which includes utilities that you can find manual pages by entering keywords. The file I downloaded, whichman-2.2.tar.gz, was placed in a directory I created /usr/src/which. I then ran the gunzip and tar commands, whichman-2.2.tar.gz and whichman-2.2.tar as arguments, respectively.

I changed to the new directory, /usr/sw/which/whichman-2.2 and listed its contents. The README file contained information about the contents of the package and how to install it. As the README file suggested, I typed make, and then make install. The commands whichman, ftwich, and fft were installed in /usr/bin. At this point, you can check the man page for each component to see what it does.

The last thing I found in the README file was a bit of configuration needed to be done. I added a MANPATH variable to $HOME/.bashrc to identify the location of man pages on my computer to be searched by the whichman utility. The line looked like this:

```
export MANPATH=/usr/share/man:/usr/man:/usr/X11R/man:/usr/share/doc/samba-2.2.3/docs
```

If you are wondering, whichman, ftwich, and fft are commands that you can use to search for man pages. They can be used to find several locations of a man page, man pages that are close to the name you enter, or man pages that are located beneath a point in the directory structure, respectively.

Although operating systems are nice (and necessary), people use desktop computers to run application programs. There has been a common belief that Fedora or RHEL can work well as a server they are not ready to challenge Microsoft's dominance of the desktop arena. There are several reasons why, I believe, Fedora and RHEL can replace Windows on the desktop, if you are committed to doing it:

- Every category of desktop application now has an open source that will run in Linux. So, for example, Adobe Photoshop doesn't run natively in Linux, you can use the GIMP or other applications to work with digital images in Linux.
- Your Windows applications that you absolutely must have usually be run without problems using Windows emulators or compatibility programs, such as QEMU and WINE. Particular efforts have been made to get Windows games (Transgaming.com) and office productivity applications (Codewavers.com) running in Linux.
- With viruses and worms rampant in Microsoft systems, many people now believe that Linux systems offer a more secure alternative, particularly if the the desktop
