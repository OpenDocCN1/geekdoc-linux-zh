```
Default Gateway . . . . . . . . : 192.168.1.1
DHCPv6 IAID . . . . . . . . . . : 167775273
DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-25-55-82-FF-00-0C-29-C1-ED-B0
DNS Servers . . . . . . . . . . : fec0:0:0:ffff::1%1
                              fec0:0:0:ffff::2%1
                              fec0:0:0:ffff::3%1
NetBIOS over Tcip. . . . . . . : Enabled
```

![](bbox=[0.21, 0.23, 0.79, 0.245])

This machine does have multiple network interfaces. Next, let's take a closer look at its routing tables.

To display the networking routing tables, we will use the route$^{654}$ command followed by the `print` argument.

```
C:\Users\Student>route print

=====================================================================

Interface List

 15...00 0c 29 c1 ed b0 ...InteI(R) 82574L Gigabit Network Connection
 4...00 0c 29 c1 ed ba ....InteI(R) 82574L Gigabit Network Connection #2
 1.............................Software Loopback Interface 1

=====================================================================

IPv4 Route Table

=====================================================================
Active Routes:
Network Destination     Netmask          Gateway          Interface      Metric
          0.0.0.0          0.0.0.0      192.168.1.1    192.168.1.111      281
          0.0.0.0          0.0.0.0        10.11.0.2       10.11.0.22      281
         10.11.0.0     255.255.255.0         On-link       10.11.0.22      281
         10.11.0.22     255.255.255.255       On-link       10.11.0.22      281
         10.11.0.255    255.255.255.255       On-link       10.11.0.22      281
          127.0.0.0         255.0.0.0       On-link       127.0.0.1       331
          127.0.0.1    255.255.255.255       On-link       127.0.0.1       331
       127.255.255.255  255.255.255.255       On-link       127.0.0.1       331
       192.168.1.0     255.255.255.0       On-link     192.168.1.111      281
       192.168.1.111   255.255.255.255       On-link     192.168.1.111      281
       192.168.1.255   255.255.255.255       On-link     192.168.1.111      281
          224.0.0.0       240.0.0.0       On-link       127.0.0.1       331
          224.0.0.0       240.0.0.0       On-link     192.168.1.111      281
          224.0.0.0       240.0.0.0       On-link       10.11.0.22      281
       255.255.255.255  255.255.255.255       On-link       127.0.0.1       331
       255.255.255.255  255.255.255.255       On-link     192.168.1.111      281
       255.255.255.255  255.255.255.255       On-link       10.11.0.22      281

=====================================================================

Persistent Routes:
Network Address        Netmask  Gateway Address       Metric
          0.0.0.0          0.0.0.0      192.168.1.1     Default
          0.0.0.0          0.0.0.0      10.11.0.2     Default
=====================================================================
```

+   $^{654}$ (Microsoft, 2015), https://docs.microsoft.com/en-us/previous-versions/windows/embedded/jj089818(v=w inemb embedded.70)