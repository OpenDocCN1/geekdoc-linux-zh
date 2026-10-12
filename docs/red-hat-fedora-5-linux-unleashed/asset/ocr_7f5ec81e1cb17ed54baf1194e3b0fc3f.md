If no argument is given, ifconfig displays the status of active interfaces. For example, the output of ifconfig, without arguments and one active and configured NIC, looks similar to this:

```
# /sbin/ifconfig
```

```
eth0
    Link encap:Ethernet HWaddr 00:30:1B:0B:07:0D
    inet addr:192.168.2.7 Bcast:192.168.2.255 Mask:255.255.255.0

    UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
    RX packets:127948 errors:0 dropped:0 overruns:0 frame:0
    TX packets:172675 errors:0 dropped:0 overruns:0 carrier:0
    collisions:7874 txqueuelen:100

    RX bytes:19098389 (18.2 Mb) TX bytes:68739080 (65.5 Mb)
    Interrupt:11 Base address:0x2000
```

```
lo
    Link encap:Local Loopback
    inet addr:127.0.0.1 Mask:255.0.0.0

    UP LOOPBACK RUNNING MTU:16436 Metric:1
    RX packets:215214 errors:0 dropped:0 overruns:0 frame:0
    TX packets:215214 errors:0 dropped:0 overruns:0 carrier:0
    collisions:0 txqueuelen:0

    RX bytes:68739080 (65.5 Mb) TX bytes:68739080 (65.5 Mb)
```

The output is easily understood. The inet entry displays the IP address for the interface. UP signifies that the interface is ready for use, BROADCAST denotes that the interface is connected to a network that supports broadcast messaging (ethernet), RUNNING means that the interface is operating, and LOOPBACK shows which device (lo) is the loopback address. The *maximum transmission unit* (MTU) on eth0 is 1500 bytes. This determines the size of the largest packet that can be transmitted over this interface (and is sometimes “tuned” to other values for performance enhancement). Metric is a number from 0 to 3 that relates to how much information from the interface is placed in the routing table. The lower the number, the smaller the amount of information.

The ifconfig command can be used to display information about or control a specific interface using commands as listed in Table 18.1. For example, to deactivate the first Ethernet device on a host, use the ifconfig command, the interface name, and the command down like so:

```
# ifconfig eth0 down
```