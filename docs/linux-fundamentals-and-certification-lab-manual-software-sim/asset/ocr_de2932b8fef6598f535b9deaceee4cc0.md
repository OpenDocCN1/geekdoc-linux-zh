# PPR

PPR is a Unix/Linux printer spooler designed for PostScript printers. PPR supports PostScript printers connected to parallel ports, serial ports, or various networks including TCP/IP. Its best feature is that it is designed to work with large numbers of printers. PPR is specifically designed to use PostScript files, but it will accept non-PostScript files and convert them to PostScript.

The queue handling provided by PPR supports hold or cancel of submitted jobs. Any administrator can hold, release, cancel, or move a print job to another printer.

PPR is also supported through the PPD-O-Matic PPD generator for Foomatic. The foomatic-rip filter script can be used as a PPR RIP filter or as a PPR interface.

# PDQ

PDQ is a Unix/Linux printer spooler designed for PostScript and non-PostScript printing. It has many queue management features that are of great help to administrators. PDQ can monitor jobs through and after completion, filter out printing of specific file types, and perform other functions.

One of the nice features of PDQ is its GUI interface (Figure 9–11). PDQ provides a very user-friendly interface to its queue manager.

![](bbox=[0.03, 0.45, 0.15, 0.48])

![](bbox=[0.26, 0.45, 0.84, 0.68])

PDQ is also supported through the PPD-O-Matic PPD generator and the companion foomatic-rip filter script. Foomatic-rip provides for not only PostScript files, but also plain text, PDF, images, and others.

PDQ processes the entire job before sending it to the printer. With heavy print loads, this can cause serious delays when printing.

# CUPS

Common Unix Printer System (CUPS) uses IPP/1.1 to provide a complete printing system for Unix/Linux systems. It is free software provided under the terms of the GNU General Public License and the GNU Library Public License.

The CUPS scheduler is a HTTP server application that handles HTTP requests via IPP. It also acts as a Web server (Figure 9–12) for documentation, status, monitoring, and administration.