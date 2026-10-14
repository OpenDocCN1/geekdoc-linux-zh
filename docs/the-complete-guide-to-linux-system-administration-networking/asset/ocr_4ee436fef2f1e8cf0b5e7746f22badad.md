```
option routers 192.168.1.254;
option domain-name-servers 192.168.1.1, 192.168.1.2;
option domain-name "mydomain.org";

subnet 192.168.1.0 netmask 255.255.255.0 {
    range 192.168.1.10 192.168.1.100;
    range 192.168.1.150 192.168.1.200;
}
```

This file defines two ranges of addresses within the 192.168.1.0 network. Within these ranges, IP addresses are assigned randomly to any client that requests an address. You can tie a specific IP address to a specific host by using the MAC address of that host’s Ethernet card. That portion of the configuration file would look like this:

```
host haagen {
    hardware ethernet 08:00:6b:3a:29:7f;
    fixed-address 192.168.1.5;
}
```

Many additional options are supported by dhcpd.conf. You can refer to the man page for a list of these. Once you have the DHCP server configured, you can start it using the standard script in /etc/rc.d/init.d or run this command:

```
# service dhcpd start
```

A DHCP client can run on any operating system. So long as it “speaks” DHCP, it can obtain an IP address from the Linux DHCP server. Windows DHCP clients, however, do not follow the DHCP standard, and require that you add a route on Linux so that they can use the Linux DHCP server (change the dev from eth0 to match your networking device as needed):

```
# route add -host 255.255.255.255 dev eth0
```

# Networked Printing Services

In Chapter 3, “Using the Shell,” you learned how to set up a local printer using a graphical utility, how to print files from the command line using the lpr command, and how to set up basic printing options using lpoptions. In this section, you learn more about printing functions in Linux, including the networking capabilities of Linux printing.

# Using Traditional Linux Printing: LPRng

The traditional Linux printing system is based on the BSD version of UNIX and is called LPRng. (The name refers to the “next generation” of the LPR printing system, though LPRng is quite old at this point.) LPRng printing allows multiple users to print files at the same time to either local or networked printers.