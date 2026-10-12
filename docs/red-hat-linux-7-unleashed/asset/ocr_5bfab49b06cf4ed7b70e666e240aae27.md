**FIGURE 19.5**
The **printtool** main dialog box may be used to test local or remote printers.

![](bbox=[0.27, 0.115, 0.69, 0.26])

To set up for printing to an SMB printer, you must have Server Message Block services enabled (through the `smbd` daemon, part of the Samba software package). You must also have the `smbcli` command and associated `smbprint` shell script installed under the `/usr/bin` directory. You must also be connected to a Windows network and have printer sharing enabled under the remote Windows computer.

For example, under Windows 95, navigate to the Network device in the Control Panel (available through the Settings menu item in the Start menu). Click the File and Print Sharing button, select I Want to Be Able to Allow Others to Print to My Printers, and click OK. Click the Identification tab at the top of the Network window, note the name of your computer, and close the window.

After rebooting, open the Printers folder, right-click the printer you would like to share, and select the Sharing menu item. Select Shared As, enter a shared name and a password, and click OK. You need the name and password information when you run printtool. According to printtool, you need the following to set up a LAN printer:

+   * Printer server name
+   * Printer server IP number
+   * Printer name
+   * Printer user
+   * Printer password
+   * Workgroup

This information (which you can also get from the shared printer's Properties menu under Network Neighborhood) is entered in the SMB Printer Entry dialog box that pops up after you select the type of printer you want to set up. You should also select the type of printer through the Select button at the Input Filter field (similar to that shown in Figure 19.4).