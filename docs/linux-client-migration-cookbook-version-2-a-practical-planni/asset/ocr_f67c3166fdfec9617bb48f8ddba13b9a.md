![](bbox=[0.285, 0.095, 0.843, 0.568])

# # Printer

Default Destination: printer1

| printer1 | HP LaserJet Series CUPSPS v1.1 |
| --- | --- |
| Description: Test printer on AD server domain of AD6380 | Location: virtual printer |
| Printer State: idle, accepting jobs. | Device URI: smb://smb3lab260/printer1 |

+   * Print Test Page | Stop Printer | Reject Jobs | Modify Printer
* Configure Printer | Delete Printer

Copyright 1993-2002 Easy Software Products, All Rights Reserved. The Common UNIX Printing System, CUPS, and the CUPS logos are the trademark property of Easy Software Products. All other trademarks are the property of their respective

**Figure 9-10** CUPS Web Interface Manage Printers page with printer1

The screen captures in this section are created using a Red Hat Desktop client connected to an Active Directory domain AD6380 with domain controller smb3lab26.

To test the printer you added using **lpadmin** or the Web interface just print a file to, or use the Print Test Page button on the Web interface.

> **Important:** Using a username and password in the printer creation process will expose your password in the CUPS definition files. It might be best to use a special printer user or make printer shares available for everyone.

Chapter 9. Integration how-tos 229