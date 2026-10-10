
## Resolution
Select the default printing resolution (such as 300, 600, or 1,200 dots per inch). Higher resolutions result in better quality, but take longer to print.

## EconoMode
Either use the printer’s current setting or choose a mode where you save toner or one where you have the highest possible quality.

> **NOTE:** For a description of other driver options, refer to the CUPS Software User Manual (`/usr/share/doc/cups-*/sum.html`) under the *Standard Printer Options* heading.

Click Apply when you are satisfied with the changes you made to the local printer.

# Configuring remote printers

To use a printer that is available on your network, you must identify that printer to your Fedora or RHEL system. Supported remote printer connections include Networked CUPS (IPP) printers, Networked UNIX (LPD) printers, Networked Windows (SMB) printers, Networked Novell (NCP) printers, and JetDirect printers. (Of course, both CUPS and UNIX print servers can be run from Linux systems, as well as other UNIX systems.)

In each case, you need a network connection from your Fedora or RHEL system that enables you to reach the servers to which those printers are connected. To use a remote printer, of course, requires that someone set up that printer on the remote server computer. See the section “Configuring Print Servers” later in this chapter for information on how to do that in Fedora and RHEL.

You can use the Printer configuration window to configure each of the remote printer types:

- 1. From the GNOME desktop, select **System → Administration → Printing**.
- 2. Click **New Printer**. The **New Printer** window appears.
- 3. Besides the local ports listed (LPT and Serial ports), you can select one of the following types of network printers:
    - **AppleSocket/HP JetDirect** — For a JetDirect printer.
    - **Internet Printing Protocol (IPP)** — For a CUPS or other IPP printer.
    - **LPD/LPR Host or Printer** — For a UNIX printer.
    - **Windows Printer via SAMBA** — For a Windows system printer.
- 4. Continue following the steps in whichever of the following sections is appropriate.

# Adding a remote CUPS printer

After choosing to add an Internet Printing Protocol (IPP) CUPS printer from the Select Connection window, you must add the following information to the window that appears:

- **Hostname** — The host of the computer to which the printer is attached (or otherwise accessible). This can be an IP address or **TCP/IP** hostname for the computer (the **TCP/IP** name is typically accessible from your `/etc/hosts` file or through a DNS name server).
- **Printername** — The printer name on the remote CUPS print server, which might look something like `printers/HP722C`. CUPS supports the concept of *printer instances*, which allows each printer to have several sets of options. So, if the remote CUPS printer is configured this way, you might be able to choose a particular path to a printer, such as `hp/300dpi` or `hp/1200dpi`. A slash character separates the print queue name from the printer instance.

Complete the rest of the procedure as you would for a local printer.

# Adding a remote UNIX printer

After you have selected to add an LPD/LPR (UNIX) printer from the Select Connection window, you must add the following information to the window that appears:

- **Hostname** — The hostname of the computer to which the printer is attached (or otherwise accessible). This is the IP address or TCP/IP name for the computer (the TCP/IP name is typically accessible from your `/etc/hosts` file or through a DNS name server). The host computer might be a UNIX or Linux print server running the `lpd` print daemon. (If you know the hostname, but not the printer name, type the hostname and select the Probe button. Available LPD printers from the host will appear in a list in the Printername field.)
- **Printername** — The printer name on the remote UNIX computer.

Although CUPS is the more popular printing system for Linux and UNIX systems today, some UNIX-like systems still use the Berkeley LPR print spooler system (see RFC1179). Early Red Hat Linux systems included LPRng print spooling software to provide this same interface for managing print servers (`lpd` daemons). So, to print to an old Red Hat system at your location, you might need to identify a printer there as a UNIX printer. For older clients, CUPS can also act like an LPD print spooler (see the bullet on enabling LPD-style printing in the “Configuring a shared CUPS printer” section later in this chapter).

Complete the configuration as you would for a local printer.

> **TIP:** If the print job is rejected *when you send it* to test the printer, the print server computer may not have allowed you access to the printer. Ask the remote computer's administrator of the UNIX printer to add your host name to the `/etc/lpd.perms` file. (Type `lpr -P` *printer* to see the status of your print job.)

# Adding a Windows (SMB) printer

Enabling your computer to access an SMB printer (the Windows printing service) involves adding an entry for that printer in the Select Connection window.

> **NOTE:** Before you can add an SMB printer queue to Linux, you must first have configured that printer to work on the Windows machine. You must also indicate that the printer can be shared and is accessible to your Linux machine on your LAN.

After you have selected Windows Printer via SAMBA to the Select Connection window (described previously), you are presented with a list of computers on your network that have been detected as offering SMB services (file or printing service). You can:

- Select the group (click the arrow next to the group you want).
- Select the server (click the arrow next the server you want).
- Select the printer from the list of available printers shown.

Alternatively, you could identify a server that does not appear on the list of servers. Type a server name and share into the `smb://` box at the top of the page. For example, you could type:

```
smb://MYGROUP/EINSTEIN/hp2100m
```

> **TIP:** To find a remote printer name on most Windows systems, first go to the Printers folder (Start → Settings → Printers), and double-click the printer being shared. From the printer queue window that appears, choose Printer → Properties, and then select the Sharing tab. The Sharing tab indicates whether the printer is shared and, if so, the name under which it is shared.

Next, enter a user name and password, if that is required to access the shared printer:

- **Username** — The user name is the name required by the SMB server system to give you access to the SMB printer. A user name is not necessary if you are authenticating the printer based on share-level, rather than user-level, access control. With share-level access, you can add a password for each shared printer or file system.
- **Password** — The password associated with the SMB user name or the shared resource, depending on the kind of access control being used. Click the Verify button to check that the Username and Password are correct.

> **CAUTION:** When you enter a User and Password for SMB, that information is stored unencrypted in the `/etc/cups/printers.conf` file. Be sure that the file remains readable only by root.

Complete the configuration as you would for a local printer.

The result is new entries in the `/etc/cups/cupsd.conf` and `printers.conf` files. This `/etc/cups/printers.conf` entry shows the printer entry you just created:

```
<Printer NS1-PS> 
Info HP LaserJet 2100M 
Location HP on ns1 
DeviceURI smb://jjones:mypassword@STREET/NS1/hp 
State Idle
Accepting Yes
Shared Yes
JobSheets none none
QuotaPeriod 0
PageLimit 0
KLimit 0
</Printer>
```

The DeviceURI is the key information. A lot of information is packed into the `DeviceURI` line. It identifies the location as an `smb` object. The user name is `jjones`, with a password of `mypassword`. The workgroup is `STREET`, the server is `NS1`, and the printer queue name is `hp`.

The contents of the `cupsd.conf` file define who you will allow to use this printer.

```
<Location /printers/NS1-PS>
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
AuthType None
</Location>
```

Based on the information just shown, only users from the local host (127.0.0.1) are allowed to use the printer. No authentication is necessary for them to use it.

If everything is set up properly, you should be able to use the standard `lpr` command to print the file to the printer. With this example, you could use the following form for printing:

```
$ cat file.ps | lpr -P NS1-PS
```

> **TIP:** If you are receiving failure messages, make sure that the computer to which you are printing is accessible. For the previous example, you could type `smbclient -L NS1 -U jjones`. Type the password (`mypassword`, in this case). If you get a positive name query response after you enter a password, you should see a list of shared printers and files from that server. Check the names, and try printing again.

# Adding a JetDirect printer

A JetDirect printer (AppSocket/HP JetDirect) is one that is connected directly to your Ethernet network via a JetDirect device. You typically use port 9100 to print to a JetDirect printer, although additional interfaces may use ports 9101, 9102, and so on. To use a JetDirect printer from Fedora or RHEL, enter the following information:

- **Hostname** — Enter the name of the JetDirect printer.
- **Port number** — Enter the port number (typically 9100) to identify the interface to the JetDirect printer.
