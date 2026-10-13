```
lo
        collisions:0 txqueuelen:100
        Interrupt:5 Base address:0x6000
        Link encap:Local Loopback
        inet addr:127.0.0.1 Mask:255.0.0.0
        UP LOOPBACK RUNNING MTU:3924 Metric:1
        RX packets:48474 errors:0 dropped:0 overruns:0 frame:0
        TX packets:48474 errors:0 dropped:0 overruns:0 carrier:0
        collisions:0 txqueuelen:0
```

The first line shows the interface name (eth0 in this case), the encapsulation method, and the Ethernet hardware address. The second line shows the IP address of the interface, the netmask, and the broadcast address. The third line shows the status of the interface (UP or DOWN). The lines after that give statistics on packets received and sent, and error counters.

Some common interface configuration problems are using the subnet mask or IP address. If two systems are accidentally configured with the same IP address, a very strange situation ensues. Packets intended for host A get stolen by the imposter B. Neither host can function properly. The situation worsens considerably if one of the hosts is a server of sorts to which many clients connect. In this case all applications that are trying to connect to this server will exhibit long behavior. To troubleshoot such a problem the most appropriate tool is the arp command, which we will look at in the next section.

One way to deal with a problem like this is to disconnect the network connection of the offending system immediately. This restores the network back to sanity and the larger problem is resolved. In addition you will have to delete the arp entry of the duplicate machine and temporarily add a static entry for the bona-fide system. Now you should be able to examine and correct the IP address of the offending system.

To change the IP address of eth0 to 10.1.0.5 and the netmask to 255.255.0.0, you can use the following steps:

```
# ifconfig eth0 down
# ifconfig eth0 address 10.1.0.5 netmask 255.255.0.0
# ifconfig eth0 up
```

In addition you should change the IP address in the local /etc/hosts file and correct the NIS and DNS databases.

# USING arp

The arp command displays the translation of an IP address to an Ethernet MAC address. This makes it an excellent debugging tool because it allows you to track the relationship between IP addresses and particular network interfaces.

For example, in the previous section we looked at what happens when an IP address is accidentally assigned to two machines. If this happens a duplicate IP address error will be reported and logged. Checking /var/log/messages on the system whose IP address is stolen by some other system should include entries similar to the following:

```
Dec  6 14:42:56 saturn vmunix: duplicate IP address!!
sent from ethernet address 00:C0:4F:A9:F9:26
```