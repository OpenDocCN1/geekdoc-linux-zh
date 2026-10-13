# Chapter 8: The Shell

# Overview

The shell is a command interpreter that provides a line-oriented interactive and noninteractive interface between the user and the operating system. You enter commands on a command line; they are interpreted by the shell and then sent as instructions to the operating system. You can also place commands in a script file to be consecutively executed much like a program. This interpretive capability of the shell provides for many sophisticated features. For example, the shell has a set of file expansion characters that can generate filenames. The shell can redirect input and output, as well as run operations in the background, freeing you to perform other tasks.

Several different types of shells have been developed for Linux: the Bourne Again shell (BASH), the Public Domain Korn shell (PDKSH), the TCSH shell, and the Z shell. All shells are available for your use, although the BASH shell is the default. You only need one type of shell to do your work. Red Hat Linux includes all the major shells, although it installs and uses the BASH shell as the default. If you use the Red Hat Linux command line shell, you will be using the BASH shell unless you specify another. This chapter discusses the BASH shell, which shares many of the same features as other shells.

**Note** You can find out more about the BASH shell at [www.gnu.org/software/bash](http://www.gnu.org/software/bash). A detailed online manual is available on your Linux system using the `man` command with the `bash` keyword.