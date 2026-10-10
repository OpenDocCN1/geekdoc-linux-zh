# Introduction to Linux

<http://www.w3.org/> (the World Wide Web Consortium) to include this feature in other applications.

+   * SGML and XML: Free parsers are available for UNIX and Linux. XML is the next generation SGML, it forms the basis for DocBook XML, a document system (this book is written in XML, for instance).

# Printing documentation

The man pages contain pre-formatted troff data which has to be formatted before it can roll out of your printer. Printing is done using the -t option to the man command:

```
man -t command > man_command.ps
```

Then print the PostScript file. If a default print destination is configured for your system/account, you can just issue the command **man -t command** to send the formatted page to the printer directly.

# 8.1.2.2 Previewing formatted files

Anything that you can send to the printer can normally be sent to the screen as well. Depending on the file format, you can use one of these commands:

+   * PostScript files: with the **gv** (GhostView) command.

+   * TeX dvi files: with **xdvi**, with KDe’s **kdvi**.

+   * PDF files: **xpdf**, **kpdf**, **gpdf** or Adobe’s viewer, **acroread**, which is also available for free but is not free software. Adobe’s reader supports PDF 1.6, the others only support PDF versions up to 1.5. The version of a PDF file can be determined using the **file** command.

+   * From within applications, such as Firefox or OpenOffice, you can usually select Print Preview from one of the menus.

# 8.2 The server side

# 8.2.1 General

Until a couple of years ago, the choice for Linux users was simple: everyone ran the same old LPD from BSD’s Net-2 code. Then LPRng became more popular, but nowadays most modern Linux distributions use CUPS <http://www.cups.org/>, the Common UNIX Printing System. CUPS is an implementation of the Internet Printing Protocol (IPP), an HTTP-like RFC standard replacement protocol for the venerable (and clunky) LPD protocol. CUPS is distributed under the GNU Public License. CUPS is also the default print system on MacOS X.