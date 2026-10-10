you know the hostname, but not the printer name, type the hostname and select the Probe button. Available LPD printers from the host will appear in a list in the Queue field.)

+   * **Queue** — The printer name on the remote UNIX computer.

Although CUPS is the more popular printing system for Linux and UNIX systems today, some UNIX-like systems still use the Berkeley LPR print spooler system (see RFC1179). Early Red Hat Linux systems included LPRng print spooling software to provide this same interface for managing print servers (1.pd daemon). So, to print to a ready old Red Hat system at your location, you might need to identify a printer there as a UNIX printer. For older clients, CUPS can also act like an LPD print spooler (see the bullet on enabling LPD-style printing in the “Configuring a shared CUPS printer” section later in this chapter).

Click Forward and complete the configuration as you would for a local printer.

> **TIP:** If the print job is rejected when you send it to test the printer, the print server computer may not have allowed you access to the printer. Ask the remote computer’s administrator of the UNIX printer to add your hostname to the `/etc/lpd.perms` file. (Type **lqpd -P printer** to see the status of your print job.)

# Adding a Windows (SMB) printer

Enabling your computer to access a Server Message Block (SMB) printer (the Windows printing service) involves adding an entry for that printer in the New Printer window.

> **NOTE:** Before you can add an SMB printer queue to Linux, you must first have configured that printer to work on the Windows machine. You must also indicate that the printer can be shared and is accessible to your Linux machine on your LAN.

After you have selected Windows Printer via SAMBA in the New Printer window (described previously), you can browse for computers on your network that offer SMB services (file or printing service) by clicking the Browse button. When the SMB Browser list appears, you can:

+   - Select the group (click the arrow next to the group you want).
+   - Select the server (click the arrow next the server you want).
+   - Select the printer from the list of available printers shown.

Alternatively, you could identify a server that does not appear on the list of servers. Type a server name and share into the `smb://` box at the top of the page. For example, you could type:

```
smb://MYGROUP/EINSTEIN/pip2100m
```

> **TIP:** To find a remote printer name on most Windows systems, first go to the Printers folder (Start → Settings → Printers), and double-click the printer being shared. From the printer queue window that appears, choose Printer → Properties, and then select the Sharing tab. The Sharing tab indicates whether the printer is shared and, if so, the name under which it is shared.