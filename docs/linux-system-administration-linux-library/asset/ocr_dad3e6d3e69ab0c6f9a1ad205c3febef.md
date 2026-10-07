# The Linux Printing Process 435

When using a non-PostScript printer, then the printing process proceeds as follows: An application (WordPerfect, xfig, Netscape, or whatever) produces a PostScript file. The file is fed into Linux printer queue, which sends the file through Ghostscript. The queue then passes Ghostscript's output to the printer. The result is that you can configure the application as a PostScript printer, even when the printer is really a low-end inkjet that could never understand PostScript.

All Linux distributions ship with Ghostscript, but not with the latest version of the program. Ghostscript is unusual in its licensing. The latest versions are free for noncommutative distribution, but any distribution for money requires negotiation of license terms with the copyright holder, Aladdin. Latest versions of Ghostscript, however, are available under the GNU General Public License (GPL), and can be distributed on commercial Linux CD-ROMs without dealing with onerous licensing issues. In most cases, the older Ghostscript is quite adequate. If you want the latest features, check the Ghostscript Web site; you can download the latest version and use it, so long as you don't include it in any program you distribute.

> **TIP** Unless you understand PostScript natively, or all of your Linux printing will rely upon Ghostscript to handle the printer. Therefore, it's critically important that your printer either be a PostScript printer or supported by Ghostscript. The Linux Printing Support Database (http://www.linuxprinting.org/printer_list.cgi) is a cross-reference database of printer models and their Ghostscript drivers, including comments on how well these drivers work. Consult before buying a printer or if you are having trouble getting a printer to work in Linux.

Ghostscript itself requires very little in the way of configuration. It includes drivers for many different printers, and the program that calls it (such as the print queue or magic filter) specifies what driver to use. In some cases, you may want to add fonts to Ghostscript, it can be done by editing the /usr/share/ghostscript/version/Fontmap file, where version is the Ghostscript version number (5.50 in Red Hat 7.0). Most programs that print with unusual fonts embed them in their output PostScript files, so there's no need to add fonts to Ghostscript explicitly.

# Magic Filters

One critical piece of information the print spooler software finds in the print cap is the magic filter, or print filter, to use with a given printer. A magic filter software receives a file from standard input, performs an action on the file's type, and outputs the result on standard output.

![](bbox=[0.893, 0.578, 0.981, 0.706])