+   11. In the drop-down list for each version of Windows, select the appropriate printer driver from the Driver Store object.

+   12. Click Next.

+   13. When prompted that the Printer Agent has been created, click OK.

That's all there is to creating Printer Agents in your tree. Before continuing, you need to understand a couple issues regarding TCP/IP communications between the iPrint Client, the iPrint Manager, and the Printer Agent.

First, data sent between the iPrint Client and the iPrint Manager can be encrypted using IP port 443. You can also use IP port 631 to send data between these two components unencrypted. Unless you have a compelling reason not to, you should always use encrypted communications.

Second, data passing from the Printer Agent and the physical printer is sent using the LPR protocol. LPR doesn't support encryption; therefore, data sent between the Printer Agent on the server and the physical printer hardware is passed in clear text. With this in mind, you should be sure communications between these two components doesn't cross a public network (such as the Internet). The best way to prevent this is to place both components behind the same firewall.

With that said, there's still one more Printer Agent configuration task to be completed. This task is related to the way printers can be added to Windows NT, 2000, and XP workstations. Remember that these operating systems are multiuser systems. Each local user in the system has his or her own profile, Desktop, and My Documents directory (among other things).

> **WARNING** In this context, the term *local user* refers to Windows user accounts, not eDirectory user accounts. The *Administrators* and *Power Users* groups mentioned refer to Windows groups on the local workstation, not to eDirectory groups.

Windows 95, 98, and Me, on the other hand, are not multiuser systems.

> **TIP** Windows Me can be configured as a quasi multiuser system, but its default configuration is a single-user system.

On Windows 9x and Me systems, every user who uses the system sees the same Desktop and the same My Documents folder, and has access to the same installed printers. If an iPrint printer is downloaded and installed on one of these operating systems, it is available to all local users in the system.