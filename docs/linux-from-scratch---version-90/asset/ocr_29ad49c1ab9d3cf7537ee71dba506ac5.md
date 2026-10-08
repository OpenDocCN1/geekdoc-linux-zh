# Sysklog

This package contains programs for logging system messages, such as those given by the kernel or daemon processes when unusual events occur.

+   - Sysvinit

This package provides the init program, which is the parent of all other processes on the Linux system.

+   - Tar

This package provides archiving and extraction capabilities of virtually all packages used in LFS.

+   - Tcl

This package contains the Tool Command Language used in many test suites in LFS packages. It is only installed in the temporary toolchain.

+   - Texinfo

This package contains programs for reading, writing, and converting info pages. It is used in the installation procedures of many LFS packages.

+   - Util-linux

This package contains miscellaneous utility programs. Among them are utilities for handling file systems, consoles, partitions, and messages.

+   - Vim

This package contains an editor. It was chosen because of its compatibility with the classic editor and its huge number of powerful capabilities. An editor is a very personal choice for many users and any other editor could be substituted if desired.

+   - XML::Parser

This package is a Perl module that interfaces with Expat.

+   - XZ Utils

This package contains programs for compressing and decompressing files. It provides the highest compression generally available and is useful for decompressing packages in XZ or LZMA format.

+   - Zlib

This package contains compression and decompression routines used by some programs.

# Prerequisites

Building an LFS system is not a simple task. It requires a certain level of existing knowledge of Unix system administration in order to resolve problems and correctly execute the commands listed. In particular, as an absolute minimum, you should already have the ability to use the command line (shell) to copy or move files and directories, directory file contents, and change the current directory. It is expected that you have a reasonable knowledge of using and installing Linux software.

Because the LFS book assumes at least this basic level of skill, the aware LFS forums are unlikely to be able to provide you with much assistance in these areas. You will find that your questions regarding such basic knowledge will likely go unanswered or simply be referred to the LFS essential pre-reading list.

Before building an LFS system, we recommend reading the following: