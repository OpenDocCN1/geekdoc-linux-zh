# 6.6. Creating Essential Files and Symlinks

Some programs use hard-wired paths to programs which do not exist. In order to satisfy these programs, create a number of symbolic links which will be replaced by real files throughout the course of this chapter after the software has been installed:

```
ln -sv /tools/bin/{bash, cat, chmod, dd, echo, ln, mkdir, pwd, rm, stty} /bin
ln -sv /tools/bin/env, install, perl, printf /usr/bin
ln -sv /tools/lib/libgcc_s.so,.1} /usr/lib
ln -sv /tools/lib/libstdc++.{a,.6} /usr/lib

ln -sv bash /bin/sh
```

The purpose of each link:

+   * /bin/bash
Many bash scripts specify /bin/bash.
* /bin/cat
This pathname is hard-coded into Glibc configure script.
* /bin/dd
The path to dd will be hard-coded into the /usr/bin/libtool utility.
* /bin/echo
This is to satisfy one of the tests in Glibc's test suite, which expects /bin/echo.
* /usr/bin/env
This pathname is hard-coded into some packages build이라.
* /usr/bin/install
The path to install will be hard-coded into the /usr/lib/bash/Makefile.inc file.
* /bin/ln
The path to ln will be hard-coded into the /usr/lib/perl5/5.30.0/<target-triplet>/Config_heavy.pl file.
* /bin/pwd
Some configure scripts, particularly Glibc's, have this pathname hard-coded.
* /bin/rm
The path to rm will be hard-coded into the /usr/lib/perl5/5.30.0/<target-triplet>/Config_heavy.pl file.
* /bin/tty
This pathname is hard-coded in Expect, therefore it is needed for Binutils and GCC test suites to pass.
* /usr/bin/perl
Many Perl scripts hard-code this path to the perl program.
* /usr/lib/libgcc_s.so,.1
Glibc needs this for the threads library to work.
* /usr/lib/libstdc++{,.6}
This is needed by several tests in Glibc's test suite, as well as C++ support in GMP.
* /bin/sh
Many shell scripts hard-code /bin/sh.