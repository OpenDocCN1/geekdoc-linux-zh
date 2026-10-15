are created and not passed on to any processes spawned from that shell. The built-in set command will display local variables for C shell and TC shell, and both local and environment variables for Bourne, Bash, and Korn shells. Environment variables, on the other hand, are passed from parent to child process, from child to grandchild, and so on. Some of the environment variables are inherited by the login shell from the /bin/login program. Others are created in the user initialization files, in scripts, or at the command line. If an environment variable is set in the child shell, it is not passed back to the parent. The shell env command will display the environment variables. Example 1.11 lists environment variables for a user running Solaris 5.9 with the Bash shell.

# EXAMPLE 1.11

```
$ env
PWD=/home/ellie
TZ=US/Pacific
PAGER=less
HOSTNAME=artemis
LD_LIBRARY_PATH=/lib:/usr/lib:/usr/local/lib:/usr/dt/lib:/usr/openwin/lib
MANPATH=/usr/local/man:/usr/man:/usr/openwin/man:/opt/httpd/man
USER=ellie
MACH_TYPE=sparc-sun-solaris2.9
TCL_LIBRARY=/usr/local/lib/tcl8.0
EDITOR=vi
LOGNAME=ellie
SHLVL=1
SHELL=/bin/bash
HOSTTYPE=sparc
OSTYPE=solaris2.9
HOME=/home/ellie
TERM=xterm
TK_LIBRARY=/usr/local/lib/tk8.0
PATH=/bin:/usr/bin:/usr/local/bin:/usr/local/etc:/usr/ccs/bin:/usr/etc:/usr/ucb:/usr/local/X11:/usr/openwin/bin:/etc:.
SSH_TTY=/dev/pts/10
_=/bin/env
```

# 1.6.6 Redirection and Pipes

# File Descriptors.

All I/O, including files, pipes, and sockets, is handled by the kernel via a mechanism called the file descriptor. A file descriptor is a small unsigned integer, an index into a file-descriptor table maintained by the kernel and used by the kernel to reference open files and I/O streams. Each process inherits its own file-descriptor table from its parent. The first three file descriptors, 0, 1, and 2, are assigned to your terminal. File descriptor 0 is standard input (stdin), 1 is standard output (stdout), and 2 is standard error (stderr). When you open a file, the next available descriptor is 3, and it will be