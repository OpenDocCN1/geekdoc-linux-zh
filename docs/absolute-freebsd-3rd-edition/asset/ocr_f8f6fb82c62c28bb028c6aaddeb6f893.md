printing situations are printers directly attached to a computer via a USB port and printers attached to a network print server.

If you have a printer attached directly to your FreeBSD machine, such as by a USB cable, I suggest using the *Common Unix Printing System (CUPS)*. This suite of software manages many popular consumer-grade and commercial printers, from lowly inkjets to web-scale laser printers. I'm not going into any detail about CUPS, as it's complicated and varies by printer model. Learn more about CUPS at `http://www.cups.org/`. Many brands of printers have special setup programs in CUPS, such as HP's `hp-setup`. If your printer supports a network connection, though, try to avoid CUPS and use network printing instead.

Accessing a remote print server or network printer via the *Line Printer Spooler Daemon (LPD)* is simple in comparison. LPD takes in PostScript and produces printouts. Most office print servers run LPD. The `lpd(8)` daemon manages LPD. Most modern networked printers also support LPD and can act as their own print server.

Test for LPD support by connecting to TCP port 515; if you get a connection, the device speaks LPD.

```
```
# nc -v color-printer 515
Connection to color-printer 515 port [tcp/printer] succeeded!
```
```

This device supports LPD. We can send print jobs to it by configuring `/etc/printcap`.

# /etc/printcap

Every printer your system knows about needs an entry in `/etc/printcap`, the printer capability database. This file is, by modern standards, in a rather obscure format and will look very unfamiliar to anyone who hasn't previously worked with termcap(5). Fortunately, to access a print server you don't need to understand printcap(5); you just need to use the following template.

To connect to a printer on a print server, you must have the print server's hostname or IP address and its name for the printer you want to