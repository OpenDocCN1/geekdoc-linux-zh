printing of multiple documents, the capability to specify local and networked printers, control of the printers, and management of the queued documents waiting in the printer's spool queue.

# ## Using Basic Print Commands

After configuring your printer, you can print from the desktop, using any printer-capable graphical clients. If you do not use the desktop but prefer to use or access your Fedora system via a text-based interface, you can enter a number of print commands from the command line, too. The main CUPS commands used to print and control printing from the command line are as follows:

+   ► **lp**—The line-printer spooling command; used to print documents that use a specific printer
+   ► **lpr**—The line-printer queue display command; used to view the existing list of documents waiting to be printed
+   ► **lpstat**—Displays server and printer status information
+   ► **lprm**—The line-printer queue management command; used to remove print jobs from a printer's queue
+   ► **lpc**—The line-printer control program; used by the root operator to manage print spooling, the lp daemon, and printer activity

These commands offer a subset of the features provided by CUPS, but can be used to start and control printers and print queues from the command line.

You print files (documents or images) by using the **lp** command, along with a designated printer and filename. For example, to print the file mydoc.txt with the printer named lp, use the **lp** command, its **-d** command-line option, and the printer's name, like this:

```
# lp -d lp mydoc.txt
```

# ## Managing Print Jobs

You can also print multiple documents from the command line. For example, to simultaneously print a number of files to the lp printer, use lpr like so:

```
# lp -d lp *.txt
```

This approach uses the wildcard capabilities of the shell to feed the **lpr** command all files in the current directory with a name ending in .txt for printing. Use the **lpq** command to view the printer's queue, as follows:

```
# lpq
lp is ready and printing
Rank   Owner   Job   File(s)         Total Size
active root     7     classes.conf     3072 bytes
```