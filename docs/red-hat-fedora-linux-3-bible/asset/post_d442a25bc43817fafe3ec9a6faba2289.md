
requires that someone set up that printer on the remote server computer. See the section “Configuring Print Servers” later in this chapter for information on how to do that in Fedora Linux.

You can use the Printer configuration window to configure each of the remote printer types:

1. From the Red Hat menu, select System Settings → Printing.
2. Click New. The Add a New Printer window appears.
3. Click Forward. The Queue Name window appears.
4. Type a short name and description of the printer and click Forward.
5. Click the Select a Queue Type box and select one of the following:
   - Networked CUPS (IPP)
   - Networked UNIX (LPD)
   - Networked Windows (SMB)
   - Networked Novell (NCP)
   - Networked JetDirect
   Click Forward.
6. Next, continue following the steps in whichever of the following sections is appropriate.

## Adding a remote CUPS printer

After choosing to add a CUPS printer from the Printer configuration window, you must add the following information to the window that appears:

- **Server** — The host of the computer to which the printer is attached (or otherwise accessible). This can be an IP address or TCP/IP host name for the computer (the TCP/IP name is accessible from your `/etc/hosts` file or through a DNS name server).
- **Path** — The printer name on the remote CUPS print server. CUPS supports the concept of printer instances, which allows each printer to have several sets of options. So, if the remote CUPS printer is configured this way, you might be able to choose a particular path to a printer, such as `hp/300dpi` or `hp/1200dpi`. A slash character separates the print queue name from the printer instance.

Complete the rest of the procedure as you would for a local printer.

## Adding a remote UNIX printer

After you have selected to add a UNIX printer from the Printer configuration window, you must add the following information to the window that appears:

- **Server** — The host name of the computer to which the printer is attached (or otherwise accessible). This is the IP address or TCP/IP name for the computer (the TCP/IP name is accessible from your /etc/hosts file or through a DNS name server. The host computer might be a UNIX or Linux print server running the lpd print daemon.
- **Queue** — The printer name on the remote UNIX computer.

Complete the configuration as you would for a local printer.

> **TIP:** If the print job is rejected when you send it to test the printer, the print server computer may not have allowed you access to the printer. Ask the remote computer's administrator or the UNIX printer to add your host name to the /etc/lpd.permissions file. (Type lpq -P*Printer* to see the status of your print job.)

## Adding a Windows (SMB) printer

Enabling your computer to access an SMB printer (the Windows printing service) involves adding an entry for the printer in the Printer configuration window.

After you have selected to add a Windows printer to the Printer configuration window (described previously), you are presented with a list of computers on your network that have been detected as offering SMB services (file and/or printing service). You can:

- Select the server (click the arrow next to its name so that it points down).
- Select the printer from the list of available printers shown.
- When prompted, fill in the user name and password needed to access the SMB printer. (You may also fill in the Workgroup information, if required.) Click OK to continue.

Alternatively, you could identify a server that does not appear on the list of servers. Click the Specify button and input the following information in the appropriate fields:

- **Workgroup** — The workgroup name assigned to the Windows server. Filling in the workgroup name isn't necessary in all cases.

> **TIP:** If you are printing to a Windows 95/98 printer, you can find the Workgroup and Hostname of Print Server entries in the Network window. From Windows 95/98, choose **Start** -> **Settings** -> **Control Panel**. Open the Network window, and then click its Identification tab, which will display the computer name and workgroup. If there is no Identification tab, you may need to install the Client for Microsoft Network client in the Network window.

- **Server** — The server name is the NetBIOS name or IP address for the computer, which may or may not be the same as its TCP/IP name. To translate this name into the address needed to reach the SMB host, Samba checks several places where the name may be assigned to an IP address. Samba checks the following (in the order shown) until it finds a match: the local /etc/hosts file, the local /etc/lmhosts file, a WINS server on the network, or responses to broadcasts on each local network interface to resolve the name.
- **Share** — The share name is the name under which the printer is shared with the remote computer. It may be different from the name by which local users of the SMB printer know the printer.

> **TIP:** To find a remote printer name on most Windows systems, first go to the Printers folder (Start → Settings → Printers), and double-click the printer being shared. On the printer queue window that appears, choose **Printer → Properties**, and then select the Sharing tab. The Sharing tab indicates whether the printer is shared and, if so, the name under which it is shared.

- **User** — The user name is the name required by the SMB server system to give you access to the SMB printer. A user name is not necessary if you are authenticating the printer based on share-level, rather than user-level, access control. With share-level access, you can add a password for each shared printer or file system.
- **Password** — The password associated with the SMB user name or the shared resource, depending on the kind of access control being used.

> **CAUTION:** When you enter a User and Password for SMB, that information is stored unencrypted in the /etc/cups/printers.conf file. Be sure that the file remains readable only by root.

Complete the configuration as you would for a local printer.

The result is new entries in the /etc/cups/cupad.conf and printers.conf files. This /etc/cups/printers.conf entry shows the printer entry we just created:

```
<Printer NS1-PS>
Info Created by redhat-Config-Exprinter 0.6.x
DeviceURI smb://jjones:my9passwd@FSTREET/NS1/hp
Location HP on ns1
State Idle
Accepting Yes
JobSheets none none
QuotaPeriod 0
PageLimit 0
KLimit 0
</Printer>
```

The DeviceURI is the key information. A lot of information is packed into the DeviceURI line. It identifies the location as a smb object. The user name is jjones, with a password of my9passwd. The workgroup is FSTREET, the server is NS1, and the printer queue name is hp.

The contents of the cupd.conf file define who you will allow to use this printer.

```
<Location /printers/NS1-PS>
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
AuthType None
</Location>
```

Based on the information just shown, only users from the local host (`127.0.0.1`) are allowed to use the printer. No authentication is necessary for them to use it.

If everything is set up properly, you should be able to use the standard `lpr` command to print the file to the printer. With this example, you could use the following form for printing:

```bash
$ cat file1.ps | lpr -P NS1-PS
```

TIP: If you are receiving failure messages, make sure that the computer to which you are printing is accessible. For the example above, you could type `smbclient -L NS1 -U ljones`. Type the password (my9passwd, in this case). If you get a positive name query response after you enter a password, you should see a list of shared printers and files from that server. Check the names, and try printing again.

## Adding a Novell (NCP) NetWare printer

With this procedure, you set up your Fedora Linux system to use a printer that is connected to (or otherwise managed by) a NetWare file and print server. As with SMB printing, you must gather the information about the server, queue, user, and password.

Select to add a Novell printer (Novell created NetWare) from the Printer configuration window (described previously), and then fill in the following information:

- **Server** — The host name of the computer to which the printer is attached (or otherwise accessible). This is the NetWare Server name for the computer.
- **Queue** — The name of the print queue on the NetWare server.
- **User** — The user name required by the NetWare server system to enable access to the NetWare printer.
- **Password** — The password associated with the user name.

Complete the configuration as you would for a local printer.

## Adding a JetDirect printer

A JetDirect printer is one that is connected directly to your Ethernet network via a JetDirect device. You typically use port 9100 to print to a JetDirect printer, although additional interfaces may use ports 9101, 9102, and so on. To use a JetDirect printer from Fedora, enter the following information:

- **Printer** — Enter the name of the JetDirect printer.
- **Port** — Enter the port number (typically 9100) to identify the interface to the JetDirect printer.
