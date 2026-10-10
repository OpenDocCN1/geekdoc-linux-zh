Masquerading or Network Address Translation (NAT), as described in Chapter 15. Table 14-3 lists the private IP addresses not used on any public part of the Internet.

# Table 14-3: Private IP Addresses

| Network Class | Network Numbers | Addresses per Network Number |
| --- | --- | --- |
| Class A | 10.0.0.0 | 167, 777, 216 |
| Class B | 172.16.0.0 to 172.31.0.0 | 65,536 |
| Class C | 192.168.0.0 to 192.168.255.255 | 256 |

So, for a small private LAN, the following numbers are examples of IP addresses that could be assigned to the host computers on your network. (You could use any of the network numbers, plus host numbers, from the table. These are just examples.)

+   - 192.168.1.1
+   - 192.168.1.2
+   - 192.168.1.3
+   - 192.168.1.4
+   - 192.168.1.5

You could continue that numbering up to 192.168.1.254 on this network, and you could use a network mask of 255.255.255.0.

# Troubleshooting Your LAN

After your LAN has been set up, your Ethernet cards installed, and hostnames and addresses added, there are several methods you can use to check that everything is up and working. Some troubleshooting techniques are shown in the following sections.

# Did Linux find your Ethernet driver at boot time?

Type the following right after you boot your computer to verify whether Linux found your card and installed the Ethernet interface properly:

```
dmesg | grep eth
```

The dmesg command lists all the messages that were output by Linux at boot time. The grep eth command causes only those lines that contain the word eth to be printed. The first message shown here appeared on my laptop computer with the NETGEAR card. The second example is from my computer with the EtherExpress Pro/100 card:

```
eth0: NE2000 Compatible: port Ox300, irq3, hw addr: 00:B0:8C:8C:8E:49
mth0: OEM 182557/182558 10/100 Ethernet at OxccO0, 00:90:27:48:67:35, IRQ 17.
```