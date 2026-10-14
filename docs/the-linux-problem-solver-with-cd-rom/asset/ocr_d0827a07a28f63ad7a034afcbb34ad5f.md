# PROBLEM 67

> **Symptoms:** You get errors referring to items like `/dev/rft0`, or tar hangs.
> 
> **Problem:** No file specified for tar.
> 
> **Fix:** The `-f` option to tar is important. Without it, tar thinks you're looking at the default device, which happens to be a tape drive.

# Taking a Look at the Extracted Source Files

Now that you’ve extracted the source and found your way into its directory, take a look around. There you’ll find files with names like INSTALL, README, Makefile.in, and configure.

# README and Other Installation Guide Files

If there’s a README file, look at it first. Usually it describes the software package, but sometimes it contains a small manual, instructions, or other notes. You might also find some other README files such as README.linux or README.first, containing additional remarks about use under Linux, special cautions, and so on.

The installation manual (with a name like INSTALL) is probably the next item to inspect—that is, if there is one. Many packages that use GNU autoconf have generic installation instructions (for an in-depth look at autoconf, see below).

It’s especially important to check the compile-time options, which set various devices. An incorrect or awkward configuration, whether it’s for a default paper size or a standard device, can cause constant annoyance.

# GNU autoconf and Makefile

If the package uses GNU autoconf, it most likely won’t have a Makefile in the clean, untouched distribution. If it doesn’t use autoconf, it might have an Imakefile (which uses a program called imake), or a special little script (called build, compile, or some similar name) from the author.

# The Source Code

The source code files can appear pretty much anywhere—all in the main directory (which is fine if there aren’t too many of them), or systematically parceled out into different libraries and packages. C source files have a .c extension, C++ files have suffixes like .cc, .C, and .cxx, and header files for either end with .h.