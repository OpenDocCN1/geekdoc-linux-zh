network printing protocols, such as the Internet Printing Protocol (IPP) or the Microsoft Server Message Block (SMB) protocol.

Aside from the CUPS web interface, there are a few command-line tools you can use for interacting with the print queues:

+   - 1pc: Start, stop, or pause the print queue.
+   - 1pq: Display the print queue status, along with any print jobs waiting in the queue.
+   - 1pr: Submit a new print job to a print queue.
+   - 1prm: Remove a specific print job from the print queue.

If you're working from the command line, you can check the status of any print queue as well as submit print jobs. For each of the commands, to specify the printer use the -P command-line option along with the printer name, as shown in Listing 23.10.

# **Listing 23.10:** Printing from the command line in Linux

```
```
$ lpq -P EPSON_ET_3750_Series
EPSON_ET_3750_Series is ready
no entries

$ lpr -P EPSON_ET_3750_Series test.txt
$ lpq -P EPSON_ET_3750_Series
EPSON_ET_3750_Series is ready and printing
Rank  Owner Job  File(s)          Total Size
active rich  1    test.txt         1024 bytes
$```
```

The first line in Listing 23.10 uses the lpq command to check the status of the print queue, which shows that the printer is ready to accept new jobs and doesn't currently have any jobs in the print queue. The lpr command submits a new print job to print a file. After the new print job is submitted, the lpq command shows that the printer is currently printing and shows the print job that's being printed.

> Red Hat-based systems use the Automatic Bug Reporting Tool (abrt) to create a report if any kernel-level hardware errors are detected. Red Hat Linux customers can send the report to tech support to help troubleshoot the hardware issue.

# Using Hot-Pluggable Devices

Computer hardware is generally categorized into two types:

+   - Cold-pluggable devices
+   - Hot-pluggable devices