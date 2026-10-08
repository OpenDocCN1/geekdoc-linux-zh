# What Is This UNIX Stuff?

```
% alias apropos _man -k \* | uniq
% apropos cd
bcd (6) - convert to antique media
cd (1) - change working directory
cdplayer - CD-ROM audio demo program
cdrom (4S) - CDROM control operations
draw, bdraw cdraw - interactive graphics drawing
fcdmd, fcd (1) - change client's current working directory
in the FSP database
getfinfo, getatcd, getflag, getacin, setac, endac (3) - get audit
```

control file information
ioctl (25) - Ethernet-to-IP address allocator
mp, madd, msum, multiv, mcmp, min, pow, god, gpow, itom, xtom,
mmtox, mfree (3X) - multiple precision integer arithmetic
rexed, inreced (8C) - remote execution server
sccs-cdc, cdc (1) - the delta commentary of an SCCS delta
srt (45) - driven by CDROM SCSI controller
termios, toctattr, toctatrx, tsendbreak, tcdrain, tcflush, tcflow,
cfgetpeed, cfgetpeed, cfsetpeed, cfsetpeed (3V) - get and set
terminal_attributes - Line control, get and set baud rate,
and set foreground process group ID

tin, rtin, cdtin, tind (1) - A Threaded Networks reader\uid_alloc, gid_alloc (8C) - UID and GID allocator daemons

That's better, but I'd like to tell me about only user commands
i don't care much about file formats, games, or miscellaneous commands
when I'm looking for a command. I'll try this:

```
% alias apropos _man -k \* | uniq grep _
% apropos cd
cd (1) - change working directory
fcdmd, fcd (1) - change client's current working directory
in the FSP database
```

sccs-cdc, cdc (1) - change delta commentary of an SCCS delta
tin, rtin, cdtin, tind (1) - A Threaded Networks reader

That's better.

I'd like to look up one more command—before I'm done here.

% man sort

SORT(1) DYNIX Programmer's Manual SORT(1)

NAME
sort - sort or merge files

```
SYNOPSIS
sort [-mubdbfintx ] [+pos1 [ -pos2 ] ... [ -o name ]
[-T directory ] [ name ] ...
```

DESCRIPTION
Sort lists of lines of all named files together and writes
t result on the standard output. The name '-' means
standard input. If no input files are named, the standard
input is sorted.