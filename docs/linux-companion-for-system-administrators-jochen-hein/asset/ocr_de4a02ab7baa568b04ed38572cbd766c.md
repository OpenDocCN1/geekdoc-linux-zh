# 330 TOOLS (NOT ONLY) FOR PROGRAMMERS

accordingly. These features are either reimplemented or sometimes functions of the program are disabled. The autoconf documentation describes this in detail.

```
(Linux): ~/gzip-1.2.4> make CFLAGS=-O2 LDFLAGS=-s
(Linux): ~/gzip-1.2.4> su
(Linux): ~/gzip-1.2.4> make CFLAGS=-O2 LDFLAGS=-a install
```

Listing 11.7 Passing special flags to make.

The standard format for the documentation of GNU programs is Texinfo. This allows you to create both printed and online documentation on the basis of the same source text. Man pages are also often installed for reference, offering a brief overview of the program's options.

# 11.3.2 Installation of other programs

Programs that are not part of the GNU project are installed in many different ways. Often, a precise description of the installation is given in the README or INSTALL files. Reading these files is essential before starting the installation. Frequently, there is also a file that contains tips and tricks for individual operating systems.

One possibility for compiling programs under different UNIX systems is the creation of a Makefile for each operating system. The appropriate Makefile must be copied and, if needed, adapted. Other programs with a large Makefile which contains all configurations for the different systems. In this case, the correct setting must be activated by means of an editor.

In many cases, the programs are already prepared for compilation and installation under LINUX. Sometimes this is not the case, but often no changes are required for LINUX anyway. Usually, you can use the settings for POSIX system. If the Makefile only considers System V and BSD-based systems, you should try the System V setting. This would be sufficient to compile many of today's freely available programs. If you need to make substantial changes to the source code or the Makefiles, you should send these to the programmer. Thus, in a later version, other users can benefit from your experience.

Currently, a relatively large number of programs is being adapted for with GNU configure. This is a relatively expensive operation, but it significantly improves portability.