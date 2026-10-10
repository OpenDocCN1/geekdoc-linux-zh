# Part I: The Linux Command Line

The GNU organization (GNU stands for GNUs Not UNiX) developed a complete set of UNIX utilities but had no kernel system to run them on. Although the bundling of the Linux kernel and GNU utilities is often just called Linux, you will see some Linux purists on the Internet refer to it as the GNU/Linux system to give credit to the GNU organization for its contributions to the cause.

# The core GNU utilities

The GNU project was mainly designed for UNIX system administrators to have a UNIX-like environment available. This focus resulted in the project porting many common UNIX system command-line utilities. The core bundle of utilities supplied for Linux systems is called the coreutils package.

The GNU coreutils package consists of three parts:

+   - Utilities for handling files
+   - Utilities for manipulating text
+   - Utilities for managing processes

Each of these three main groups of utilities contains several utility programs that are invaluable to the Linux system administrator and programmer. This book covers each of the utilities contained in the GNU coreutils package in detail.

# The shell

The GNU/Linux shell is a special interactive utility. It provides a way for users to start programs, manage files on the filesystem, and manage processes running on the Linux system. The core of the shell is the command prompt. The command prompt is the interactive part of the shell. It allows you to enter text commands, and then it interprets the commands and executes them in the kernel.

The shell contains a set of internal commands that you use to control tasks such as copying files, moving files, renaming files, displaying the programs currently running on the system, and stopping programs running on the system. Besides the internal commands, the shell allows you to enter the name of a program at the command prompt. The shell passes the program name to the kernel to start it.

You can also group shell commands into files to execute as a program. Those files are called shell scripts. Any command that you can execute from the command line can be placed in a shell script and run as a group of commands. This provides great flexibility in creating utilities for commonly run commands or processes that require several commands grouped together.

Quite a few Linux shells are available to use on a Linux system. Different shells have different characteristics, some being more useful for creating scripts and some being more useful for managing processes. The default shell used in all Linux distributions is the Bash shell. The Bash shell was developed by the GNU project as a replacement for the standard UNiX shell, called the Bourne shell (after its creator). The Bash shell name is a play on this wording, referred to as the “Bourne again shell.”