# SUSE System Administration
Part III

To create a local printer entry to print on a remote printer via Samba, start YaST, select System Administration, then Network Configuration. Scroll down to the Connect to Printer via YaST's menu and press Enter. You'll see the dialog shown in Figure 24.16.

FIGURE 24.16
Setting up be to print to a remote printer via Samba services requires several important configuration parameters.

![](bbox=[0.323, 0.226, 0.818, 0.443])

This dialog is used to configure an /etc/printcap entry for the remote printer. You'll need to specify the use of color, printer type, printer name, paper format, resolution, of the remote server, name of the printer service, and the username and password for the remote printer.

This information is entered in the dialog box. When finished, press the Install button to create the entry.

> Note
Check Chapter 16, "Samba," for information on setting up other services through Server Message Block (SMB) Windows-based networks. Need more detailed instructions on how to print from Linux to a printer on a Windows 95/98/NT system or to print to a Linux printer from Windows 5? Browse to: http://sdb.suse.de/sdb/en/html/fehr_druck_1.html for information on configuring and troubleshooting printing with SuSE Linux. You'll also find the latest information about Samba at http://samba.anu.edu.au/samba.

Before you can print to your SMB printer, you should have an active network connection. You can use the smbprint command, part of Arthur Tridgill's collection of programs in the Samba software package, to print to a LAN printer. The smbprint command is a shell script, found under the /usr/doc/packages/samba/examples/printing directory, that