```
```
Encryption Required
Order allow,deny
Allow localhost
Allow 10.0.0.5
</Location>

<Location /admin/conf>
AuthType Basic
Require user @SYSTEM
Order allow,deny
Allow localhost
Allow 10.0.0.5
</Location>
```
```

From the computer at address 10.0.0.5, I typed the same address line shown in Figure 16-3 in my Web browser (substituting the CUPS server's name or IP address for the local host). When prompted, I entered the root username and password.

Now, with the Admin screen displayed, you can set up a printer as follows:

+   1. Click on the “Add Printer” button. The Add New Printer screen appears.
+   2. Type a Name, Location, and Description for the printer and click Continue.
+   3. Select the device to which the printer is connected. The printer can be connected locally to a Parallel, SCSI, Serial, or USB port directly on the computer. Alternatively, you can select a network connection type for CUPS (e.g., AppSocket/HP JetDirect), Internet Printing Protocol (HTTP or IPP), or Windows printer (using SAMBA or SMB).
+   4. If prompted for further information, you may need to further describe the connection to the printer. For example, you may need to enter the baud rate and parity for a serial port, or you might be asked for the network address (Device URI) for an IPP or Samba printer.
+   5. Select the make of the printer driver. (If you don’t see the manufacturer of your printer listed, choose PostScript for a PostScript printer or HP for a PCL printer.) For the make you choose, you will be able to select a specific model. If options are available for that printer, the Set Printer Options screen appears.
+   6. Depending on the printer driver, there may be a few or a lot of options available for your printer. For example, you may be able to choose page size, manual feed, print quality, and other features. After you have chosen the settings you want, select “Set Printer Options.”
+   7. If the printer was added successfully, the next page you see should show a link to the description of that printer. Click that link. From the new printer page, you can print a test page or modify the printer configuration.

After you are able to print from CUPS, you can return to the CUPS Web-based administration page and do further work with your printers. Here are a few examples:

■ **List Print Jobs** — Click “Manage Jobs” to see what print jobs are currently active from any of the printers configured for this server. Click “Show Completed Jobs” to see information about jobs that are already printed.