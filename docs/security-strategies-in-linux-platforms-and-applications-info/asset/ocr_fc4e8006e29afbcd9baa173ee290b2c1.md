# CHAPTER 8 | Networked Filesystems and Remote Access

In other words, it uses authentication systems such as the Password Authentication Protocol (PAP), Challenge-Handshake Authentication Protocol (CHAP), and the Extensible Authentication Protocol (EAP). The first two are commonly associated with connections over telephone modem. EAP is an authentication system often used on wireless networks.

Such authentication systems require a username and password database. RADIUS can work with a variety of such databases, including the LDAP, the Network Information Service (NIS), Microsoft's Active Directory, Novell's eDirectory, and even the old standby, the local shadow password suite.

# RADIUS Configuration Files

When installed on an Ubuntu system, configuration options are commented into a number of files in the /etc/freeradis/ directory. On some other systems, you'll find these files in the /etc/raddb/ directory. Table 8-2 describes the function of each of these files and subdirectories.

# Moving Away from Clear-Text Access

To understand the risks associated with clear-text access, take a look at Figure 8-4. It's an excerpt from the Wireshark network analyzer. It can read the contents of every packet sent over the local network. Every system on an Ethernet network can listen in all network communications, even those two remote systems on the LAN. That's the way Ethernet works. Figure 8-3 illustrates the contents of one packet, which happens to be one letter of a password.

Wireshark is readily available for most Linux distributions, including Red Hat and Ubuntu. Early in this chapter, we noted to regular Telnet that can be hiding usernames and passwords in network communication.

![](bbox=[0.165, 0.636, 0.835, 0.856])