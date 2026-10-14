![](bbox=[0.15, 0.12, 0.8, 0.38])

# Figure 12-11 Many print queues can refer to a single physical printer

> The arrangement in Figure 12-11 can also be implemented using multiple instances of a single print queue in CUPS, as described later in this chapter.

# Understanding Print Filters and Drivers

To print different types of documents from Linux applications to a variety of printer devices, Linux uses special programs called print filters, as described previously. A Linux print filter is essentially the same as a printer driver in other operating systems: it converts documents or images into a format that the printer can use.

Each printer uses a page description language to guide what it prints. A page description language is a special set of codes that determine the graphics elements, text font, and everything else about what appears on a printed page. The most widely used page description languages are PostScript and Printer Control Language (PCL). If a printer uses PostScript, for example, everything sent to that printer must be written in the PostScript page description language.

The documents you create in text editors, word processors, spreadsheets, and other Linux programs are not written in PostScript, PCL, or any other page description language. The print filter converts each document that you want to print into instructions using the appropriate page description language for the printer you want to use.

PostScript was developed by Adobe and is widely used by many types of printers. PCL, developed by Hewlett-Packard, is supported by most Hewlett-Packard printers and by many others as well. Many printers support multiple page description languages.

> If you want to see what PostScript looks like, use the cat or less command to view the file /usr/share/doc/HTML/en/kdvi/aboutkdvi.ps on Red Hat Linux or Fedora. Use the command locate .ps to see what other PostScript files are on your system.