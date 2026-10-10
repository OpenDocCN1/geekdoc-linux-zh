+   3. Type a Name, Location, and Description for the printer and click Continue.

+   4. Select the device to which the printer is connected. The printer can be connected locally to a Parallel, SCSI, Serial, or USB port directly on the computer. Alternatively, you can select a network connection type for Apple or HP printers (AppSocket/HP JetDirect), Internet Printing Protocol (https or ipp), or Windows printer (using Samba or SMB).

+   5. If prompted for further information, you may need to further describe the connection to the printer. For example, you may need to enter the baud rate and parity for a serial port or you might be asked for the network address (Device URI) for an IPP or Samba printer.

+   6. Select the make of the print driver (if you don’t see the manufacturer of your printer listed, choose PostScript for a PostScript printer or HP for a PCL printer). For the make you choose, you will be able to select a specific model. If options are available for that printer, the Set Printer Options screen appears.

+   7. Depending on the printer driver, there may be a few or a lot of options available for your printer. For example, you may be able to choose page size, manual feed, print quality and other features. After you have chosen the settings you want, select Set Printer Options.

+   8. If the printer was added successfully, the next page you see should show a link to the description of that printer. Click that link. From the new printer page, you can print a test page or modify the printer configuration.

After you are able to print from CUPS, you can return to the CUPS Web-based administration page and do further work with your printers. Here are a few examples:

+   *   **List print jobs** — Click Manage Jobs to see what print jobs are currently active from any of the printers configured for this server. Click Show Completed Jobs to see information about jobs that are already printed.

+   *   **Create a printer class** — Click Add Class; then identify a name, location and description for a printer class. Then, from the list of printers configured on your server, select which ones will go into this class and click Add Class.

+   *   **View printers** — You can click Manage Printers and view the printers you have configured. Click on a printer to control that one. You can click Pause Printer (to stop the printer from printing, but still accept print jobs for the queue), Reject Jobs (to not accept any further print jobs for the moment), or Print Test Page (to print a page). Those and other actions you can do from the Printers page appears in Figure 16-5 in the maintenance drop list.