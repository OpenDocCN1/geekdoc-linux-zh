
# THE make PROGRAM 325

directory tree specified by the programmer and sets the appropriate access rights as well.

Listing 11.2 shows a slightly more complex Makefile, which uses both variables and default rules for compilation instead of the call of gcc.

This Makefile shows a certain resemblance to the commonly used Makefiles. In the first section, some variables are set which can later be used in the rules or dependencies. With the variable CFLAGS, the options for the C compiler are set. Here, it is the option -2 for optimization. The variable LDFLAGS contains the options for the linker; here, the option -s is used.

In this Makefile, the prune program is created in two steps: first, the source code is translated into the so-called object format (file name prune.o). Subsequently, this object file is linked with the standard C library to create an executable program. Both are default rules; the definition of all default rules can be displayed by means of the command make -p.

```
CFLAGS=-2
LDFLAGS=-s
INSTALLDIR=/usr/local/sbin

all: prune

install: prune
    install -m 755 prune $(INSTALLDIR)/prune
echo "edit /etc/prune.conf to suit your system"

prune: prune.o
clean:
    rm -f prune.o
```

Listing 11.2 A slightly more complex Makefile.

In the install target, the program is copied into the directory INSTALLDIR. A new member is the target clean, which deletes previously generated programs or object files. The next make call must then completely recompile the program, which makes sense, for example, in case of configuration changes. Another frequently used target is dist, which usually creates a tar file with the source code.

In larger programs, it is often necessary to adapt individual parameters before the compilation; for example, the names of configuration or lock files, or the installation directories. Usually, these variables can be found at the beginning of the Makefiles, where you can also find comments on the meaning of the variables.

The make program has a series of options that can influence the operation of make. An important and useful one is the option -n, which causes make to display the necessary commands instead of executing make. Thus, it is possible, for example, to verify which files will be installed by using the command make -n install instead of make.

make can start several programs simultaneously, so that on computers with sufficient memory, the CPU can be charged to capacity as far as possible. The option -j allows parallel execution of several programs. If this option is followed by a number, the number of programs started simultaneously by make is limited to this number. Without this, there is no limit.

With the start of many processes, the 'load', that is, the number of processes competing for processor time, goes up. With the option -l, followed by a number, new processes are started if other processes are still running and the load is greater than this. If no number is specified, the load is not considered. Thus, if you start make processes, you must keep an eye on the occupation of main memory and processor load to obtain benefits in use. Obviously, multi-processor machines have a significant advantage.

```
report.dvi:report.tex figure1.eps figure2.eps
latex report

%.eps:%fig
fig2dev -L ps $< $
```

Listing 11.3 A Makefile for LaTeX

Listing 11.3 shows an example for the use of make to generate the DVI file report.dvi. This file is dependent on the source text report.tex and the illustrations figure1.eps and figure.eps. These illustrations were generated with the xfig program and converted into eps format (Encapsulated PostScript). The use of make automates the conversion of the illustrations and ensures that the most-to-date illustrations are always included in the DVI file.

This example also shows further functions of make. The symbol $ represents the files needed as input, the symbol $ is replaced at runtime with the name of the file to be generated. These symbols are used in a rule which describes the general dependencies between illustrations (.fig) and their format (.eps). Thus it is not necessary to specify a rule for each illustration.

This information is intended to help you understand Makefiles. Before you begin to develop your own Makefiles, you should read the manual for GNU make, which is distributed in Texinfo format. It provides extensive documentation on the use of make and the creation of Makefiles. If you frequently edit Makefiles, you can use the makefile-mode of the emacs editor, which provides a series of useful functions.

For the GNU project programs, the document standards.texinfo provides a sort of prescription, as well as the C programming and the style to be employed, also outlines the most important functions for a Makefile. You may not agree with all of these prescriptions, but the document certainly contains a series of useful hints.

| Additional Information and Sources |
|---|---|
| Documentation: | make(1), Texinfo manual |
| ftp server: | ftp.gnu.org |
| ftp path: | /pub/gnu |
| File name: | make-3.72.1.tar.gz |
| Size: | about 550 Kbytes |

# 11.2 The imake program

The imake program is a part of the X Window system and is therefore often used to compile X programs. For any such program, an Imake is created which describes the programs and libraries to be compiled. On the basis of system-specific configuration files, a Makefile is generated from the Imake which is then used for the compilation of the program.

Usually, the system-specific Makefile is generated by means of the xmkmf command. If the sources of the program are distributed across several directories, the Makefiles can also be automatically generated in the subdirectories by means of the xmkmf -a command. For this purpose, xmkmf internally starts make Makefiles and subsequently make includes and may depend.

The configuration files for the imake program can be found in the directory /usr/X11R6/lib/X11/config. The file linux.cf contains all necessary adaptations for LINUX. User-defined adaptations can be made in the file site.def, but usually none are required. A complete introduction to use and configuration of imake can be found, for example, in Dubois(1993).

# 11.3 Installation of programs

One recurrent task a UNIX system administrator is faced with all the time is the installation of new programs or new versions of existing programs. Practically all programs used under LINUX are free, that is, the source code is available. Since this software is generally also employed under other UNIX systems, it must be portable compilation on different platforms. Thus, the programs must be between different systems.

# 11.3.1 Installation of GNU programs

The aim of the Free Software Foundation (FSF) is the creation of a free, UNIX-like operating system (The Hurd). All essential UNIX programs are developed and employed over the world under the most disparate UNIX versions. Many of the programs employed over Linux are GNU versions of the standard UNIX service programs. Therefore, Linux is described as a GNU system on a Linux basis. Without these programs, Linux would not be what it is today.

The GNU programs are portable and powerful, therefore they are installed on many computers in addition to standard UNIX service programs. The portability is achieved by analysing the system before the program is compiled and by adapting the program accordingly. The analysis of the system is started by many of the configure script. The GNU project has some standards for the creation of programs and Makefiles which are observed by nearly all GNU programs. You can find the GNU coding standard on every GNU mirror in the file standards.texi.

The configure script analyzes the system and compiles a series of tests for the program. First, however, we have look at some examples for the configuration of GNU programs. We begin with the configuration of gzip. The GNU replacement of UNIX compress gzip substantially better and has the advantage that no license on the basis of existing patents is needed for its use.

```
(Linux):> tar zxf /tmp/gzip-1.2.4.tar.gz
(Linux):> cd gzip-1.2.4
(Linux):> ~/gzip-1.2.4 ./configure
```

Listing 11.4 Unpacking and configuring a GNU program.

The script displays a series of messages which allow you to follow the course of the configuration. More recent versions of GNU programs are distributed with configure scripts that also display the results of the analyses. At the end of the configure run, a Makefile is created with which the program can be compiled. The number of displayed messages can be influenced with the options --verbose or --quiet.
