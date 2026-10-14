/usr/local/samba/bin/smbclient "\\\\server\\$service" $password -U $server -N -p $logfile

The effect is that Ghostscript runs on the input lpd feeds to the print filter, and Ghostscript sends a bitmap to smbclient.

# 5.5 printcap Generation and Distribution

For larger networks with many printers, getting the correct /etc/printcap to the right machines can take a lot of time. You should automate this task using a master list of printers—from that you can generate files based on host name. The traditional Unix tool for the printcap is a macro-processing language called m4. Practically everyone has their own system, so we might as well describe our own.

In the directory support/printing/printcap on the included CD-ROM, you’ll find a collection of m4 files and a Makefile.

If you run m4 generic-lprng.m4, the output will be a generic LPRng client printcap containing a number of printers. printer-list.m4 defines these printers, but before you examine that file, let’s examine the generic-lprng.m4 file:

```
define(this_host,generic-host)dnl
```

This line defines the host that gets the printcap. This particular definition can be used by a number of hosts, none of which have a local printer attached. We use the name generic-host, which doesn’t match any host name on the network (more on matching host names later).

```
include(common.m4)dnl
include(lprng-printcap.m4)dnl
```

These lines pull in m4 source code from other files. The first one, common.m4, defines some macros common to all kinds of output, such as spool directory prefixes. The second one, lprng-printcap.m4, creates customized output for LPRng.

```
include(printer-list.m4)dnl
```

Finally, m4 reads the printer list and creates the output.

# The printer-list.m4 file

The file printer-list.m4 is a list of printers and descriptions with entries like this:

```
HP4SI(hp160b,HP LaserJet 5Si,hp160b|160b,room 160b Ryerson,
    printerserv.cs.uchicago.edu,
    HP_LaserJet_4Si_300_dpi,hp160b.cs.uchicago.edu)dnl
```