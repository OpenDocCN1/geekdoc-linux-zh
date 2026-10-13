# The Line Printer Server: LPRng

LPRng is an enhanced version of the Berkeley Line Printer Daemon (LPD) lpd and associated lpr applications. It features a wide range of capabilities that include security measures and access to remote printers. Many of the commands are the same as those used by LPD on a standard Unix system. The Linux printer server program is called lpd, the line printer daemon. Printers are installed to run under lpd, which then handles print jobs for them both locally and from remote sources. Though lpd is called the line printer daemon, it is designed to manage any kind of printer, not just line printers. You should think of it as a general-purpose print server capable of handling laser, inkjet, PostScript, and dot-matrix printers. LPRng also features a companion IFHP filter package, which provides hardware-level support for PostScript, PCL, and text printers, among others (see www.astart.com/lprng.html).

The lpd daemon is installed and configured on your Linux system during installation. lpd is run as a standalone process by the lpd startup script in the /etc/rc.d/init.d directory. You can use the service command on this script to start, stop, and restart the daemon:

```
service lpd restart
```

The lpd daemon makes use of two configuration files: lpd.conf and lpd.perms. lpd.conf contains general lpd configuration commands. You use lpd.perms to set up rules with which you can restrict access to the lpd server. Here you can deny access by certain hosts, users, or even networks.

Requests to print documents are performed by print clients such as lpr. When a document is submitted for printing, it becomes a print job that is placed on a queue for the printer it was sent to. While the job is on the queue waiting to print, you can check its status and even remove it from the queue, canceling the job. The lpq command lets you check a print queue, lpc allows you to make changes to it, and lprm is used to remove a print job from a queue.

# LPRng Print Clients

You can use any of several LPRng print clients to manage the printing jobs on your printer or printers, such as Klpq and several command line print clients like lpr and lpq. Klpq is a KDE desktop utility and is labeled the Print Job Administration tool. With Klpq, you can list the print jobs for a printer, remove a print job, and move a print job to the top of the queue. You can also disable printing for a printer. To have the print queue listing automatically updated, you can set an update frequency in the Options menu.

# printcap File

The /etc/printcap file holds entries for each printer connected to your system. A printcap entry holds information, such as the pathname for a printer's spool directory and the device name of the printer port the printer uses. The first field in a printcap entry is a list of possible names for the printer. These are names you can make up yourself, and you can add others if you want. Each name is separated from the next by a | symbol. You use these names to identify the printer when you enter various printer commands or options, such as the -P option. These names are also used for special shell variables, such as the PRINTER variable, used in many initialization scripts.

The fields following the list of names set different fields for your printer. The fields are separated by colons and assigned a value using the = symbol. Three of the more important fields are lp, sd, and if. The lp field is set to the device name the printer uses. The sd field is set to the pathname of the spool directory, and if is set to the particular filter used for this printer. Some fields have Boolean values and simply list the field name with no assignment, which indicates a value of "true." You can find a complete listing of the printcap fields in the printcap Man pages: man printcap. An example of a printcap entry follows:

```
myprinter|myepson:\n:sh:\n:ml=0:\n:mx=0:\
```