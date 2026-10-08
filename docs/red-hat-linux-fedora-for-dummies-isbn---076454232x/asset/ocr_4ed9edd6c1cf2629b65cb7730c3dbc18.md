The configuration utility sends a test page to the printer. If the page prints okay, click the Yes button in the Information dialog box.

**10. Close the configuration utility by choosing Action → Quit.**

![](bbox=[0.13, 0.21, 0.64, 0.42])

The printer configuration droid allows you to go back and edit or delete a printer configuration.

# Configuring a Linux client to print through the print server

Samba makes sharing a printer to Linux, Unix, and Windows computers easy because all those types can speak the Session Message Block (SMB) protocol; SMB is a Windows way of spreading the wealth (yeah, right).

Samba comes configured to automatically export the default Linux printer. Half the battle is won! You don't have to configure the server; you only have to configure each client.

Configure a Linux client to print through the Linux print server by repeating the steps in the preceding section. The steps are the same except that you select the Windows queue type rather than Local. You select the Windows type because the client is sending its jobs to the server via Samba; Samba makes the server act like it's a Windows queue type.

You can print a PostScript test page to test your printer configuration by choosing Test → US Letter PostScript Test Page in the Printer Configuration utility.