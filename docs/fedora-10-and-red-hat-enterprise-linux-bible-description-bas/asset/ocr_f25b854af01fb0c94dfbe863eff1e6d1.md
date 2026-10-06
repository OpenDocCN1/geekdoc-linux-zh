# Part IV: Fedora RHEL Network and Server Setup

From the computer at address 10.0.0.5, I typed the same address line shown in Figure 17-4 in my Web browser (substituting the CUPS server's name or IP address for localhost). When prompted, I entered the root user name and password.

+   1. Now, with the Admin screen, you can set up a printer as follows:
2. Click the Add Printer button. The Add Printer screen appears.
3. Type a Name, Location, and Description for the printer and continue.
4. Select the device to which the printer is connected. The printer can be connected locally to a Parallel, SCSI, Serial, or USB port directly on the computer. Alternatively, you can select a network connection type for Apple printers (AppContext/HP JetDirect), Internet Printing Protocol (ipp or ipp), or Window printer (using SAM or SMB).
5. If prompted for further information, you may need to enter the detail for the printer. For example, you may need to enter the baud rate and parity for a serial printer, or you might be asked for the network (Device URL) for an IP or Samba printer.
6. Select the make of the driver (if you don't see the manufacturer of your printer listed, choose PostScript for a Postscript printer or HP for a PCL printer). For the make you choose, you will be able to select a specific model. If options are available for that printer, the Set Printer Options appears.
7. Depending on the printer driver, there may be a few or a lot of options available for your printer. For example, you may be able to choose page size, manual feed, print quality and other features. After you have chosen the settings you want, select Set Printer Options.
8. If the printer was added successfully, the next page will show a link to the description of that printer. Click that link. From the new printer page, you can print a test page or modify the printer configuration.

After you are able to print from CUPS, you can return to the CUPS Web-based administration page and do work with your printers. Here are a few examples:

+   * **Print jobs** — Click Manage Jobs to see what print jobs are currently active from any of the printers configured for this server. Show Completed Jobs to see information about jobs that are already printed.
* **Create a printer class** — Click Add Class; then identify a name, location and description for a printer class. Then, from the list of printers configured on your server, select which one goes into this class and click Add Class.
* **View printers** — You can click Manage Printers and view the printers you have configured. For each printer that you can click Stop Printer (to stop the printer from printing, but still accept print jobs for the queue), Reject Jobs (to not accept any further jobs for the moment), or Print Test Page (to print a page). Those and other actions you can do from the Printers page appears in Figure 17-5.