5. To modify the configuration file you must be authenticated as an Ubuntu user with administrative privileges. Enter the userID and password for an administrative account on the Ubuntu server. A login dialog box appears (shown in Figure 22-8) to allow you to log in with your Ubuntu administrative user account.

![](bbox=[0.18, 0.28, 0.92, 0.68])

Figure 22-8: The CUPS admin login dialog box.

6. The CUPS window confirms the new printer has been added.

After you’ve added the new printer, you can view the printer status and manage the printer by selecting the Printers tab at the top of the CUPS main page. Each printer configured on the CUPS server appears with a series of buttons that allow you to control the printer operation, as shown in Figure 22-9.

From this interface you can print a test page, stop the printer, remove jobs from the print queue, and delete the printer.

After you’ve added the new printer via the CUPS web interface, it’ll automatically become available on the Samba server. If you set the browseable setting for printers to yes in your Samba smb.conf configuration file, you can browse to connect to the printer from your Windows workstations.