# 258 Part II: Using Fedora and RHEL

To format a man for typesetting, you can specify PostScript or HP LaserJet output. you should direct the output to a file or to a printer. Here are a couple of examples:

```
$ groff -Tps -man /tmp/chown.1 > /tmp/chown.ps
$ groff -Tlj4 -man -1 /tmp/chown.1
```

The first example creates PostScript output (-Tps) and directs it to a file /tmp/chown.ps. This file can be read by a PostScript viewer (as Ghostscript) or sent to a printer (lpr /tmp/chown.ps). The next example handles LaserJet output (-Tlj4) and directs it to the default (-option).

> TIP: you can convert man pages to HTML format for viewing in a browser. For example:cat /usr/share/man/man1/chown.1.gz | man2html | /tmp/chown.html.

# Creating a man page with Groff

Before WHO-TO and info files, man pages were the foundation for information about UNIX (and UNIX-like) systems. Each command, file format, device, or other had its own man page or was grouped on a man page with similar components. Creating your own man page requires that you learn a few macros (in particular, man macros). Figure 6-3 shows the source for a fictitious man page for a command waycool.

```
. the document processor source for the command waycool
.TH way 1 "May 12, 2000" "GNU Linux Programmer's Manual"
.SH NAME
.waycool -v my cool command
.BR
.BfwaycoolVR [V-abfVR] [I file ...]
.SH SYNOPSIS
This man page documents the GNU waycool usage X,XX
.SH DESCRIPTION
.BfwaycoolVR is a cool command.
.SH VERSION
The first version of \waycoolVR is better than the last one.
.SH OPTIONS
-o
All options, with it:
-a
Run all options, with the file.
-f
effects files linked to any referenced file
available only on systems that can change the
behavior of a symbolic link.
-v
Print the version number with the command.
.SH COMMENTS
If you like this command, don't tell me. It will just hurt my friends.
.SH ENVIRONMENT
Some environment variables are used by \waycoolVR:
.SH UID
This sets the UID display variable.
.SH PATH
This contains the location of the waycool database.
.SH FILES
.Bf
/usr/local/share/commodity.com/
.SH REPORTING
Report bugs to waycool functionality.
.SH COPYRIGHT
Copyright (c) 2003 Free Software Foundation, Inc.
.AR
This is free software: some for copying commands. There is NO
guarantee for MAINTAINABILITY or FITNESS FOR A PARTICULAR PURPOSE.
.SH ACKNOWLEDGEMENTS
I'd like to talk to all of my friends.
```

Figure 6-3: Simple markup is required to create man pages.