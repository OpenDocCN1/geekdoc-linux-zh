```
TERM=xterm-color
BLOCKSIZE=K
SHELL=/bin/csh
SSH_CLIENT=182.185.191.114 52885 22
SSH_CONNECTION=182.185.191.114 52885 202.147.169.196 22
SSH_TTY=/dev/pts/1
HOSTTYPE=FreeBSD
VENDOR=amd
OSTYPE=FreeBSD
MACHETYPE=x86_64
SHLVL=1
PWD=/home/sarwar
GROUP=faculty
HOST=pcbsd-srv
REMOTEHOST=182.185.191.114
LANG=en_US.UTF-8
EDITOR=vi
PAGER=more
MANPATH=/usr/share/man:/usr/local/man:/usr/share/openssl/man:/usr/pbi/man:/usr/local/lib/perl5/5.16/man:/usr/local/lib/perl5/5.16/perl/man
NO_PROXY=127.0.0.1,localhost
no_proxy=127.0.0.1,localhost
CLICOLOR=true
MORE=-erX
%
```

In the following in-chapter exercises, you will create a simple shell script and make it executable. Also, you will use the set and env commands to display the names and values of shell variables in your environment.

# EXERCISE 14.1

Display the names and values of all shell variables on your UNIX machine. What command(s) did you use?

# EXERCISE 14.2

Create a file that contains a shell script comprising the date and who commands, one on each line. Make the file executable and run the shell script. List all the steps for completing this task.

# 14.4 READING AND WRITING SHELL VARIABLES

You can use any of three commands to assign a value to (write) one or more shell variables (environmental or user-defined): @, set, and setenv. The set and setenv commands are used to assign a string to a variable. The difference is that the setenv command