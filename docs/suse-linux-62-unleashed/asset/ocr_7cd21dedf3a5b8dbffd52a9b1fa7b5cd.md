faq.pl). Linux also supports the AppleTalk and LocalTalk protocols. According to the recent kernel help files, the GNU boycott of Apple is now over, so even politically correct people may now set this option.

Linux may be configured as fully functional NetWare server, and now it provides experimental support for the SPX protocol. For more information on IPX services, see the IPX-HOWTO in the /usr/doc/howto/ directory of your SuSE CD-ROM or at ftp://metalab.unc.edu/pub/linux/docs/HOWTO. Telling you how to install Linux as a unifying force would probably require its own book, but general information on configuring Linux to glue together a heterogeneous network of Novell, Macintosh, and TCP/IP workstations can be found at http://www.eats.com/linux_mac_win.html.

# Enterprise Networks and X.25 Support

Enterprise administrators will be most interested in the Linux support for X.25 protocol, which is a means for putting many virtual circuits through one high-speed line. This support is presently labeled experimental and does not include support for dedicated X.25 network cards. Linux does provide X.25 services over ordinary modems and Ethernet networks, using the 802.2 LLC or LAPB protocols.

The WAN option is of interest to enterprise admins who are looking for an inexpensive alternative to a dedicated WAN router. Using commercially available WAN interface cards and the WAN-tools package from ftp://ftp.sangoma.com, you can make a low-cost Linux machine a perfectly serviceable router. In addition, the Linux router can still be used for other purposes, such as providing a firewall, a Web server, or anon-FTP. For the serious enterprise, the Free/WAN project in Toronto now offers a free encryption layer for the Linux WAN, using 1,024-bit keys and 168-bit Triple-DES technology and incorporates Internet Security Protocol (IPSEC). Free/WAN also uses encryption technology from outside the U.S. to avoid export restrictions (3DES).

Related to X.25 and WAN, Linux also provides support for frame-relay. See the DLCI options under "Network Devices."

# Forwarding on High-Speed Interfaces and CPUs

One popular use of Linux is to breathe new life into aging hardware. This can lead to some networking problems, however, even a 120MHz machine can be overrun by a 10Mb/sec Ethernet connection. If you experience trouble with network overruns, these options will modify the network support to accommodate the slower machines.