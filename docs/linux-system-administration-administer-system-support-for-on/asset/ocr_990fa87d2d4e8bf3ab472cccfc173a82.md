# # Linux Firewalls

Because Linux can handle multiple network interface cards (NICs), it can also work as a firewall. Linux does come with its own built-in firewall: `ipfw`, `ipfwadm`, and `xfw`.

![](bbox=[0.06, 0.45, 0.62, 0.82])

**Listing 11-5: Viewing routing information in /proc/net**

```
# ls -1 /proc/net
total 0
-r--r--r-- 1 root root 0 Jul 23 17:42 arp
-r--r--r-- 1 root root 0 Jul 23 17:42 dev
-r--r--r-- 1 root root 0 Jul 23 17:42 igmp
-r--r--r-- 1 root root 0 Jul 23 17:42 ip_auto-fw
-rw-r--r-- 1 root root 0 Jul 23 17:42 ip_forward
-rw-r--r-- 1 root root 0 Jul 23 17:42 ip_input
-r--r--r-- 1 root root 0 Jul 23 17:42 ip_masq-app
-r--r--r-- 1 root root 0 Jul 23 17:42 ip_masq-ade
-rw-r--r-- 1 root root 0 Jul 23 17:42 ip_output
-rw-r--r-- 1 root root 0 Jul 23 17:42 raw
-r--r--r-- 1 root root 0 Jul 23 17:42 route
-r--r--r-- 1 root root 0 Jul 23 17:42 rt-Cache
-r--r--r-- 1 root root 0 Jul 23 17:42 snmp
-r--r--r-- 1 root root 0 Jul 23 17:42 sockstat
-r--r--r-- 1 root root 0 Jul 23 17:42 tcp
-r--r--r-- 1 root root 0 Jul 23 17:42 udp
-r--r--r-- 1 root root 0 Jul 23 17:42 unix
```

In addition to network addresses, your Slackware system also has a hardware address associated with the network card. This is a MAC address. If you want to map an IP address to a MAC address, use the Address Resolution Protocol (ARP). There also is a Reverse ARP (RARP), which maps the MAC address to the IP address.

On Slackware Linux, there are two different commands to help manipulate ARP and RARP: they are `arp` and `rarp`. These can be important if you’re using a NIC for a host or routing; however, for dialup connections, you don’t need to worry about this.

A good portion of the routing information is located in /proc/net, shown in Listing 11-5. This file contains routing, IP, device, and protocol information for the previous commands and other configurations.

```
4 pos0-0.wr1.NUO.globalcenter.net (206.251.0.122) 2.541 ms 2.404 ms 2.318 ms
5 pos1-0-0C12.wr1.SNV.globalcenter.net (206.251.0.74) 3.808 ms 3.880 ms
2.908 ms
6 pos5-0.cr1.SNV.globalcenter.net (206.251.0.105) 3.684 ms 3.544 ms 5.642 ms
7 www9.yahoo.com (204.71.200.74) 3.604 ms 3.321 ms 3.268 ms
```