
## Part IV Networking

### Printer Driver Options
-   **Levels of Gray** — Choose to use the printer's current levels of gray or have enhanced or standard gray levels turned on.
-   **Resolution** — Select the default printing resolution (such as 300, 600, or 1,200 dots per inch). Higher resolutions result in better quality but take longer to print.
-   **EconoMode** — Either use the printer's current setting or choose a mode where you save toner or one where you have the highest possible quality.
-   **Job Options** — Click on the "Job Options" item to set common default options that will be used for this printer if the application printing the job doesn't already set them. These include Common Options (number of copies, orientation, scale to fit, and pages per side), Image Options (scaling, saturation, hue, and gamma), and Text Options (characters/inch, lines/inch, and margin settings).

> **NOTE** For a description of other driver options, refer to the CUPS Software User Manual (/usr/share/doc/cups/*/*.html) under the "Standard Printer Options" heading.

Click Apply when you are satisfied with the changes you made to the local printer.

### Configuring Remote Printers

To use a printer that is available on your network, you must identify that printer to your CentOS system. Supported remote printer connections include Networked CUPS (IPP) printers, Networked UNIX (LPD) printers, Networked Windows (SMB) printers, Networked Novell (NCP) printers, and JetDirect printers. (Of course, both CUPS and UNIX print servers can be run from Linux systems, as well as other UNIX systems.)

In each case, you need a network connection from your CentOS system that enables you to reach the servers to which those printers are connected. To use a remote printer, of course, requires that someone set up that printer on the remote server computer. See the section "Configuring Print Servers" later in this chapter for information on how to do that in CentOS.

You can use the Printer Configuration window to configure each of the remote printer types:

1.  From the GNOME desktop, select System > Administration > Printing.
2.  Click "New Printer." The New Printer window appears.
3.  Besides the local ports listed (LPT and Serial ports), you can select one of the following types of network printers:
    -   **AppleSocket/HP JetDirect** — For a JetDirect printer
    -   **Internet Printing Protocol (IPP)** — For a CUPS or other IPP printer
    -   **LPD/LPR Host or Printer** — For a UNIX printer
    -   **Windows Printer via Samba** — For a Windows system printer
4.  Continue following the steps in whichever of the following sections as appropriate.

### Adding a Remote CUPS Printer

After choosing to add an IPP CUPS printer from the Select Connection window, you must add the following information to the window that appears:

-   **Host** — The host of the computer to which the printer is attached (or otherwise accessible). This can be an IP address or TCP/IP hostname for the computer. (The TCP/IP name is typically accessible from your /etc/hosts file or through a DNS name server.)
-   **Queue** — The printer name on the remote CUPS print server, which might look something like printers/HP\22C. CUPS supports the concept of print instances, which allows each printer to have several sets of options. So, if the remote CUPS printer is configured this way, you might be able to choose a particular path to a printer, such as hp/300dpi or hp/1200dpi. A slash character separates the print queue name from the printer instance.

I suggest that you fill in the hostname and select “Find Queue,” to find the available IPP printers from that host. After selecting the printer from a list, the Host and Queue information are automatically filled in. Click on the Verify button to make sure that the printer is accessible. Click Forward and complete the rest of the procedure as you would for a local printer.

### Adding a Remote UNIX Printer

After you have selected to add an LPD/LPR (UNIX) host or printer from the Select Connection window, you must add the following information to the window that appears:

-   **Host** — The hostname of the computer to which the printer is attached (or otherwise accessible). This is the IP address or TCP/IP name for the computer (the TCP/IP name is typically accessible from your /etc/hosts file or through a DNS name server). The host computer might be a UNIX or Linux print server running the lpd print daemon. If you know the hostname but not the printer name, type the hostname and select the Probe button. Available LPD printers from the host will appear in a list in the Queue field.
-   **Queue** — The printer name on the remote UNIX computer

Although CUPS is the more popular printing system for Linux and UNIX systems today, some UNIX-like systems still use the Berkeley LPR print spooler system (see REF1.179). Some early Linux systems included LPng print spooling software to provide this same interface for managing print servers (lpd daemon). So, to point to a really old Unix system at your location, you might need to identify a printer there as a UNIX printer. For older clients, CUPS can also act like an LPD print spooler (see the bullet on enabling LPD-style printing in the “Configuring a Shared CUPS Printer” section later in this chapter).

Click Forward and complete the configuration as you would for a local printer.

> **TIP** If the print job is rejected when you send it to test the printer, the print server computer may not have allowed you access to the printer. Ask the remote computer’s administrator of the UNIX printer to add your hostname to the /etc/lpd.perms file. Type `lpq -P printer` to see the status of your print job.

### Adding a Windows (SMB) Printer

Enabling your computer to access an SMB printer (the Windows printing service) involves adding an entry for that printer in the Select Connection window.

> **NOTE** Before you can add an SMB printer queue to Linux, you must first have configured that printer to work on the Windows machine. You must also indicate that the printer can be shared and is accessible to your Linux machine on your LAN.

After you have selected Windows Printer via Samba to the Select Connection window (described previously), you can browse for computers on your network that offer SMB services (file or printing service) by clicking on the Browse button. When the SMB Browser List appears, you can:

-   Select the group (click the arrow next to the group you want).
-   Select the server (click the arrow next to the server you want).
-   Select the printer from the list of available printers shown.

Alternatively, you could identify a server that does not appear on the list of servers. Type a server name and share into the smb:// box at the top of the page. For example, you could type:

```text
smb://MYGROUP/EINSTEIN/hp2100m
```

Next, select the “Authentication required” box to enter a username and password, if that is required to access the shared printer:

-   **Username** — The username is the name required by the SMB server system to give you access to the SMB printer. A username is not necessary if you are authenticating the printer based on share-level, rather than user-level, access control. With share-level access, you can add a password for each shared printer or file system.
-   **Password** — The password associated with the SMB username or the shared resource, depending on the kind of access control being used. Click on the Verify button to check that the username and password are correct.

> **CAUTION** When you enter a username and password for SMB, that information is stored unencrypted in the /etc/cups/printers.conf file. Be sure that the file remains readable only by root.

Click Forward and complete the configuration as you would for a local printer.

If everything is set up properly, you should be able to use the standard lpr command to print the file to the printer. With this example, you could use the following form for printing:

```text
$ cat file1.ps | lpr -P hp2100m
```
