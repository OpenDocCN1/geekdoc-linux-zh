# Hour 18. Printing in the Unix Environment

# Goals for This Hour

In this hour, you will learn

+   - How to find local printers with `lpstat`
+   - About CUPS
+   - How to send a print job to a printer with `lpr` or `lp`
+   - About formatting print jobs with `pr` and `col`
+   - How to work with the print queue by using `lpq` and `lprm`
+   - About working with cloud-based printing services

Printing is one of the greatest shortcomings of Unix. Generating printouts is a sufficiently common task that it should be fairly easy to accomplish. However, in this one area of Unix, continual conflict exists between the System V and BSD groups, to the detriment of all.

This hour focuses on some of the most common Unix commands for working with printers. It is a primer on learning what printers are hooked up to your system, how to send output to a printer, how to check that your print requests are in the queue for printing, and how to remove your print requests from the queue if you decide not to print.

Various techniques can minimize the complexity of printing in Unix. The best one is to create an alias called `print` that has all the default configuration information you want. If you define `PRINTER` as an environment variable (probably in your `.login` file or similar), most of the Unix print utilities will default to that device, for example, when searching print queues for jobs. The queue, or list, is where all print jobs are placed for processing by the specific printer.

# Note

The differing “philosophies” of BSD and System V have caused problems in the area of printing. In a nutshell, because Unix systems are almost always networked (that is, hooked together with high-speed data-communications lines), the most valuable feature of a printing tool would be allowing the user to choose to print on any of the many printers attached to the network. For this to work, each machine with an attached printer must be listening for requests from other machines. The root of the BSD versus System V problem is that the two listen for different requests. A System V machine typically can’t send a print job to a printer attached to a BSD machine and vice versa. And we haven’t even started talking about Linux systems, Windows servers, and Mac systems yet. It’s, well, complicated.