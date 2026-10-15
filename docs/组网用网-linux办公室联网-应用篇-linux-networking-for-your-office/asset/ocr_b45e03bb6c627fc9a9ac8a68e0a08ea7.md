Many distributions (including Red Hat 6.0) configure themselves to start dhcpd when you reboot the computer, but for some, you may need to add an appropriate line to /etc/rc.d/rc.local or some other startup file.

This discussion only scratches the surface of DHCP configuration in Linux. For more information, you should consult the dhcpd.conf and dhcpd manpages or the DHCP Mini-HOWTO, available with most Linux distributions and on this book's CD in the doc/HOWTO/mini directory.

# Using linuxconf to Configure Networking

The preceding discussions provide the nitty-gritty detail of how Linux goes about configuring itself for networking. This is useful information, particularly if you're trying to debug a network connection that's not working properly. If you just want to quickly configure a machine, however, you might prefer a streamlined configuration approach, particularly if you need to set up static IP addresses. This streamlined approach is provided by the linuxconf utility in Red Hat 6.0. Many other distributions provide similar GUI configuration tools, though the details of their operation do differ.

# Setting Basic Host Information

To begin, you should select the Config, Networking, Client tasks, Basic host information option in linuxconf. The first item you can enter here is the host name, and you should enter it. When you click the Adaptor 1 tab, you can enter additional information, as shown in Figure 7.1. If you select DHCP as the Config mode, you only need to enter the Net device and Kernel module; the system obtains the rest of the information from the DHCP server. If you select Manual for the Config mode, you need to enter your machine's full name and IP address, at a minimum, in addition to the Net device and Kernel module.

You should also select Config, Networking, Routing and gateways, Defaults to set the default gateway (again, that's the computer that transfers information from your local network to the Internet at large). You specify this machine by its numerical IP address rather than its machine name.

# Name Server Specification

To configure your name server and related options, you should first select Config, Networking, Client tasks, Name server specification (DNS). This produces the display shown in Figure 7.2, in which you can enter the default domain, up to three nameservers, and up to six search domains.