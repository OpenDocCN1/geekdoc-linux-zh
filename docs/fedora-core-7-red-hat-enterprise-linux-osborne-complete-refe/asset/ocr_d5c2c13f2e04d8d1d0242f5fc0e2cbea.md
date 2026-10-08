**Figure 5-5**
The system-config-securitylevel tool, version 1.8.

![](bbox=[0.38, 0.11, 0.78, 0.49])

The Custom Rules panel lets you load an IP-tables file that can hold customized firewall rules. Instead of having to choose whether to use system-config-securitylevel or to create a entire set of rules in an IP-tables file, you can use system-config-securitylevel to automatically configure the standard firewall rules and then set up an IP-tables file that holds only customized rules for your system. These will be added to the standard set implemented by system-config-securitylevel. See Chapter 20 for a detailed discussion of IP-tables firewall rules.

Often a Linux system will be used as a router if it is also used to run servers for wider network. If you are creating a strong firewall but still want to run a service such as a Web server, allow users to perform FTP file transfers on the Internet, permit Samba desktop browsing, or allow remote encrypted connections such as SSH, you will have to specify them in the Trusted Services panel. Samba desktop browsing lets you access your Samba shares, like remote Windows file systems, from your GNOME or KDE desktops.

The Custom Ports panel lets you specify ports that you may want opened for certain services, like BitTorrent. Click the Add button to open a dialog where you can enter the port number along with the protocol to control (tcp or udp).

# InfiniBand Support

Fedora, since the 2.6.10 kernel, includes InfiniBand support. This is a new I/O architecture that is used to replace the older bus architectures used in current systems. Often InfiniBand is used as a replacement for local network connections. It is currently implemented in supercomputer and network server clusters. You can find more about InfiniBand at the