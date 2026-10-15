# Additional Printer Ports

If you intend to set up a Linux box as a print server, you might find that you want to serve more than one printer from a single computer. Because most printers come with parallel ports, and because most motherboards have only one parallel port, you might need to add one or more parallel ports to your computer. ISA boards to do this are common, and may contain one or two ports. Linux should have no problem using such ports, assuming that you configure the board properly. Where your first parallel port is /dev/lp0, the second is /dev/lp1 and the third is /dev/lp2.

It’s difficult to use more than three parallel ports on a standard Intel-architecture machine. Therefore, you might want to look into using a serial port for further printers, either with a printer that accepts serial input or with a parallel-to-serial adapter. Printing via a serial port is typically slower than via a parallel port, however.

The Universal Serial Bus (USB) is another method of attaching a printer. USB support was added to the Linux kernel with version 2.2.8, but was still quite crude at that time. You can find more information on the state of USB support for Linux at http://peloncho.fis.ucm.es/~inakiy/usbdb-www/. USB is becoming a common interface for printers, especially for inkjets, and in theory you can attach several dozen USB printers to a single computer, so when this technology matures it might be quite useful to Linux users.

Finally, if no other options are available, you can purchase dedicated Ethernet print servers or, for some printers, install an Ethernet board in the printer. These devices make one or more printers directly available on your network. In many cases, using such a server obviates the need for using Linux as a print server. If you want to use Ghostscript in Linux to convert PostScript into the printer’s native format, however, you still need to configure a printer queue and serve that in the usual way. This sort of configuration increases the traffic on your network because the file goes first to your Linux print server and then to the printer itself.

# Backup Hardware

Murphy’s Law guarantees that at least one of your network’s computers will crash catastrophically, taking its operating system and perhaps user data with it. That’s why you should look into using your Linux box as a backup server, using media such as a tape drive for backups. To do this, however, you need appropriate backup hardware, as described in the following sections.

# Tape

One of the most popular backup media is tape. Tape drives come in four major types of interface: SCSI, EIDE/ATAPI, floppy, and parallel port. For serious server use, I recommend a SCSI tape unit. These drives tend to be the most reliable, and they’re available in some of the