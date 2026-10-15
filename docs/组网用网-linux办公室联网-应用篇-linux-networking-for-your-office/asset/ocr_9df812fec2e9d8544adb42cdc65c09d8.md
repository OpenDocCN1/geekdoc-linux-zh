If the system responds package dhcpcd is not installed, then you need to install it from your CD-ROM. If the system responds with a precise package version, then DHCP client support is installed on your system. To configure your system with DHCP on the eth0 interface, type

```
/sbin/dhcpcd -d -D -H eth0
```

This command tells the system to do maximal configuration through DHCP, including the computer's domain name (the -D option) and host name (the -H option). You set your own domain and host names by omitting these options from the dhcpcd command line and setting them manually, as described in "Setting the Machine Name," earlier in this chapter, or by using the -h option to specify a host name manually. You can learn more about dhcpcd's options by typing man dhcpcd.

dhcpcd sets the following networking options:

+   - The machine name—dhcpcd sets this option if configured to do so with the -H switch, and if the DHCP server provides this information.
+   - The network name—dhcpcd sets this option if configured to do so with the -D switch, and if the DHCP server provides this information.
+   - The IP address—This address can change from one session to another, and even midsession if your client and the server need to renegotiate the DHCP "lease."
+   - The netmask—This is likely the same from one session to another.
+   - The gateway—This is the computer through which traffic to the Internet as a whole flows.
+   - The DNS servers—DHCP sets the addresses of remote DNS servers. It does not configure a DNS server on your own computer.
+   - The Ethernet adapter—DHCP brings up the Ethernet adapter, much as ifconfig does.

In other words, DHCP does all the work outlined in the section "Configuring a System with a Fixed Address" except for running a DNS server on your system. You shouldn't run a DNS server on a system that obtains its address via DHCP, anyhow, since its IP address isn't guaranteed to remain constant. As a constant IP address is a practical necessity for a DNS server, being a DHCP client and a DNS server are mutually incompatible. (If you also run the DHCP server, you could configure it to provide a fixed address to the DHCP client/DNS server, but in that case you might simply run both servers on one computer.) Running many other types of TCP/IP servers on DHCP-served computers is also suboptimal at best, because remote machines might have trouble locating the server's current IP address if and when it changes.