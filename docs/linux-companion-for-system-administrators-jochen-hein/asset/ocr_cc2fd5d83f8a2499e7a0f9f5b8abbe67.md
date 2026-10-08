# 328 TOOLS (NOT ONLY) FOR PROGRAMMERS

this software is generally also employed under other UNIX systems, it must be portable compilation on different platforms. Thus, the programs must be between different systems.

# 11.3.1 Installation of GNU programs

The aim of the Free Software Foundation (FSF) is the creation of a free, UNIX-like operating system (The Hurd). All essential UNIX programs are developed and employed over the world under the most disparate UNIX versions. Many of the programs employed over Linux are GNU versions of the standard UNIX service programs. Therefore, Linux is described as a GNU system on a Linux basis. Without these programs, Linux would not be what it is today.

The GNU programs are portable and powerful, therefore they are installed on many computers in addition to standard UNIX service programs. The portability is achieved by analysing the system before the program is compiled and by adapting the program accordingly. The analysis of the system is started by many of the configure script. The GNU project has some standards for the creation of programs and Makefiles which are observed by nearly all GNU programs. You can find the GNU coding standard on every GNU mirror in the file standards.~texi.

The configure script analyzes the system and compiles a series of tests for the program. First, however, we have look at some examples for the configuration of GNU programs. We begin with the configuration of gzip. The GNU replacement of UNIX compress gzip packs substantially better and has the advantage that no license on the basis of existing patents is needed for its use.

```
(Linux):> tar zxf /tmp/gzip-1.2.4.tar.gz
(Linux):> cd gzip-1.2.4
(Linux):> ~/gzip-1.2.4 ./configure
```

Listing 11.4 Unpacking and configuring a GNU program.

The script displays a series of messages which allow you to follow the course of the configuration. More recent versions of GNU programs are distributed with configure scripts that also display the results of the analyses. At the end of the configure run, a Makefile is created with which the program can be compiled. The number of displayed messages can be influenced with the options --verbose or --quiet.