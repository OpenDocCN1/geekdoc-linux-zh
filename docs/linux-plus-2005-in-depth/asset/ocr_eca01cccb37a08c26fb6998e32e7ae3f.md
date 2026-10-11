accessed easily. The most common form of documentation for Linux commands is **manual pages** (commonly referred to as man pages). Simply type the man command followed by a command name, and extensive information about that Linux command is displayed page-by-page on the terminal screen. This information includes a description of the command and its syntax, as well as available options, related files, and commands. For example, to receive information on the format and usage of the whoami command, you can use the following command:

```
[root@serverl root]# man whoami
```

The manual page is then displayed page-by-page on the terminal screen. You can use the cursor (arrow) keys on the keyboard to scroll though the information or press q to quit. The manual page for whoami is similar to the following:

```
WHOAMI(1)           User Commands           WHOAMI(1)

NAME
       whoami - print effective user id

SYNOPSIS
       whoami [OPTION]...

DESCRIPTION
       Print the user name associated with the current effective
       user id.  Same as id -un.

       --help      display this help and exit

       --version   output version information and exit

AUTHOR
       Written by Richard Mlynarik.

REPORTING BUGS
       Report bugs to <bug-coreutils@gnu.org>.

COPYRIGHT
       Copyright © 2004 Free Software Foundation, Inc.
       This is free software; see the source for copying condi-
       tions.  There is NO warranty; not even for MERCHANTABILITY
       or FITNESS FOR A PARTICULAR PURPOSE.
```