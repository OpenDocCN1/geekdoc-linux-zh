contain the Xwindow system and files. Local binaries are in /usr/bin and /usr/local/bin. Manual pages are stored in /usr/man. Many other files exist in the /usr directory; therefore it takes up a lot of space.

```
```
$ ls -ld /usr/*
lrwxrwxrwx    1 root     root            5 Aug  6 03:55 /usr/X11 -> X11R6
drwxr-xr-x    9 root     root          1024 Apr 27 1994 /usr/X11R6
lrwxrwxrwx    1 root     root            8 Aug  6 03:48 /usr/adm -> /var/adm
drwxr-xr-x    2 root     root          9216 Mar 23 12:33 /usr/bin
drwxr-xr-x    2 root     root          1024 Nov  25 1993 /usr/dict
drwxr-xr-x  116 root     root          3072 Jun  8 1994 /usr/doc
drwxr-xr-x    2 root     root          1024 Nov 25 1993 /usr/etc
drwxr-xr-x    4 root     root          1024 Jun  8 1994 /usr/games
lrwxrwxrwx    1 root     root            9 Aug  6 03:50 /usr/i486-coff -> ix86-coff
lrwxrwxrwx    1 root     root           10 Aug  6 03:50 /usr/i486-linux -> ix86-linux
lrwxrwxrwx    1 root     root           14 Aug  6 03:50 /usr/i486-linuxaout -> ix86-linuxaout
drwxr-xr-x    3 root     root          1024 Aug 13 1995 /usr/i486-sysv4
lrwxrwxrwx    1 root     root           10 Aug  6 03:51 /usr/i586-pc-linux-gnu/libc1 -> ix86-i5linux
drwxr-xr-x   20 root     root          3072 Aug  6 03:58 /usr/include
drwxr-xr-x    2 root     root          5120 Jun 20 1997 /usr/info
drwxr-xr-x    4 root     root          1024 Feb 20 22:01 /usr/ix86-coff
drwxr-xr-x    5 root     root          1024 May 15 17:15 /usr/ix86-linux
drwxr-xr-x    4 root     root          1024 Jun 11 1995 /usr/ix86-linuxaout
drwxr-xr-x   29 root     root          4096 Aug  6 03:58 /usr/lib
drwxr-xr-x    4 root     root          1024 Nov  4 1996 /usr/libexec
drwxr-xr-x   13 root     root          1024 Aug  6 03:57 /usr/local
drwxr-xr-x    2 root     root         12288 Aug  6 03:38 /usr/lost+found
drwxr-xr-x   13 root     root          1024 Jun  4 17:59 /usr/man
drwxr-xr-x    8 root     root          1024 May 26 1994 /usr/openwin
lrwxrwxrwx    1 root     root           13 Aug  6 03:48 /usr/preserve -> /var/preserve
drwxr-xr-x    3 root     bin           3072 Aug  6 03:53 /usr/sbin
drwxr-xr-x   10 root     root          1024 Feb 14 11:55 /usr/share
lrwxrwxrwx    1 root     root           10 Aug  6 03:48 /usr/spool -> /var/spool
drwxr-xr-x    3 root     root          1024 Aug  6 03:52 /usr/src
lrwxrwxrwx    1 root     root            8 Aug  6 03:48 /usr/tmp -> /var/tmp
```
```

The /var directory contains various system administration files. These include the log files, the spool directory for mail, cron, printing, and other applications. It also contains the process ID information (/var/pid) and other system information.