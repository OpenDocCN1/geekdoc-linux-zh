If you choose to compile, GIMP has been designed to be a compiler-friendly
(ANSI C) as possible. However, in reality nothing compiles the GIMP as pain-
lessly as the trusty GNU C compiler (and variants), as the proprietary compil-
ers might not have all the features necessary to compile the GIMP, though
should. You might want to check and see if you have the gcc compiler
installed. (Issue a gcc -v). If not, you might need to ask yourself why the
neck not! Obtain it from http://www.gnu.org/software/gcc/gcc.html.

![](bbox=[0.155, 0.137, 0.263, 0.193])

# Installing GIMP

The following sections contain instructions for installing GIMP on your system. The first
thing to do in approaching GIMP installation is to determine which installation method
you want to use. Depending on your situation, there are a few different ways to go about
installing GIMP.

# Binary Installation

If you want to get the GIMP up and running as quickly and painlessly as poss-
ble, binary installation is by far the best way to go. (Binary is another term for
executable program.) This means that you will install the program into its proper
place, and then run it.

> NEW TERM

Note that the binaries on the CD-ROM are for Linux 2.0+, Solaris, and IRIX
only. If you are running another platform, you will need to get the binaries
elsewhere, or compile the source code on your machine.

![](bbox=[0.175, 0.608, 0.273, 0.663])

There are generally two main ways to go about a binary installation: the standard way
by using a package manager.

# The Standard Way

The standard way to go about a binary installation is to grab the program in the form
of compressed archive (usually a tar.gz file), decompress the archive (tar -xzvf *.tar.gz),
and put the files where they need to go according to the documentation. The GIMP
for Solaris on the CD-ROM is packaged in this manner.

# Using RPM

Another popular way to do this is using RPM—the Red Hat Package Manager. This
program, which is available by default on the Red Hat, Caldera, and S.u.S.E distributions