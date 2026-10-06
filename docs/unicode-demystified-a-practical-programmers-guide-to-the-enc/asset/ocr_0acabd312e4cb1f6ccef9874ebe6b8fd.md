![](bbox=[0.305, 0.0565, 0.795, 0.29])

# Figure 17-8 The CUPS Printer page

You can use the CUPS interface to set up and maintain printers while still using all the standard lpr commands followed by :cups.

+   - lpr.cups Sends a job to the printer
- lpq.cups Displays the print queue
- lprm.cups Removes a job from the print queue

Refer to lpr on page 1232 for information about the corresponding lpr commands.

# Manually Adding a Local Printer

To add a local printer manually, you must perform these steps while you are working as root:

+   - Name the printer.
- Create a printcap entry.
- Create a spool directory.
- Turn on the print queue (spooler).
- Start or restart the lpd daemon.

The following simple entry in /etc/printcap starts with the name of the printer (fox), followed by capabilities that you can set to a value. Each capability must be separated from the next with a colon; for clarity, the example uses two colons between the last entry on one physical line and the first on the next. The printcap entry must appear on one logical line: Each line in the example ends with a backslash that quotes the following NEWLINE.