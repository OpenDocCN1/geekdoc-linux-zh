# Using TCP/IP Diagnostic Commands

Assuming the network is configured, you should check to see whether the network is up and running and whether your Red Hat Linux system is properly configured for TCP/IP networking. You can, of course, use network applications such as TELNET and FTP to verify that the network is up and running, but Red Hat Linux also includes a number of utility programs that help you monitor and diagnose problems.

# Checking the interfaces

Type the /sbin/ifconfig command to view the currently configured network interfaces. The ifconfig command also configures a network interface (associates an IP address with a network device) during system startup. However, if you run ifconfig without any command-line arguments, the command displays information about the current network interfaces. Here is the result of a typical invocation of ifconfig:

```
/sbin/ifconfig
eth0      Link encap:Ethernet  HWaddr 02:60:8C:8E:C6:A9
          inet addr:192.168.1.200  Bcast:192.168.1.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:3007  errors:0  dropped:0  overruns:0  frame:0
          TX packets:1140 errors:0  dropped:0  overruns:0  carrier:0
          collisions:0 txqueuelen:100
          Interrupt:5  Base address:0x300

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:3924  Metric:1
          RX packets:54 errors:0 dropped:0 overruns:0 frame:0
          TX packets:54 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
```

This output shows that two interfaces — the loopback interface (lo) and an Ethernet card (eth0) — are currently active on this system. For each interface, you get to see the IP address, as well as statistics on packets delivered and sent. For the Ethernet card, ifconfig also reports the IRQ (shown as Interrupt: 5) and the base I/O port address (0x300). If the Red Hat Linux system had a dial-up PPP link up and running, you’d also see an item for the ppp0 interface in the output.

# Checking the IP routing table

Another network configuration command, /sbin/route, also provides status information when you run it without any command-line argument. If you are having