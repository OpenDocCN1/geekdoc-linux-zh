
Next, select the “set authentication details now” check box, if authentication is required to access the shared printer, and enter the following details:

- **Username** — The user name is the name required by the SMB server system to give you access to the SMB printer. A user name is not necessary if you are authenticating the printer based on share-level, rather than user-level, access control. With share-level access, you can add a password for each shared printer or file system.
- **Password** — The password associated with the SMB user name or the shared resource, depending on the kind of access control being used. Click the *Verify* button to check that the Username and Password are correct.

> **CAUTION:** When you enter a User and Password for SMB, that information is stored unencrypted in the `/etc/cups/printers.conf` file. Be sure that the file remains readable only by root.

You can also leave the default choice to prompt the user for the authentication details as needed.

Click *Forward* and complete the configuration as you would for a local printer.

If everything is set up properly, you should be able to use the standard `lpr` command to print the file to the printer. With this example, you could use the following form for printing:

```
$ cat file1.ps | lpr -P hp2100m
```

> **TIP:** If you are receiving failure messages, make sure that the computer to which you are printing is accessible. For the previous example, you could type `smbclient -L NS1-U ijones`. Type the password (my9passwd, in this case). If you get a positive name query response after you enter a password, you should see a list of shared printers and files from that server. Check the names, and try printing again.

### Adding a JetDirect printer

A JetDirect printer (AppSocket/HP JetDirect) is one that is connected directly to your Ethernet network via a JetDirect device. You typically use port 9100 to print to a JetDirect printer, although additional interfaces may use ports 9101, 9102, and so on. To use a JetDirect printer from Fedora, enter the following information:

- **Host** — Enter the name of the JetDirect printer.
- **Port number** — Enter the port number (typically 9100) to identify the interface to the JetDirect printer.

## Using Web-based CUPS administration

The Printer Configuration window effectively hides the underlying CUPS facility. There may be times, however, when you want to work directly with the tools and configuration files that come with CUPS. The following sections describe how to use some special CUPS features.

> CAUTION: Plain-text configuration files are at the base of the CUPS printing facility. When different tools, such as the CUPS Web-based interface and Printer Configuration window, manipulate the same config files, those files can become unusable by the other tools. When possible, you should use system-config-printer (Printer Configuration window) to work with printers in Fedora. You will see warnings to this effect if you start to use the CUPS interface.

Although the preferred way to configure CUPS printing in Fedora is with the Printer configuration window, CUPS offers its own Web-based administrative tool.

If CUPS is already running on your computer, you can immediately use CUPS Web-based administration from your Web browser. If CUPS is not running yet, refer to the following section describing the `cupsd` daemon for information on starting it.

CUPS listens on port 631 to provide access to the CUPS Web-based administrative interface. On the local computer, type the following into your Web browser’s location box:

```
http://localhost:631/admin
```

A screen similar to the one shown in Figure 16-4 appears.

![](img/c78bdcb5b7842a0d73dcc98921f872a2_689_0.png)

Figure 16-4: CUPS enables Web-based administration via port 631.

By default, Web-based CUPS administration is available only from the localhost. To access Web-based CUPS administration from another computer, you must change the /admin section in the /etc/cups/cupsd.conf file. As recommended in the text of this file, you should limit access to CUPS administration from the Web. Also keep in mind that passwords are passed as clear text, so someone sniffing your network could see your password. Consider accessing this service through an SSH tunnel if you want to do CUPS administration over an insecure network.

In the following example, I tell CUPS to listen on its LAN interface for outside connections (in this example, the IP address of eth0 is 10.0.0.20). I changed BrowseAllow to all. I then added Allow lines to allow access from a host from IP address 10.0.0.5 for the root of the server(/), /admin, and /admin/conf.

```
Listen 10.0.0.20
BrowseAllow all

<Location />
Order allow,deny
Allow @LOCAL
Allow 10.0.0.5
</Location>

<Location /admin>
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

From the computer at address 10.0.0.5, I typed the same address line shown in Figure 16-4 in my Web browser (substituting the CUPS server's name or IP address for localhost). When prompted, I entered the root user name and password. Now, with the Admin screen displayed, you can set up a printer as follows:

1. Click the Add Printer button. The Add New Printer screen appears.
2. Select the type of printer, local or network, as well as the specific type of local or network printer.
3. Type a Name, Location, and Description for the printer and click Continue.
4. Select the device to which the printer is connected. The printer can be connected locally to a Parallel, SCSI, Serial, or USB port directly on the computer. Alternatively, you can select a network connection type for Apple or HP printers (AppSocket/HP JetDirect), Internet Printing Protocol (https or ipp), or Windows printer (using Samba or SMB).
5. If prompted for further information, you may need to further describe the connection to the printer. For example, you may need to enter the baud rate and parity for a serial port or you might be asked for the network address (Device URI) for an IPP or Samba printer.
6. Select the make of the print driver (if you don’t see the manufacturer of your printer listed, choose PostScript for a PostScript printer or HP for a PCL printer). For the make you choose, you will be able to select a specific model. If options are available for that printer, the Set Printer Options screen appears.
7. Depending on the printer driver, there may be a few or a lot of options available for your printer. For example, you may be able to choose page size, manual feed, print quality and other features. After you have chosen the settings you want, select Set Printer Options.
8. If the printer was added successfully, the next page you see should show a link to the description of that printer. Click that link. From the new printer page, you can print a test page or modify the printer configuration.

After you are able to print from CUPS, you can return to the CUPS Web-based administration page and do further work with your printers. Here are a few examples:

- **List print jobs** — Click Manage Jobs to see what print jobs are currently active from any of the printers configured for this server. Click Show Completed Jobs to see information about jobs that are already printed.
- **Create a printer class** — Click Add Class; then identify a name, location and description for a printer class. Then, from the list of printers configured on your server, select which ones will go into this class and click Add Class.
- **View printers** — You can click Manage Printers and view the printers you have configured. Click on a printer to control that one. You can click Pause Printer (to stop the printer from printing, but still accept print jobs for the queue), Reject Jobs (to not accept any further print jobs for the moment), or Print Test Page (to print a page). Those and other actions you can do from the Printers page appears in Figure 16-5 in the maintenance drop list.
