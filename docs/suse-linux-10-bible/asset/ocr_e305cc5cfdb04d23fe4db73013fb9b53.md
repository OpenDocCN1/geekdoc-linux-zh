# 412 Part III ◆ Using the Command Line in SUSE Linux

tions discuss configuring your IP network from the command line. Throughout the rest of this chapter, you will need to be logged in as root to complete network configuration.

# ifconfig

If you need to view the configuration of your network, the ifconfig command is an easy and quick way to do this. As root, you can just type ifconfig to show the configuration of all active network ports (see Listing 15-1), both physical and virtual (we talk about virtual interfaces later in the chapter).

# Listing 15-1: Output of the ifconfig Command

```
# ifconfig
eth0          Link enc:Ethernet HWaddr:00:03:ff:69:68:12
       inet addr:192.168.1.130 Bcast:192.168.1.255 Mask:255.255.255.0
       inet6 addr:fe80::203f:ff69:68d12/64 Scope:Link
      UP BROADCAST RUNNING MULTICAST  Metric:1 MTU:1500
  rx packets:30256 errors:0 dropped:0 overflows:0 frame:0
  tx packets:36509 errors:0 dropped:0 overflows:0 carrier:0
  collisions:0 txuellen:1000
  rx bytes:4048565 (3.8 Mb) TX bytes:34473633 (32.8 Mb)
  Interrupt:1 Base address:0x1080
lo            Link enc:Loopback
       inet addr:127.0.0.1 Mask:255.255.0.0
       inet6 addr ::/128 Scope:Host
      UP LOOPBACK MTU:16384 Metric:1
  rx packets:3162 errors:0 dropped:0 overflows:0 frame:0
  tx packets:3162 errors:0 dropped:0 overflows:0 carrier:0
  collisions:0 txuellen:0
  rx bytes:11507333 (1.0 Mb) TX bytes:11507333 (1.0 Mb)
```

The output of ifconfig can seem confusing for new users. See Chapter 6 for information on understanding most of the output.

![](bbox=[0.115, 0.712, 0.193, 0.745])

Table 15-1 shows a breakdown of the ifconfig output.

You may come across other flags that are attached to your network interface, one common being the PROMIS flag. This flag means that your Ethernet adapter will actually listen to all packets traversing its link as opposed to listening only for packets destined for its own station.

![](bbox=[0.115, 0.796, 0.193, 0.855])