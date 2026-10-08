
[content]

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
```

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
the result on the standard output. The name '-' means
standard input. If no input files are named, the standard
input is sorted.

# Hour 1

The default sort key is an entire line. Default ordering is lexicographic by bytes in machine collating sequence. The ordering is affected globally by the following options, one or of which may appear.

Ignore leading blanks (spaces and tabs) in field com--More

On almost every system, the man command feeds output through the more program so that information won't scroll by faster than you can read. You can also see the output of a man command to a file if you need to study the information in detail. To save this particular manual entry to the file sort.manpage, you could use sort > sort.manpage.

Notice in the sort page that there are many options to the sort command (certainly more than discussed in this book). As learn UNIX, if you find areas about which you'd like more information, or if you need a capability that doesn't seem to be available, check the man page. There just might be a flag for what you seek.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_28_0.png)

You obtain lots of valuable information by reading the introduction to each section of the man pages. Use man 1 intro to read the introduction to Section 1, for example.

If your version of man doesn't stop at the bottom of each page, you can remedy the situation using atlas man "\* | more".

# JUST A MINUTE

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_28_1.png)

UNIX was one of the first operating systems to include online documentation. The man pages are an invaluable reference. Most of them are poorly written, unfortunately, and precious few examples of actual usage. However, as a quick reminder of flags and options, as an easy way to find the capabilities of a command, man is great. I encourage you to explore the man pages and even read the man page on command itself.

# SUMMARY

# Task 1.2: Other Ways to Find HELP in UNIX

The man pages are really the best way to learn about what's going on UNIX commands, but some alternatives also prove helpful. Some systems have a help command. Many UNIX utilities make information available with the -h or ? flag. Finally, one trick you can try is feed a set of gibberish flags to a command, which sometimes generates an error and a helpful message reminding you what possible the command accepts.

# DESCRIPTION

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_28_2.png)

14

1

# What Is This UNIX Stuff?

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_29_0.png)

If your version of man doesn't stop at the bottom of each page, you can remedy the situation using atlas man "\* | more".

# JUST A MINUTE

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_28_1.png)

UNIX was one of the first operating systems to include online documentation. The man pages are an invaluable reference. Most of them are poorly written, unfortunately, and precious few examples of actual usage. However, as a quick reminder of flags and options, as an easy way to find the capabilities of a command, man is great. I encourage you to explore the man pages and even read the man page on command itself.

# SUMMARY

# Task 1.2: Other Ways to Find HELP in UNIX

The man pages are really the best way to learn about what's going on UNIX commands, but some alternatives also prove helpful. Some systems have a help command. Many UNIX utilities make information available with the -h or ? flag. Finally, one trick you can try is feed a set of gibberish flags to a command, which sometimes generates an error and a helpful message reminding you what possible the command accepts.

# DESCRIPTION

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_28_2.png)

14

1

# What Is This UNIX Stuff?

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_30_0.png)

