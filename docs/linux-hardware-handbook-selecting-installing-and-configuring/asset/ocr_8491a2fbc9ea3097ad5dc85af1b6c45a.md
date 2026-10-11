# Note

If you're using a Linux computer exclusively as a print server for Windows computers, you might be able to serve a printer that can't otherwise be used from Linux. You must load the printer's native drivers on the Windows client computers and export the printer as a “raw” queue—that is, without filtering the print jobs through Ghostscript. This procedure works for Windows-only printers that don't have any unusual timing requirements, but it doesn't work with most host-based printers.

# Using Printers in Linux

In most OSs, printer drivers serve as an interface between an application and a printer. Communication can go both ways in this arrangement. For instance, a printer driver can inform an application that the printer supports wide margins. This isn't the case in Linux. In Linux, applications produce PostScript output, usually without features that tailor the output for specific printers. If your printer supports wide margins, you must find some way to convince your application of this fact.

Because most printers sold for the x86 market are not PostScript printers, Linux includes a utility, Ghostscript, that converts between PostScript and an assortment of other printer languages. In effect, Ghostscript takes over many of the roles of a printer driver in other OSs, although Ghostscript doesn't communicate back to the application what a printer's capabilities are.

In addition to Ghostscript, Linux computers implement a printer queue system. This queue holds the output from an application until the printer becomes ready. The queue then feeds the job through Ghostscript or some other program, if necessary, and passes the result on to the printer.

# Understanding Linux Printer Queues

Most Linux installations use a printer queue system known as lpr, named after one of its component programs. To print using this system, a user or program calls lpr and passes to it the name of a file to print. Optionally, it also passes various parameters, such as the name of a printer, for instance,

```
lpr -Pepson example.ps
```

This command prints the file example.ps to the printer queue called epson. The lpr printing system includes a second program, known as lpd. This program is a daemon, which processes files in the queue according to rules outlined in the /etc/printcap configuration file, which I