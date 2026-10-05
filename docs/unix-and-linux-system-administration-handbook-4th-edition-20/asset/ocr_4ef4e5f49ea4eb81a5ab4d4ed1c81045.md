# Chapter 26 Printing

# Printer autfiguration

You can use CUPS without a printer (for example, to convert files to PDF or fax format), but its typical role is to manage real printers. In this section we review the ways in which you can deal with the printers themselves.

In some cases, adding a printer is trivial. CUPS tries to autodet USB printers when they're plugged into the system and figure out what to do with them.

Printer manufacturers typically supply installation software that does most of the setup work for Windows and even Mac OS (which also uses CUPS). However, few vendors explicitly support Linux.

Even if you have to do configuration work, adding a printer is often no more painful than plugging in the hardware, connecting to the CUPS interface at localhost:631/admin, and answering a few questions. KDE and GNOME come with their printer configuration widgets, which you may prefer to the CUPS interface. (We like the CUPS GUI.)

If someone else adds a printer and one or more CUPS servers running on the network know about it, your CUPS server will learn of your existence. You dont have to explicitly add the printer to the local inventory or copy PPDs to your machine.

# Network printer configuration

Network printers—that is, printers whose hardware interface is an Ethernet-need configuration of their own to be proper citizens of the TCP/IP network. In particular, they need to know their own IP addresses and netmasks. That information is usually conveyed in one of two ways.

Modern printers can get this information across the network from a BOOTP or DHCP server, and this method works well in environments that have many printers. See DHCP: Dynamic Host Configuration Protocol on page 469 for more information about DHCP.

Alternatively, you can assign the printer a static IP address from its console, which usually consists of a set of buttons on the printer's front panel and a one-line display. Fumble around the menus until you discover where to set the IP address (If there is a menu option to print the menus, use it and put the printer underneath for future reference.)

A few printers give you access to a virtual console through a serial port. It's a nice idea, but the total amount of work is probably more than suffering through the front-panel interface. The principles are the same.

Once configured, network printers usually have a web console accessible from a browser. However, printers need to have an IP address and be up and running on the network before you can get to them this way, so this interface is unavailable when you might want it most.