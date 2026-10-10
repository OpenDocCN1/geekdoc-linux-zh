# Introduction to Linux

Things to note:

+   * two network interfaces, even on a system that has only one network interface card: “lo” is the local loop, used for internal network communication; “eth0” is a common name for a *real* interface. Do not ever change the local loop configuration, or your machine will start malfunctioning. Wireless interfaces are usually defined as “wlan0”; modem interfaces as “ppp0”, but there might be other names as well.
+   * IP addresses, marked with “inet”: the local loop always has 127.0.0.1, the physical interface can have any other combination.
+   * The hardware address of your interface, which might be required as part of the authentication procedure to connect to a network, is marked with “ether”. The local loop has 6 pairs of all zeros, the physical loop has 6 pairs of hexadecimal characters, of which the first 3 pairs are vendor-specific.

# 10.2.3.2 The ifconfig command

While *ip* is the most novel way to configure a Linux system, **ifconfig** is still very popular. Use it without option for displaying network interface information:

```
```
els@assus:~$ /sbin/ifconfig
eth0      Link encap:Ethernet  HWaddr 00:50:70:31:2C:14
          inet addr:60.138.67.31  Bcast:66.255.255.255  Mask:255.255.255.192
          inet6 addr: fe80::250:70ff:fe31:2c14/64  Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:31977764 errors:0 dropped:0 overruns:0 frame:0
          TX packets:51896866 errors:0 dropped:0 overruns:0 carrier:0
          collisions:8022207 txqueuelen:1000
          RX bytes:2806974916 (2.6 GiB)  TX bytes:2874632613 (2.6 GiB)
          Interrupt:11 Base address:0xec00
lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128  Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:765762 errors:0 dropped:0 overruns:0 frame:0
          TX packets:765762 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:624214573 (595.2 MiB)  TX bytes:624214573 (595.2 MiB)
```
```

Here, too, we note the most important aspects of the interface configuration:

+   * The IP address is marked with “inet addr”.
+   * The hardware address follows the “HWaddr” tag.

Both **ifconfig** and *ip* display more detailed configuration information and a number of statistics about each interface and, maybe most important, whether it is “UP” and “RUNNING”.