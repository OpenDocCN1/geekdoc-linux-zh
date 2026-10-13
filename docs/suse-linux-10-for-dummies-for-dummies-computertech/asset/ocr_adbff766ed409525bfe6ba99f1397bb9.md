is working. SUSE Linux includes several commands to help you monitor and diagnose problems. These tasks are best done by typing commands in a terminal window. I explain a few useful network commands.

# Checking the network interfaces

Use the `/sbin/ifconfig` command to view the currently configured network interfaces. The `ifconfig` command is used to configure a network interface (that is, to associate an IP address with a network device). If you run `ifconfig` without any command line arguments, the command displays information about current network interfaces. The following is typical output when you type **/sbin/ifconfig** in a terminal window:

```
```text
eth0      Link encap:Ethernet  HWaddr 00:08:74:E5:C1:60
          inet addr:192.168.0.6  Bcast:192.168.0.255  Mask:255.255.255.0
          inet6 addr: fe80::208:74ff:fee5:c160/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:9370 errors:0 dropped:0 overruns:1 frame:0
          TX packets:74097 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:33574333 (32.0 Mb)  TX bytes:8832457 (8.4 Mb)
          Interrupt:10 Base address:0x3000

eth1      Link encap:Ethernet  HWaddr 00:02:2D:8C:F8:C5
          inet addr:192.168.0.8  Bcast:192.168.0.255  Mask:255.255.255.0
          inet6 addr: fe80::202:2dff:fe8c:f8c5/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:3403 errors:0 dropped:0 overruns:0 frame:0
          TX packets:22 errors:1 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:254990 (249.0 Kb)  TX bytes:3120 (3.0 Kb)
          Interrupt:3 Base address:0x100

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:3255 errors:0 dropped:0 overruns:0 frame:0
          TX packets:3255 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:2686647 (2.5 Mb)  TX bytes:2686647 (2.5 Mb)
```
```

This output shows that three network interfaces — the loopback interface (lo) and two Ethernet cards (eth0 and eth1) — are currently active on this system. For each interface, you can see the IP address, as well as statistics on packets delivered and sent. If the SUSE Linux system has a dialup link up and running, you also see an item for the ppp0 interface in the output.