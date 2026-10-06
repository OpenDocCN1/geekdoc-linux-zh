# 708 Part V ♦ Running Servers

The first three examples show the form for local printers (parallel, serial, and scsi). In each case, the other examples are for remote hosts, hostname can be the host's name or IP address. Port numbers or paths identify the locations of each printer on the host.

If you find that you are not able to print because a particular printer driver is not supported in CUPS, you can set up your printer to accept jobs in raw mode. This can work well if you are printing from Windows clients that have the correct printer drivers installed. To enable raw printing in CUPS, uncomment the line in the /etc/cups/mime.types file in:

```
application/octet-stream
```

And uncomment the following line in the /etc/cups/mime.conv file:
application/octet-stream/vnd.cups-raw 0

After that, you can print files as raw data to your printers without using the -raw option to print commands.

![](bbox=[0.128, 0.203, 0.193, 0.255])

# Using Printing Commands

To remain backward compatible with older UNIX and Linux facilities, CUPS supports many of the old commands for working with printing. Command-line printing with CUPS can be performed with the lpr command. Word-processing applications such as StarOffice, OpenOffice, and AbiWord are set up to use this facility for printing.

You can use the Printer Configuration window to define the filters needed for each printer so that the text can be formatted properly. Options to the lpr command can add filters to process the text. Other commands for managing printed documents include lpq (for viewing the contents of print queues), lprrm (removing print jobs from the queue), lpc (for controlling printers).

# Printing with lpr

You can use the lpr command to print documents to both local and remote printers. Document files can be either added to the end of the lpr command or directed to the lpr command using a pipe (|). Here's an example of a simple lpr command:

```
$ lpr doc.ps
```

When you specify a document file with lpr, output is directed to the default printer. As an individual user, you can change the default printer by setting the value of the PRINTER variable. Typically, you add the PRINTER variable to one of your startup files, such as $HOME/.bashrc. Adding the following line to your .bashrc file, for example, sets your default printer to lp3: