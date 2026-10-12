your printer. The lpc command is intended for administrators, so it may not be in your default PATH. To start the lpc command, type the following:

```
# /usr/sbin/lpc
lpc> status
Printer Printing Spooling Jobs Server Subserver Redirect Status
hp@localhost enabled disabled 4 none none
lp0@localhost enabled enabled 0 none none
lpc>
```

When the command returns the lpc> prompt, type the word status. This example shows the status of two printers: hp and lp0. The hp printer has four jobs waiting. Although queueing and printing are enabled, they haven't printed because the print queue is not enabled. (The printer may be disabled.) The lp0 printer shows no problems, no print jobs are waiting.

# Displaying Documents with Ghostscript and Acrobat

Red Hat Linux publishing can be very paper-intensive if you send a Groff or LaTeX document to the printer each time you want to make a change to the document's content or formatting. To save paper and time spent running around, you can use some print preview programs to display a document on screen as it will appear on the printed page. The following sections describe the ghostscript command for displaying PostScript files and the Adobe Acrobat reader for displaying Portable Document Format (PDF) files.

# Using the ghostscript and gv commands

To display PostScript or PDF documents in Red Hat Linux, you can use the ghostscript command. The ghostscript command is a fairly crude interface, intended to let you step through documents and interpret them one line at a time. (If the ghostscript command is not installed on your system, you can get it by installing the ghostscript package from CD-1 that comes with this book.)

You can display any .ps or .pdf file you happen to have on your computer. For example, if the vnc-doc package is installed, you could type the following to display a PDF file (otherwise, you could find your own PDF file to try it):

```
$ ghostscript /usr/share/doc/vnc-doc-*/rfbprotoheader.pdf
>>showpage, press <return> to continue<<
```

At the GS> prompt, press Enter (or Return) to go through the file one page at a time. When the file is done, you can type the name of another PostScript or PDF file and page through that file. When you are done, type quit.

The gv command (ghostview) is another, more friendly way of viewing PostScript files. (If the gv command is not installed on your system, you can get it by installing the gv package from CD-2 that comes with this book.)