
## 644 CHAPTER 17 CONFIGURING AND MONITORING A LAN

![](img/45ff4cd21497435daa35084a84b95d07_694_0.png)

Figure 17-4 The Network Connections window

To modify the configuration of a NIC, select the appropriate tab, highlight the description of the connection you want to configure, and click Edit; nm-connection-editor displays the Editing window (Figure 17-5). The IPv4 Settings tab allows you to select DHCP or manual configuration of the connection. When you are finished working in the Editing window, click Apply.

Wireless settings: It is usually easier to configure a wireless connection using the NetworkManager applet (next section) than it is to use the Editing window. To use the Editing window

![](img/45ff4cd21497435daa35084a84b95d07_694_1.png)

Figure 17-5 The Editing window (wireless connection)

# NetworkManager: Configures NETWORK CONNECTIONS

| Wired Network |
| :--- |
| Auto Ethernet |
| Disconnect |
| Wireless Networks |
| Barcoast Open Access |
| Disconnect |
| Available |
| 2WIRE643 |
| 6330 7027 |
| Barbary Coast Secure |
| hpsetup |
| linksys |
| More networks |
| VPN Connections |
| Connect to Hidden Wireless Network... |
| Create New Wireless Network... |

Figure 17-6 The NetworkManager applet left-click menu

to configure wireless settings, click the Wireless tab, click Add (or highlight the connection and click Edit), and enter the appropriate information. When you are finished entering information in the Editing window, click Apply.

# THE NETWORKMANAGER APPLET LEFT-CLICK MENU

Left-clicking the NetworkManager applet displays a menu that lists the available wireless networks. It also displays selections labeled More networks, Connect to Hidden Wireless Network, and Create New Wireless Network (if the system has a wireless connection), Wired Network, Disconnect, and VPN Connections. In Figure 17-6, Auto Ethernet appears below Wired Network and Disconnect appears below Wireless Networks, meaning that the system is using the Ethernet wired connection and not using a wireless connection.

Click the name of the wired network (e.g., Auto Ethernet) or the name of a wireless network (under the word Available) to connect to a network. The NetworkManager applet shows activity while it connects to the new network. It then displays the wireless or wired icon, as appropriate (Figure 17-2, page 643). To disable a network, click Disconnect below the name of the connection you want to disable.

# SETTING UP SERVERS

Setting up local clients and servers can make a LAN both easier to use and more useful. The following list briefly describes some of these tools and references the pages that describe them in detail.

- Firewall: Although not a server, a firewall—which is typically installed on the router—is an important part of a LAN. See gufw (page 876) and iptables (page 880) for more information.

- NIS: NIS can provide a uniform login regardless of the system you log in. The NIS authentication server is covered on page 750 and the client on page 744. NIS is often combined with home directories that are mounted using NFS.

- NFS: NFS allows you to share directory hierarchies. Sharing directories using NFS requires that the server export the directory hierarchy (page 785) and clients mount the hierarchy (page 777).

- Using NFS: You can store all home directories on one system and mount them from other systems as needed. This configuration works well with NIS login authentication. With this setup, it can be convenient to create a world-writable directory—/home/shared—that users can use to exchange files. If you set the sticky bit (page 1174) on this directory (chmod 1777 /home/shared), users can delete only files they created. If you do not set the sticky bit, any user can delete any file.

- OpenSSH: OpenSSH tools include ssh (logs in a remote system; page 670) and scp (copies files to and from a remote system; page 672). You can also set up a shared home directory with NFS, each user's ~/.ssh directory (page 666) is the same on each system; a user who sets up a personal authentication key (page 677) will be able to use OpenSSH tools between systems without entering a password. See page 677 for information on how to set up an OpenSSH server. You can just use the ssh and scp clients—you do not have to have them.

- DNS: Setting up a local cache can reduce the traffic between the LAN and the Internet and can improve response times. For more information refer to “JumpStart: Setting Up DNS Cache” on page 834.

- DHCP: DHCP enables a client to retrieve network configuration information from each time it connects to a network. See page 470 for more information.

- LDAP: LDAP is a database server that can hold names and addresses, authentication, and other types of data. See page 758 for more information.

- Samba: Samba allows Linux systems to participate in a Windows network, sharing directories and printers, and accessing those directories and printers by Windows systems. Samba includes a special share for accessing users' home directories. For more information refer to “The [homes]: Sharing Users” on page 814.

You can also use Samba to share the following:

```
[public]
comment = 
path = /home/shared
read only = no
browseable = yes
```

# INTRODUCTION TO CACTI

Cacti is the complete RRtool-based graphing solution store time-series data efficiently, and through the use of aggregation functions makes it easy to create a lot of detail for time periods but progressively less detail as the files age. RRDtool generates both simple and complex graphs from RRD files.

Cacti is part of the next generation of monitoring tools. It builds on the lessons learned from tools such as MRTG (ossetiker.ch/mrtg; page 948) and Cricket (sourceforge.net/projects/cricket). Each of these tools has the following capabilities:

- Periodically polls devices for data. The tool commonly used to collect this data is SNMP (Simple Network Management Protocol); www-net-snmp.org.
- Stores the data in RRD file.
- Has a Web interface that allows you to examine graphs generated from stored data. These graphs typically display daily, weekly, and yearly information.

Cacti configuration is performed through its Web interface, whereas MRTG and Cricket are configured by editing text files.

RRD files and RRDtool are the key to much of Cacti's functionality. The Cacti Web describes Cacti as "the complete RRtool-based graphing solution store time-series data efficiently, and through the use of aggregation functions makes it easy to create a lot of detail for time periods but progressively less detail as the files age."

Many extensions and plugins are available for Cacti. Once you are familiar with the basic use and operation of Cacti, visit cacti.net/additional_scripts.php for a partial list of these additions. Also visit the documentation and the user forums to obtain more information about Cacti and to learn how you can add functionality and support for different devices and data sources.

# CONFIGURING SNMP

If you want to monitor data sources on the local system, install and run the SNMP daemon on the local system as explained under "Setting Up a Remote Data Source" on page 654.

# SETTING UP LAMP

You must install these applications before you can configure Cacti. This section explains how to set up the software on the system running Cacti. See "Setting Up a Remote Data Source" on page 654 for an explanation of how to set up a system that Cacti will query and report on. By default, Cacti sets up the local system to run Cacti and a data source.

# NOTES

When you set up LAMP, you use the MySQL database; databases named mysql and cacti. Ubuntu sets up the mysql database when you install MySQL. You set up and populate the cacti database as explained under "Configuring MySQL" on page 650.

You need to set up the following database users. Each of these accounts should have a password:
