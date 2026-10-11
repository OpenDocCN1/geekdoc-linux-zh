# # The Seven Critical Network Files

Networks can be global in nature or as simple as a room with two or three computers connected together. There are two basic ways to set up the software to connect a Solaris machine to a network:

+   - Run the sys-unconfig utility and reboot the machine. After rebooting, it will ask you for system configuration information such as the host name, domain name, time zone, IP address, IP subnet mask, and root password. This is not recommended for the typical user because it can have dire effects. Only an experienced system administrator should ever attempt this, and only after doing a complete backup of the system.

+   - You can set up networking software by editing a few files such as hosts, netmasks, defaultrouter, and <i>hostname.<interface></i>. If you change the system name, you must also edit the /etc/net/ticlts/hosts, /etc/net/ticots/hosts, and /etc/net/ticotsord/hosts files.

There are seven critical network files that provide TCP/IP configuration information, all of which are created by a default Solaris installation. In most instances, network problems can be resolved by examining these files, making sure the entries are correct, and/or editing the entries that are not correct.

The seven critical network files are as follows:

**/etc/hostname.<interface>** This file defines the network interface device, typically a NIC, and includes the IP address and host name. For example, in a system with two NICs (called a dual-homed system), each NIC would have a file. Dual-homed systems are often used in routers and proxy servers because they provide physical network isolation of one network (say an Internet connection) to an internal network. When you are using IPv6, the file /etc/ hostname6.<interface> is used to start the network interface.

**/etc/nodename** This file should have only one entry in it, the host name of the local system.

**/etc/defauldomain** This file should contain the fully qualified NIS domain name of the domain that the system’s local host is on.

**/etc/defaultrouter (optional)** This file should contain the name of any router that is connected to your network in the form of the network interface name that serves as the router between networks.

**hosts database** The hosts database contains a table of IP addresses and host names for systems on your network. For any of the common name services