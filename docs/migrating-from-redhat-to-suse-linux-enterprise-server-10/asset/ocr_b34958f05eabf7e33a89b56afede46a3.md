+   - On Cable Connection. If there is a physical network connection.
+       - On Hotplug. When the hardware is plugged in.
+       - Manually.
+       - Never.
+       
+       Normally only root is allowed to activate and deactivate a network interface. To allow this for normal users activate the option **User Controlled**.

+   - **MTU.** (Maximum Transfer Unit) Maximum size of an IP package. The size depends on the hardware (Ethernet: max. 1,500 Bytes).

After you save the configuration with YaST, the ethernet card should be available in the computer. You can verify this with the command `ip`, as in the following:

```
dxf1:~ # ip address show
 1: lo: <LOOPBACK,UP> mtu 16436 qdisc noqueue
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 brd 127.255.255.255 scope host lo
    inet6 ::1/128 scope host
 2: eth0: <BROADCAST,MULTICAST,UP> mtu 1500 qdisc pfifo_fast qlen 100
    link/ether 00:e0:7d:9e:02:e8 brd ff:ff:ff:ff:ff:ff
    inet 10.0.0.51/24 brd 10.0.0.255 scope global eth0
    inet6 fec0::1:200:1cff:feb5:6516/64 scope site dynamic valid_lft 2591994sec preferred_lft 604794sec
    inet6 fe80::200:1cff:feb5:6516/10 scope link
 3: sit0@NONE: <NOARP> mtu 1480 qdisc noop
    link/sit 0.0.0.0 brd 0.0.0.0
```

In this example, the interface eth0 was configured.

Two network devices are always set up by default-the loopback device (lo) and the device sit0@NONE, which is needed for integrating cards in networks with IPv6.