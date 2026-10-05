
BitTorrent is a handy tool for downloading large static data files such as the Ubuntu installation ISO images. It can replace protocols such as anonymous FTP, where client authentication is not required.

# EXERCISES

- 1. Why would you use HTTP or FTP instead of BitTorrent for downloading large files?
- 2. Which command would you give to perform a complete upgrade?
- 3. Why would you build a package from its source code when a (binary) deb file is available?
- 4. Suggest two advantages that deb files have over source distributions.

# ADVANCED EXERCISES

- 5. When you compile a package yourself, rather than from a deb file, directory hierarchy should you put it in?
- 6. Which steps should you take before performing an upgrade on a mission-critical server?

# 14
# PRINTING WITH CUPS

# IN THIS CHAPTER
- Jumpstart I: Configuring a Local Printer................................ 549
- system-config-printer: Configuring a Printer.......................... 550
- Jumpstart II: Setting Up a Local or Remote Printer Using the CUPS Web Interface....................... 555
- Traditional UNIX Printing............................................... 558
- CUPS on the Command Line............................................... 560
- Printing from Windows.................................................. 561
- Printing to Windows....................................................... 568

# INTRODUCTION

LPD and LPR
Traditionally, UNIX had two printing systems: BSD Printer Daemon (LPD) and System V Line Printer (LPR). Linux adopted those systems first, and both UNIX and Linux have seen modifications and replacements for these systems. CUPS is the default printing system under Ubuntu.

CUPS
CUPS (Common Unix Printing System) is a cross-platform print server built around IPP (Internet Printing Protocol), which is based on HTTP. CUPS provides many printer drivers and can print different types of files, including PostScript. Because it is built on IPP and can be written to, CUPS runs under many operating systems, including Linux and Windows. Other UNIX variants, including Mac OS; recent versions of Windows have the ability to print to IPP. Thus CUPS is an ideal solution for printing in a heterogeneous environment. CUPS provides System V and BSD command-line interfaces and, in addition to IPP, supports LPD/LPR, SMB, and JetDirect (socket) protocols.

IPP
The project (www.pwg.org/ipp) began in 1996, when Novell and several other companies designed a protocol for printing over the Internet. IPP enables users to:
- Determine the capabilities of a printer.
- Submit jobs to a printer.
- Determine the status of a printer.
- Cancel a print job.

IPP is a client/server protocol in which the server side can be a network-capable standalone printer.

Printers and queues
On a modern computing system, when “send a job to a printer,” you actually add the job to the list of jobs waiting their turn to be printed. This list is called a print queue or simply a queue. The phrase configuring (or setting up) a printer is used when configuring a print queue. This chapter uses these phrases interchangeably.

# PREREQUISITES
Install the following packages (most are installed with the Base Ubuntu system):
- cups-common
- cups-bsd (optional; BSD printing commands)
- cups-client (optional; System V printing commands)
- openprinting-ppds (PPD files)
- openprinting-ppds-extra (optional; more PPD files)
- system-config-printer-gnome (optional; graphical printer tool)

# JUMPSTART I: CONFIGURING A LOCAL PRINTER
To add, modify, and remove printers from the local system, you must be a member of the lpadmin group. For more information see the tip on page 550. To use the CUPS web interface, you need an X server and a Web browser.

cups init script
When you install the cups package, the dpkg postinst starts the cupsd daemon. After you configure CUPS, call the cups init script to restart the cupsd daemon:

```
$ sudo service cups restart
```
Restarting Common Printing System: cupsd [ OK ]

# MORE INFORMATION
- Local CUPS Documentation: With the CUPS web interface (page 560), point a local browser at localhost:631/help.
- Web linux-foundation.org/en/Printing: Information on printers and printing under Linux. Hosts a support database with details about many printers, including notes and driver information; also offers forums, articles, and HOWTO document on printing.
- CUPS home page: www.cups.org
- IPP information: www.pwg.org/ipp
- HOWTO: The SMB HOWTO has a section titled "Sharing a Windows Printer with Linux Machines."

# NOTES
- Firewall: A CUPS server normally uses TCP port 631 for IPP connection and port 80 for an LPR/LPD connection. If the CUPS server is running, you need to open one or both of these ports. Use ufw (page 876), open one or both of these ports by adding a rule that allows service for port 631 and/or port 80 from the clients you want to be able to access the server.
- printer: You can set up a virtual PDF printer by installing the cups-pdf package, and you can set up this printer manually.

# JUMPSTART I: CONFIGURING A LOCAL PRINTER
In many cases, when you connect a printer to the local system and turn it on, Ubuntu sets up the printer and briefly displays a Printer added message (Figure 14-1). If you want to modify the new printer's configuration, click Configure on the message or use the Printing window (Figure 14-2, next page), described in the next section. Both techniques display the Printer properties window.

![](img/45ff4cd21497435daa35084a84b95d07_599.png)
Figure 14-1 Printer added message

# system-config-printer: CONFIGURING A PRINTER
**You must be a member of the lpadmin group**

To modify a printer using the Printing window (system-config-printer), you must be a member of the lpadmin group (the first user is a member of this group). See page 597 for instructions on how to add a user to a group.

The Printing window (Figure 14-2) enables you to add, remove, and configure local and remote printers. To display this, select menu: System⇒Administration⇒Run or give the command system-config-printer from a terminal emulator or Run Application window (ALT+F2).

Highlight a printer in the Printing window and select Printer⇒Set as Default from the window menu to specify the highlighted printer as the default printer. If just one printer appears in the Printing window, it is the default printer; you do not have to set it up as such. The tick on the printer in Figure 14-2 indicates the default printer.

# CONFIGURATION SELECTIONS
This section describes the six selections found in the frame at the left side of the Printer Properties window. These selections allow you to configure the printer you chose in the Printing window.
