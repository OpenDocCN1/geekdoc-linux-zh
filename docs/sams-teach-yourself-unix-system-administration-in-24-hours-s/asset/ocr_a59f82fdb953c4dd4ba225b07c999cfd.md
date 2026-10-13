```
hardware Ethernet 00:A0:DD:8E:C3:F9;
fixed-address 198.76.82.151
}
range 198.76.82.131 198.76.82.132
}
```

As you can see, most of the information is identical to that specified for a single client on the network. The host iMac is the iMac system, and it's always assigned the same fixed IP address. Finally, the range of available IP addresses here is quite small: 131 to 132. Normally we'd have quite a few more IP addresses than that for the DHCP pool.

You'll want to create the empty dhcpd.leases file so that the server can create timestamp and lease information, which can easily be done with

```
# touch /var/lib/dhcpd.leases
```

> The dhcpd server automatically rotates the dhcpd.leases file as needed, renaming the old lease file dhcpd.leases~. On very rare occasions the system could crash in the midst of this lease rotation, in which case you'll want to rename the - file back to the original name (for example, mv dhcpd.leases- dhcpd.leases) to ensure that any DHCP leases currently assigned are still valid and known.

To start or stop the server, create the appropriate link (in Red Hat Linux, at least) to the /etc/rc.d/init.d/dhcp from within the /etc/rc.d/rcn.d directory for run state n.

Although configuring a Linux system to be a good network citizen isn't quite as simple and straightforward as a Mac or Windows box, it's not too far off. If you opt to use some of the graphical interfaces to Linux (notably linuxconf), you can set up almost everything shown here in just a few minutes.

Also, if you find that you don't have dhcpd on your Red Hat Linux distro, it might be because you didn't install the optional packages on the additional CD-ROMs, or because you didn't specify the server configuration upon installation. Verify this by using RPM (rpm -qa | grep -i dhcp will do the trick). You can remedy this omission most easily by flipping back to Hour 8, "Unix Package Management," and searching Pbone or a similar archival site for the dhcp package, and installing it with rpm.