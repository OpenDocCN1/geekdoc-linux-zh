printers. Other information in the output includes /etc/printcap definitions, diagnostics regarding each printer's spool directory (under /var/spool/lpd/printername), and the permissions of all print filters.

You print files (documents or images) using the lpr command, along with a designated printer and filename. For example, to print the file mydoc.txt using the printer named 1pr, use the lpr command and its -P command-line option and the printer's name, like this:

```
# 1pr -Plp mydoc.txt
```

The lpr command uses a default printer name determined by (in order of priority): the command line, the PRINTER, LPDEST, NPRINTER, or NGPRINTER environment variables, the first entry in your system's /etc/printcap, or the default printer specified in /etc/lpd.conf.

# Manage Print Jobs

You can also print multiple documents from the command line. For example, to print a number of files at once to the lpr printer like so:

```
# 1pr -Plp *.txt
```

This approach uses the wildcard capabilities of the shell to feed the lpr command all files in the current directory with a name ending in .txt for printing. Use the lpq command to view the printer's queue like:

```
# 1lpq
Printer: 1lp@thinkpad
Queue: 1 printable job
Server: pid 9531 active
Unsporer: pid 9532 active
Status: IF filter 'wrapper' filter msg - \
<</HW/Resolution[300 300]>>setageddevice at 12:29:03.569
```

| Rank Owner/ID Class Job Files Size Time |
| 1 root@thinkpad+530 A 530 CHANGES 251703 10:29:02 |

The lprq reports on the printer, number of jobs, the lpd PID, information from the filter (such as dots per inch, or dpi), and a formatted list of print jobs—each with a job number (530 in this example), owner, name of file, size, and the time the job started. Job numbers are used by LPRng to keep track of documents waiting to be printed, and each job will have a unique job number. To stop the print job in this example, use the lpr-rm command, followed by the job number, like this: