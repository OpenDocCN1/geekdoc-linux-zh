and you might have good reason to, but you're on your own. In this book, we only cover the printing software that comes by default.

You can tell what kind of printing software your system has by looking for the spooler. CUPS has cuspd BSD has lpd, and System V has ipsched, so the command which cuspd lpd lpd lpsched tells you which one you have.

# Print spoolers

Each system has a spooler: a piece of software that receives prints, stores them, prioritizes them, and sends them out sequentially to one or more printers. You'll sometimes see the spooler referred to a print daemon or server.

Some printers (usually high-end models) have their internal spoolers. If telling your printing to discard all the jobs in its queue does not fix a problem right away, consider that there may be jobs stored inside the printer. To discard those as well, you may need to shut off the spooler and restart it.

The lpd (BSD) and lpsched (SysV) spoolers are stand-alone daemons that are specifically designed for printing. Applications on the system either talk to these servers or read and write configuration files in "well known" locations as /var/spool or /etc.

# 2.2 CUPS PRINTING

CUPS servers are also web servers, and CUPS clients are web clients. The clients can be commands such as CUPS versions of lpr or lpq, or they can be applications with their GUIs such as kprinter. The covers they're all apps, even if they're only talking to the CUPS daemon on the local system. CUPS servers can also act as clients of other CUPS servers.

A CUPS server provides a web interface to its full functionality on port 631. For administrators, a web browser is usually the most convenient way to manage the system; just navigate to http://printhost:631. If you need communication with the daemon (and your system offers it) use https://printhost:443 instead. Scripts use discrete commands to control the system, and users will probably access it through a GNOME or KDE interface. These routes are equal.

HTTP is the underlying protocol for all interactions among CUPS servers and their clients. Actually, it's Internet Printing Protocol, a souped-up version of HTTP. Clients submit jobs with the HTTP/IPP POST operation and request status with HTTP/IPP GET. The CUPS configuration files also look suspiciously similar to Apache configuration files.

# Interfaces to the printing system

CUPS is modern enough that most CUPS printing is done from a GUI, and administration is often done through a web browser. As a sysadmin, you (and perhaps some of your hard-core terminal users) may want to use shell-level