
existing peripherals are hard to support Linux, it is probably less expensive to buy new devices that are known to run under Linux.

Information about open source projects that support peripheral extensions can be found on the following Web sites:

- Common UNIX Printing System (CUPS), see 9.7, "How to use network printers in the domain" on page 219,
  http://www.cups.org
- Scanner Access Now Easy (SANE):
  http://www.sane-project.org
- UNIX SmartCard Driver Project:
  http://smartcard.sourceforge.net
- gphoto-2 - Digital camera support:
  http://www.gphoto.org

## 4.6.3 Connectivity options

Now that the Internet is seemingly everywhere and many services are "on demand", connectivity becomes one of the most important features of a client. The Internet was created on UNIX-based servers, and because Linux was created as a UNIX-like operating system for the x86 architecture originally, it should come as no surprise that Linux easily fulfils connectivity requirements.

The majority of Ethernet network cards are supported. Because DSL and Cable modem connections operate over an Ethernet network interface, support in Linux for those devices is also common. For DSL connections, PPP and PPPPoE Protocols are supported. Cable modem connections are easy, too, because they usually provide IP addresses via DHCP.

Wireless network device compatibility is where you will need to be most careful in testing your target client systems and devices. In this situation, we recommend that you choose devices from larger manufacturers; for example, Cisco offers Linux drivers for its wireless network cards. Support for wireless devices has improved significantly, so there should be no problem finding a solution to give your users connectivity.

Supporting dial-up connectivity can be more problematic, especially in the case of winmodems, which are extremely common in notebook computers. These are modems that use software to emulate the hardware components, and therefore, you need special software in order to use it.

For winmodems, some Linux drivers are available for some models. Up-to-date information about this can be found at:

http://linmodems.org

The support of these devices is dependent upon the distribution. Sometimes, it is easier to use an external modem with a supported chipset than to spend a lot of effort to get the internal modem working.

## 4.6.4 Offline mode

In this section, we discuss working in offline mode.

### Offline messaging

There are many full-featured desktop e-mail client available (such as Microsoft Outlook or IBM Lotus Notes) that provide for offline access to a user's e-mail. Frequently when planning a Linux migration for mobile (laptop-based) users, supporting a Linux-based messaging client with offline capabilities will be the single most important design decision in a mobile desktop application migration strategy. There are Linux-based messaging client options that provide for offline access modes. Mozilla Thunderbird supports POP and IMAP protocols. More information about Thunderbird can be found at:

http://www.mozilla.org

Although Thunderbird will support offline messaging modes, it does not provide a way to integrate calendar and scheduling functionality into the messaging client that is provided by systems such as Microsoft Outlook with Microsoft Exchange back-end and IBM Lotus Notes with Domino back-end. For this reason, we choose to demonstrate of Novell's Connector combined with the Novell Evolution e-mail client in Chapter 8, "Client migration scenario" on page 173. Extending the example migration scenario in Chapter 9, "Integration how-tos" on page 195, for the notebook user that you will also have to test and evaluate the offline capabilities of that solution.

### Offline files

Because every user to some extent creates and manages files and folders, follows that the notebook user should be able to access copies of their files in offline mode. However, the primary storage location for these files should be a regularly backed up and highly available server.

For example, Microsoft provides methods for automatic synchronization of files between servers and mobile clients. One of these methods uses the Briefcase, a special folder whose contents are synchronized at specific intervals. A second method was provided with the launch of Windows 2000, where a new function called offline files was implemented. This mechanism is able to synchronize whole folders. While the notebook is offline, the files are fully accessible, and changes are retransmitted automatically after connecting to the network.

In Linux, this kind of server-to-client file synchronization is not built into the operating system itself. Instead, the task of developing and supporting Linux-based file synchronization services between client and server is left to ISVs. For example, Novell offers a solution called iFolder. More information can be found at:

http://www.novell.com/products/ifolder

Another possibility is to use rsync. Because it builds checksums of the files and transfers only the missing parts, rsync is extremely effective over small-bandwidth connections. The Web site for rsync is:

http://samba.org.edu/rsync/

By using rsync, you can develop a client that run on Linux.

## 4.7 Unmigratable applications

This section discusses issues related to applications that cannot be migrated to Linux. We propose alternate ways to support these applications. We assume that the number of migratable applications is small and that a small percentage of users are using these applications. If this is not the case, then the case for the migration has to be reconsidered.

### 4.7.1 What makes an application migratable

We define an application as migratable when one or more of the following statements about the application are true:

- A Linux version of the application or an alternative application does not exist.
- Porting the application to Linux is not feasible.
- License issues make a move to Linux impossible or highly expensive.

Once an application is designated as migratable, there are several ways to migrate to a Linux client:

- Investigate whether the application can run on a Windows server and be used through remote access mechanisms such as Terminal Server, Citrix Metaframe, or NoMachine NX.
- When using Workplace™ on the Linux client, investigate the use of tools like Connect to connect to Windows servers.
- Examine whether it is possible from a cost perspective to run VMware workstation on the client to create virtual Windows machines on those clients that still need to run the application natively in Windows.
- Create dual-boot clients if the application is not used very often.
- Leave some clients out of the migration and consolidate applications on shared clients.

### 4.7.2 Terminal Server, Citrix Metaframe, or NoMachine NX solutions

If the application can run as a centralized application on a server, solutions such as Windows Terminal, Citrix Metaframe, or NoMachine NX can be used to access them remotely. Before an application can be moved to a central server, certain conditions have to be met:

- The application has to be able to run on a multi-user environment. A multi-user environment has several consequences:
  - Settings must be stored in a per-user location in the registry and file system.
  - More than one user can run the application simultaneously.
  - The application license must allow you to run it in a multi-user environment.
  - The servers must have enough resources to allow you to concurrently run multiple instances of the application or other non-migrated applications.

Client applications are available for Linux for Windows Terminal Server, Citrix Metaframe, and NoMachine NX. The client for Windows Terminal Server, desktop, is open source; the Citrix client is available when you purchase Metaframe solutions; and NoMachine has released the NX client under the GPL.
