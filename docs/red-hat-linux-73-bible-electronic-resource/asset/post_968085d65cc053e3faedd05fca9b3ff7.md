
able to print from other Linux computers on your network to your shared printer. You can modify your `lpd.perms` file if you want to restrict access to your printer.

## Configuring a shared NetWare printer

NetWare server functions delivered with Red Hat Linux are offered using the `mars_nwe` package. This package enables you to do file and printer sharing from Red Hat Linux as though the resources being shared were coming from a NetWare server. Although not all NetWare features are offered, the `mars_nwe` package does well with basic NetWare file and printer sharing.

> **CROSS-REFERENCE**: See Chapter 18 for information on setting up the `mars_nwe` package to share NetWare resources. The `mars_nwe` service must be running to share your printer as a NetWare print server.

You can make your Red Hat Linux printers available as NetWare printers by adding entries to the `/etc/nwsserv.conf` file. This file is used for configuring most `mars_nwe` information. Of particular interest for adding printers is the Print Queues section (section 21). Red Hat Linux printers are identified as NetWare print queues by indicating each line as a section 21 entry. Here is an example:

```
21 PSPRINT  SYS:/PRINT/PSPRINT lpr -Ppsprint
```

The number 21 identifies the entry as a NetWare print queue. PSPRINT is the name of the queue. The queue directory is identified as `SYS:/PRINT/PSPRINT`. Note that the queue directory is different from the `lpd` spool directory. Finally, the last part of the entry is the `lpr` command line used to print documents submitted to this print queue.

Assuming you have done your basic NetWare server configuration, as described in Chapter 18, use this procedure to check that you are able to print to the NetWare print server you just set up in Linux:

1.  Restart the `mars_nwe` service to incorporate the changes you just made to `nwsserv.conf`, by typing the following:

    ```
    # /etc/init.d/mars-nwe stop
    # /etc/init.d/mars-nwe start
    ```

2.  Type the `slist` command to make sure that the NetWare server you configured is available:

    ```
    # slist
    Known NetWare File Servers    Network    Node Address
    ---------------------------------------------------------------
    PINE                          7F000001   000000000001
    ```

In this example, the NetWare server name (of the NetWare server running on Linux) is called PINE. Your server name will be different.

3.  Use the nprint command to print to your NetWare print server in Linux. Type the following commands:

    ```
    $ cd /usr/share/printconf/tests
    $ nprint -S PINE -U GUEST -q PSPRINT testpage.asc
    Logging into PINE as GUEST
    Password:
    ```

In the previous example, the NetWare server name is PINE, the user name is GUEST, and the print queue name is PSPRINT. By default, the guest account has no password, so you can just press Enter at the Password prompt.

> **NOTE:** You don't need to change to the `tests` directory in the previous example. I did that because I know that directory contains several test print pages in different formats. The `textpage.asc` is a plain-text file. You can also try printing `testpage.ps` (a PostScript file) or `testpage-a4.ps` (an A4 PostScript page).

## Configuring a shared Samba printer

Your Red Hat Linux printers can be configured as shared SMB printers by using the Samba SWAT (Samba Web Administration Tool) program. To use SWAT, you need to have the Samba package installed and the swat service configured so that SWAT can be opened in your browser window. You also need a TCP/IP connection between you and the client computers that will use your printer.

> **CROSS-REFERENCE:** Chapter 18 describes how to set up Samba and SWAT to be used in your browser.

With SWAT configured, you can open that program by opening Netscape on your local computer and typing the following address in the location box:

```
http://localhost:901/
```

From the main Samba SWAT screen, click the Printers icon. The Printer Parameters page appears. It is possible that your printers are already made available as shared SMB printers. Click the down arrow next to the Choose Printer box. You should see a list of available printers. Those printers from the pop-up list that have an asterisk preceding their name were automatically loaded as shared printers.

To create a new SMB printer, type a name into the Create Printer box and click Create Printer. Then, fill in the information about the printer (the path, security options, printing options, browse options, and miscellaneous options). When you are done, click Commit Changes. To find out how you would set up an SMB printer from Linux, see the section “Adding a Windows (SMB) printer” earlier in this chapter.

Chances are good that if you are configuring an SMB printer on your Red Hat Linux computer, you will want to share it with Windows clients. If SMB is set up properly on your computer, and the client computers can reach you over the network, finding and using your printer should be fairly straightforward.

The first place a client computer should look for your shared SMB printer is in Network Neighborhood (or My Network Places, for Windows 2000). From the Windows 9x desktop, double-click the Network Neighborhood icon. (From Windows 2000, double-click the My Network Places icon.) The name of your host computer (the NetBIOS name, which is probably also your TCP/IP name) should appear on the screen or within a workgroup folder on the screen. Open the icon that represents your computer. The window that opens should show your shared printers and folders.

If your computer’s icon doesn’t appear in Network Neighborhood, try using the Find: Computer window. From Windows 95, choose Start $\rightarrow$ Find $\rightarrow$ Computer. Type your computer’s name into the Named box and click Find Now. If the Find window finds your computer, double-click it. A window displaying the shared printers and folders from your computer appears, as shown in Figure 17-4.

![](img/1744bde8c889adfab3fc911e1687fecf_731_0.png)

After your shared printer appears in the window, the client can configure a pointer to that printer by opening (double-clicking) the printer icon. You should see a message telling you that you have to set up the printer before you can use it. Click Yes to proceed to configure the printer for local use. The Add Printer Wizard appears. Answer the questions on how you intend to use the printer, and add appropriate drivers. When you are done, the printer will appear in your printer window. It can now be selected as the printer for any application program in Windows 9x.

Another way to configure an SMB printer from a Windows operating system is to go to Start $\rightarrow$ Settings $\rightarrow$ Printers. Open the Add Printer icon, and then select Network Printer from the first window. Open the Add Printer icon. Then, follow the instructions to add a printer from the network.

## Summary

Sharing printers is an economical and efficient way to use your organization’s printing resources. A centrally located printer can make it easier to maintain a printer, while still allowing everyone to get his or her printing jobs done.

You configure your printer with the printconf-gui window. Printers configured with this tool can be printed with the lpr or lp commands. A variety of filters make it possible to print to different kinds of printers, as well as to printers that are connected to computers on the network.

The default printing service in Red Hat Linux is LPRng. You can replace that service with the Common UNIX Printing Service (CUPS). Using the alternatives feature you can switch between the two services so that overlapping components can be exchanged in a way that is transparent to people using the print service.

Besides being able to set up your computer as a Red Hat Linux print server, you can also have your computer emulate a NetWare or an SMB (Windows 9x) print server. After your network is configured properly and a local printer is installed, sharing that printer over the network as a UNIX, NetWare, or SMB print server is not very complicated.
