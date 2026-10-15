In addition to interface configuration, ifconfig is also used to report interface status; therefore, ifconfig's functionality can be grouped into two sections: interface reporting and interface configuration.

# Interface Reporting

Most often ifconfig is used for interface reporting to assist in network troubleshooting.

The basic command without any parameters proves very useful:

```
[root@lefty /sbin]# /sbin/ifconfig
et0      Link encap:Ethernet  HWaddr 00:E9:29:4B:AC:0C
          inet addr:192.168.1.254  Bcast:192.168.1.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:9833  errors:0  dropped:0  overruns:0  frame:0
          TX packets:10195 errors:0  dropped:0  overruns:0  carrier:0
          collisions:306  txqueuelen:100 
          Interrupt:10  Base address:0xb800

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:3924  Metric:1
          RX packets:18  errors:0  dropped:0  overruns:0  frame:0
          TX packets:18  errors:0  dropped:0  overruns:0  carrier:0
          collisions:0  txqueuelen:0
```

ifconfig has reported all interfaces recognized by the kernel and configured for use. (Linux ifconfig, unlike other versions of UNIX, does not require an additional parameter to see all interfaces.) On the eth0 we can easily determine that the interface is Ethernet based on the interface name (eth0), the Link encap:Ethernet, and the 6-byte (48 bits) address. The IP address is reported on the next line with the broadcast address and netmask used.

The third line reports that the interface is currently running (UP), which means it can send and respond to network traffic. It is running in broadcast (standard for Ethernet) and additionally is configured to listen to multicast traffic. The multicast configuration is required to allow multicast traffic to be examined by the kernel and user applications such as RIP-2 because RIP-2 uses the RIP multicast address of 224.0.0.9.

The maximum transmission unit (MTU) is 1500 bytes, a standard length for Ethernet frames, and ifconfig has reported this is the size the kernel is configured to. As the name, maximum transmission unit, implies, this is the largest packet size that will be transmitted out of that interface. Should the administrator manually lower the size of the MTU, it will only affect the outgoing packets, which means the system will still recognize the incoming packets that are within the largest MTU supported by the topology. Common MTU sizes are shown in Table 9.1.