# Printing with SuSE Linux
CHAPTER 24

+   - lpr—The (auto)printer name used to print PostScript documents and graphics;
automatically recognizes different types of documents by the extension (such as .ps)

+   - raw—The printer used when raw output and speed are required when printing, such
as straight text documents

These printer definitions are created in /etc/printcap, and each will have its own /var/
spool/lpd directory. The apsilter filter and associated scripts reside in a directory, or
printer queue, under /var/spool/lpd with the assigned names.

After setting up your printer, you can then use the -P option of the lpr command, followed
by the printer's name and the name of the file you'd like to print. For example, to print a
file called myfile.txt, enter the following:

# # lpr -Pip myfile.txt

An even better test of the capabilities of the apsilter system is to print a PostScript
graphic on your printer. For example, if you're using X11, use the g command to load the
file tiger.ps like this:

```
# g /usr/share/ghostscript/5.10/examples/tiger.ps
```

You'll see the graphic shown in Figure 24.7.

# Figure 24.7
The g command
will display Post-\Script graphics
You can send to your
configured printer.

![](bbox=[0.198, 0.548, 0.76, 0.868])

Printing with
SuSE Linux