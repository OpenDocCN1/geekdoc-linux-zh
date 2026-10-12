Linux may be configured as a fully functional NetWare server, and even provides support for the SPX protocol. For more information on IPX services, see the 1PX-HOWTO, which can be found at the Linux Documentation Project (http://www.linuxdoc.org).

Installing Linux as the Grand Unified Linux Field is content enough for its own book, but general information on configuring Linux to glue together a heterogeneous network of Novell, Macintosh, and TCP/IP workstations can be found at Linux/Mac/Win Web page (http://www.eats.com/linux_mac_win.html).

# Enterprise Networks and X.25 Support

Enterprise administrators will be most interested in the Linux support for X.25 protocol. This is a method for putting many virtual circuits through one high-speed line. This support is presently labeled experimental and does not yet include support for dedicated X.25 network cards. Linux does provide X.25 services over ordinary modems and Ethernet networks using the 802.2 LLC or LAPB protocols.

The WAN option is also of interest to enterprise admins looking for an inexpensive alternative to a dedicated WAN router. Using commercially available WAN interface cards and the WAN-tools package from Sangoma (ftp://ftp.sangoma.com), a low-cost Linux machine will make a perfectly serviceable WAN router. This router can also still be used for other purposes, such as providing a firewall, a Web server, or an FTP site. For the serious enterprise, the FreeS/WAN project in Toronto has a free encryption layer for the Linux WAN, using 1,024-bit keys and 168-bit Triple-DES technology, and incorporating the Internet Protocol Security (IPSEC).

Related to X.25 and WAN, Linux also provides support for frame-relay. Look under the DLCI options in Network Devices for more information.

# Ethernet Bridging

Ethernet Bridging will bind together the network segments on multiple Ethernet cards to create one seamless network. Several such nodes can be used to link multiple composite networks. For more information, consult the Ethernet Bridge Mailing List home page (http://openrok.net/~mailman/listinfo/bridge).

# Forwarding on High-Speed Interfaces and Slow CPUs

One popular use of Linux is to breathe new life into aging hardware. This can, however, lead to networking problems because even a 120MHz machine can be overrun by a 10Mb/sec ethernet connection. If you experience trouble with network overruns, these options will modify the network support to accommodate the slower machines.