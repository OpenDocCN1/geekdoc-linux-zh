# Printing with SUSE Linux
CHAPTER 24

uses the smclient command to send files to a shared printer. You'll need to configure and
install this script if you want to use it to print to the remote printer. For details about
smclient, see its man page.

# Linux Printing Commands

Of course, you don't have to use the yast command to set up your printer. You can edit
/etc/printcap directly, but you should know what you're doing and understand
printcap's format. This file, an ASCII database of your system's local and networked
printers, describes the capabilities of each printer in detail. For full details, see the
printcap man page for commands and the termcap man page for the file's layout.

In fact, you can have multiple entries for each printer, which is helpful if you want to print
different size papers, print color or black-and-white documents, or change printer trays.

SUSE Linux uses the 4.3BSD line printer pooling system. This time-tested system, ported
from the Berkeley Software Distribution's UNIX, has a number of features and associated
programs to support background printing, multiple local and networked printers, and
control of the printers and queued documents.

The main files used in Linux printer spool systems are as follows:

+   - /etc/printcap
- /usr/sbin/lpd
- /usr/sbin/lpc
- /usr/bin/lpr
- /usr/bin/lrm
- /usr/bin/lpq
- /dev/printer (a symbolic link to /var/run/etc/rc.d)

When you first boot SUSE Linux, the shell script lpd (under /etc/rc.d/) starts lpd, the
printer daemon. The lpd daemon is a printer server. When first started, such as an
init script, the daemon reads the /etc/printcap file and runs in the background and
wais for print requests. Print requests are started with the lpr command. For example, the
following command line will print your document to a file in the /var/spool/lpdndirectory:

```
# lpr myfile.txt
```

Other print-spooling commands can help track your request. If you're printing a large
document or a number of smaller files, you can see a list of print jobs running using the
lpq command. For example, to print a number of files at once, use this: 

![](bbox=[0.835, 0.615, 0.963, 0.818])