
![](img/2344fc4a798f29dca9e8b5ed7288171a_693_0.png)

Figure 17-2 The NetworkManager applet on the “Top panel

## THE NETWORKMANAGER APPLETS RIGHT-CLICK MENU

Right-click the NetworkManager applet to display a menu that allows you to turn on/off networking and, if available, wireless (networking). See Figure 17-3. Click either Enable Networking or Enable Wireless to place or remove a tick next to the entry; a tick indicates the service is enabled. You can also select Connection Information to display a window showing information about the active connection or you can select Edit Connections (next).

## THE NETWORK CONNECTIONS WINDOW (nm-connection-editor)

Selecting Edit Connections from the NetworkManager applet right-click menu runs the nm-connection-editor utility, which opens the Network Connections window (Figure 17-4, next page). Alternatively, you can give the command nm-connection-editor from a terminal emulator or Run Application window (Alt+F2). From this window you can modify the configuration of wired and wireless NICs.

The Network Connections window has tabs that allow you to configure wired, wireless, and other types of network connections. After the system identifies and configures new network hardware, you can use this window to modify the configuration.

![](img/2344fc4a798f29dca9e8b5ed7288171a_693_1.png)

Figure 17-3 The Network Manager applet right-click menu

![](img/2344fc4a798f29dca9e8b5ed7288171a_694_0.png)

**Figure 17-4** The Network Connections window

To modify the configuration of a NIC, select the appropriate tab, highlight the description of the connection you want to configure, and click **Edit**; **nm-connection-editor** displays the Editing window (Figure 17-5). The IPv4 Settings tab allows you to select DHCP or manual configuration of the connection. When you are finished working in the Editing window, click **Apply**.

### Wireless settings

It is usually easier to configure a wireless connection using the NetworkManager applet (next section) than it is to use the Editing window. To use the Editing window

![](img/2344fc4a798f29dca9e8b5ed7288171a_694_1.png)

**Figure 17-5** The Editing window (wireless connection)

![](img/2344fc4a798f29dca9e8b5ed7288171a_695_0.png)

to configure wireless settings, click the **Wireless** tab, click **Add** (or highlight the connection and click **Edit**), and enter the appropriate information. When you are finished entering information in the Editing window, click **Apply**.

## THE NETWORKMANAGER APPLET LEFT-CLICK MENU

Left-clicking the NetworkManager applet displays a menu that lists the available wireless networks. It also displays selections labeled **More networks**, **Connect to Hidden Wireless Network**, and **Create New Wireless Network** (if the system has a wireless connection), **Wired Network**, **Disconnect**, and **VPN Connections**. In Figure 17-6, **Auto Ethernet** appears below **Wired Network** and **Disconnect** appears below **Wireless Networks**, meaning that the system is using the Ethernet wired connection and is not using a wireless connection.

Click the name of the wired network (e.g., **Auto Ethernet**) or the name of a wireless network (under the word **Available**) to connect to a network. The NetworkManager applet shows activity while it connects to the new network. It then displays either the wireless or wired icon, as appropriate (Figure 17-2, page 643). To disable a network, click **Disconnect** below the name of the connection you want to disable.

## SETTING UP SERVERS

Setting up local clients and servers can make a LAN both easier to use and more useful. The following list briefly describes some of these tools and references the pages that describe them in detail.

- **Firewall** Although not a server, a firewall—which is typically installed on the router—is an important part of a LAN. See **gufw** (page 876) and **iptables** (page 880) for more information.
- **NIS** NIS can provide a uniform login regardless of which system you log in on. The NIS authentication server is covered on page 750 and the client on page 744. NIS is often combined with home directories that are mounted using NFS.
- **NFS** NFS allows you to share directory hierarchies. Sharing directories using NFS requires that the server export the directory hierarchy (page 785) and that clients mount the hierarchy (page 777).
  - Using NFS, you can store all home directories on one system and mount them from other systems as needed. This configuration works well with NIS login authentication. With this setup, it can be convenient to create a world-writable directory—for example, **/home/shared**—that users can use to exchange files. If you set the sticky bit (page 1174) on this directory (**chmod 1777 /home/shared**), users can delete only files they created. If you do not set the sticky bit, any user can delete any file.
- **OpenSSH** OpenSSH tools include **ssh** (logs in on a remote system; page 670) and **scp** (copies files to and from a remote system; page 672). You can also set up automatic logins with OpenSSH: If you set up a shared home directory with NFS, each user’s `~/.ssh` directory (page 666) is the same on each system; a user who sets up a personal authentication key (page 677) will be able to use OpenSSH tools between systems without entering a password. See page 677 for information on how to set up an OpenSSH server. You can just use the **ssh** and **scp** clients—you do not have to set them up.
- **DNS cache** Setting up a local cache can reduce the traffic between the LAN and the Internet and can improve response times. For more information refer to “JumpStart: Setting Up a DNS Cache” on page 834.
- **DHCP** DHCP enables a client system to retrieve network configuration information from a server each time it connects to a network. See page 470 for more information.
- **LDAP** LDAP is a database server that can hold names and addresses, authentication information, and other types of data. See page 758 for more information.
- **Samba** Samba allows Linux systems to participate in a Windows network, sharing directories and printers, and accessing those directories and printers shared by Windows systems. Samba includes a special share for accessing users’ home directories. For more information refer to “The [homes] Share: Sharing Users’ Home Directories” on page 814.

You can also use Samba to set up a shared directory similar to the one described under “NFS.” To share a Linux directory with Windows computers, the value of `Workgroup` in `/etc/samba/smb.conf` must be the same as the Windows workgroup (frequently `MSHOME` or `WORKGROUP` by default). Place the following code in `smb.conf` (page 808):

```
[public]
comment = Public file space
path = /home/shared
read only = no
public = yes
browseable = yes
```

Any Windows or Mac user can access this share, which can be used to exchange files between users and between Linux, Mac, and Windows systems.

## INTRODUCTION TO CACTI

Cacti (cacti.net) is a network monitoring tool that graphs system and network information over time (*time-series data*) and provides a comprehensive Web interface for browsing and examining the ongoing performance of the devices on a network.

For example, you can configure Cacti to monitor the network traffic passing through the network ports on local servers and the switch and router ports on the local network. Cacti graphs provide information on traffic levels on the various parts of the network. When the network is slow, for example, you can refer to the historical graphs and see if anything out of the ordinary has occurred. In addition to network traffic levels, Cacti can collect data on CPU utilization, disk space usage, page views on a Web server, and almost any other data points available on the local network.

Cacti collects baseline (typical) data over time. You can use that information to gain insight into the ongoing behavior of a system and network and help you resolve problems. The information can even predict what may happen in the future (e.g., when a disk is likely to become full).

Once installed and configured, Cacti periodically polls devices on a network for the data it needs and stores the data in RRD files for use with RRDtool (round-robin database tool; oss.oetiker.ch/rrdtool). The Cacti Web interface allows you to browse a list of devices and graphs, and see visual representations of the devices over time.

Cacti is part of the next generation of monitoring tools. It builds on the lessons learned from tools such as MRTG (oss.oetiker.ch/mrtg; page 948) and Cricket (sourceforge.net/projects/cricket). Each of these tools has the following capabilities:
