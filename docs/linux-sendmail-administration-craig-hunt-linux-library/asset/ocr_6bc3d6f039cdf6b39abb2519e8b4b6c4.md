```
install -c -o bin -g bin -m 444 vacation.0 /usr/man/man1/vacation
make[1]: Leaving directory
```

/usr/local/src/sendmail-8.11.0/obj.Linux.2.2.10.i586/vacation'

The build command installs the man pages in the /usr/man directory and the executables in /usr/sbin and /usr/bin. It installs the help file (sendmail.hf) and the status file (sendmail.st) in /etc/mail.

# Known Problems

The Sendmail documentation lists some problems that are known to affect compilation on Linux systems. The problems fall into several categories ranging from compiler problems to kernel problems.

Two problems relate to GNU tools that are commonly used on Linux systems. One is an incompatibility detected between GDBM and Sendmail 8.8. Later versions of Sendmail improved the heuristic to detect GDBM so that the Sendmail code can adapt to GDBM. The Sendmail release notes suggest Berkeley Daly instead of GDBM.

The other GNU problem is with the gcc compiler. Old versions of gcc, versions 2.4 and 2.5, cannot be used to compile Sendmail with the compiler optimization (-o) option. This was fixed when version 2.6 was released. The Caldera system used to generate the example in Listing 3.10 used the Experimental GNU Compiler Suite 2.91, which is a follow-on to gcc.

Several problems are described that existed with very old kernels (pre-version 1.0), very old versions of glibc (pre-version 4.7), and a very old version of the BIND name software (version 4.9.3). No one should currently be running any of this software.

The Sendmail documentation also reports problems that relate to having previously BIND on your system. The symptoms of this problem are unresolved references during the link phase of the Sendmail compile. If you have compiled BIND from source code on your system and BIND wrote header files in /usr/local/lib and /usr/local/, these may cause problems when Sendmail is compiled. The documentation suggests -resolv to LIBS in the Sendmail Makefile to avoid this problem.

Finally, the documentation mentions problems with Linux kernel 2.2.0. This is the most worrisome of the problems reported by the documentation does not provide a workaround for this problem. I have never personally seen this problem, but if I did, I would upgrade the Linux kernel to the highest patch.

Frankly, none of the problems described in the Sendmail installation notes has ever struck any Linux system that I have worked with. A far more common occurrence is