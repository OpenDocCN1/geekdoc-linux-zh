![](bbox=[0.22, 0.13, 0.62, 0.38])

# FIGURE 17.4

You can select File, Page Setup before printing to set the options available in this dialog box.

# Printing from Linux to Macintosh Printers

The Netatalk package includes three utilities that are useful for printing from a Linux computer to a Macintosh printer. These utilities and their functions are as follows:

+   - pap—This utility sends a print job to a Macintosh printer. Because Macintosh printers are normally PostScript printers, the input should be PostScript. This program is analogous to lpr for printing to Linux or UNIX printers.
+   - psf—This program is a filter that's intended to be used in the if= line of a Linux /etc/printcap file to prepare data to be sent to a Macintosh printer.
+   - papstatus—This program reads the status of a Macintosh printer. It's analogous to the lpq command.

In addition to printing to printers that are shared by Macintoshes, or printers that connect directly to your Ethernet network and use the Macintosh's PAP communications options, you can use these tools to print to printers shared from another Linux or UNIX computer using Netatalk. This feature can be convenient if you're on a Macintosh-dominated network that uses a Linux netatalk printer server if you can't or don't want to configure that printer with native UNIX-style printing.

# Using pap Directly

The general syntax for using pap is

```
pap [-c] -p printer_file
```

The parameters to the pap command include: