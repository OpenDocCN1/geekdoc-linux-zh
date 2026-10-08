# THE /usr HIERARCHY 29

Please note that this is an exception to the rule that no package should get a directory of its own in /usr.

| Symbolic name | Real name |
|---|---|
| /usr/bin/X11 | /usr/X11R6/bin |
| /usr/lib/X11 | /usr/X11R6/lib/X11 |
| /usr/include/X11 | /usr/X11R6/include/X11 |

Table 2.5 Compatibility links for X.

# 2.4.2 /usr/bin - programs

The /usr/bin directory is the primary directory for programs in a LINUX or UNIX system. An exception is constituted by programs that are exclusively destined to be used by the system administrator (these programs are stored in the corresponding /sbin directory), programs that have been installed installed by the administrator in /usr/local for the system in question, and the programs required for system start-up, which must be located in /bin.

When creating scripts that are started via the ! mechanism, you must specify the complete path to the interpreter. The character sequence ! tells the kernel that the program cannot be started directly, but has to be processed by an interpreter. Thus, the interpreter is loaded and passed the script.

The absolute path is no problem for sh or c scripts since these programs can be found in the /bin directory in every UNIX system. More problems are caused by interpreters, such as perl, tcl, or python, which are often installed in different locations. Scripts that use these interpreters can often not be ported unchanged from one system to the other, because the path in the first line of the script must be modified. Here, the file system hierarchy recommends that these interpreters be installed in the /usr/bin directory, or that symbolic links to the programs should be established. Then scripts can reference the interpreter in /usr/bin, independently of the directory in which the programs are actually installed.

# 2.4.3 /usr/include - include files

This directory contains the header or include files for the C library libc. It contains a series of subdirectories in which the header files for different subsystems are stored. The header files belonging to libc are not complete; the kernel-specific header files are missing. Here, the symbolic links to the kernel