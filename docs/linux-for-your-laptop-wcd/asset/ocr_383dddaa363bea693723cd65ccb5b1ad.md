# ### Printing with Linux

Most Red Hat–based Linux distributions use the Berkeley Software Distribution (BSD) printer spooling system. Others, such as Caldera’s OpenLinux and SuSE Linux, might use an improved hybrid system named LPing. These print-spooler systems work through the lp d daemon, which runs in the background, waiting for print jobs to appear in a selected directory, such as /var/spool/lpd/nameofprinter. _nameofprinter_ is the printer you define when you create a printer for Linux (see the next section).

# ## Alternative Printing with LPing

LPing is a new and enhanced print spooling system available for Red Hat–based Linux distributions. LPing is also used by other distributions, such as Caldera’s OpenLinux and SuSE Linux. This system is transparently compatible with BSD’s lp d but offers enhanced security features and better controls for managing large printer installations on big networks. LPing is compatible with Red Hat’s print filter system. For more information, see the LPing URL under “Resource Information” at the end of this chapter.

When a document appears in the printer’s spool directory, lp d spawns a copy of itself to take care of printing the document according to the printer’s specifications, contained in the printer’s entry in the Linux printer capabilities database, /etc/printcap. The main daemon is used to control print queuing, ordering of print jobs, and your system’s printers.

Many, if not most, Linux applications output print documents and graphics as text documents in the PostScript language. These PostScript documents are then automatically sent or _filtered_ through the Ghostscript interpreter, _gs_, and then translated to HPCL for output to your printer, according to a specified filter entry in the printer’s /etc/printcap entry.

# ### Creating a Printer

To create a printer for Linux, you need to create a proper entry in /etc/printcap. A single printer may have multiple entries and different names in /etc/printcap. This way, you can define the same printer as a color printer, gray-scale printer, or black-and-white-only printer. Although you can manually edit /etc/printcap (as root) with a text editor, most mobile Linux users prefer to use a software tool with a