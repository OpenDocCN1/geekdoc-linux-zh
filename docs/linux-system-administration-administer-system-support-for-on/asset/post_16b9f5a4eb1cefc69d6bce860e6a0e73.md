
Request for Comments; these white papers define the Internet standards. You can find RFC 1918 at http://info.internet.isi.edu/in-notes/rfc/files/rfc1918.txt and its valid Internet network address is 158.92.200.0.

To delete a route, issue the following command:

```
# route del -net 192.92.200.0
```

You don't need to include the netmask because it's a Class C address. If you want to add a route, use the following command:

```
# route add -net 156.92.200.0 netmask 255.255.255.0 dev eth1
```

Because the new address isn't Class C and we're using a Class C netmask, include a Class C netmask. You should also specify the device, especially if you have more than one Ethernet card.

If you configure the Ethernet card, use the ifconfig command. If you run ifconfig by itself, it will display the current network interface status.

```
# ifconfig eth1
eth1
    Link encap:Local Loopback
    inet addr:156.92.200.8  Bcast:156.92.200.255  Mask:255.255.255.0
    UP BROADCAST  ETHENETO  RUNNING  MTU:3584  Metric:1
    RX packets:323310 errors:0 dropped:0 overruns:0 frame:0
    TX packets:323310 errors:0 dropped:0 overruns:0 carrier:0 coll:0
```

You shouldn't need to configure Ethernet cards with ifconfig. With ifconfig, you can reconfigure the address on a card, activate and deactivate it, and define its netmask as well as other network information. The ifconfig command is great for troubleshooting the status of a network card.

If you want to see all the networking information at once, use the netstat command. The netstat command displays the connections, routing tables, link information, interface information, and masqueraded connections.

If you want to see everything, type netstat -a, as shown in Listing 11-4. Otherwise, you can specify any of the individual information you want to see.

### Listing 11-4: Using netstat -a

```
# netstat -a
Active Internet connections (including servers)
Proto  Recv-Q Send-Q Local Address   Foreign Address   State
tcp        0      0 *:sunrpc        *:*             LISTEN
tcp        0      0 *:time          *:*             LISTEN
tcp        0      0 *:ftp           *:*             LISTEN
tcp        0      0 *:telnet        *:*             LISTEN
tcp        0      0 *:shell         *:*             LISTEN
tcp          0 0 *:login                 *:*                        LISTEN
tcp          0 0 *:pop3                  *:*                        LISTEN
tcp          0 0 *:imap2                 *:*                        LISTEN
tcp          0 0 *:finger                *:*                        LISTEN
tcp          0 0 *:systat                *:*                        LISTEN
tcp          0 0 *:netstat               *:*                        LISTEN
tcp          0 0 *:auth                  *:*                        LISTEN
tcp          0 0 *:printer               *:*                        LISTEN
tcp          0 0 *:711                   *:*                        LISTEN
tcp          0 0 *:2049                  *:*                        LISTEN
tcp          0 0 *:smtp                  *:*                        LISTEN
tcp          0 0 *:www                   *:*                        LISTEN
udp          0 0 *:sunrpc                *:*                        
udp          0 0 *:syslog                *:*                        
udp          0 0 *:time                  *:*                        
udp          0 0 *:biff                  *:*                        
udp          0 0 *:ntalk                 *:*                        
udp          0 0 *:708                   *:*                        
udp          0 0 *:2049                  *:*                        
raw          0 0 *:1                     *:*

Active UNIX domain sockets (including servers)

Proto RefCnt Flags      Type    State    I-Node Path
unix 2    [ ]          STREAM CONNECTED  486
unix 1  [ ACC ]        STREAM LISTENING 499   /dev/log
unix 1  [ ACC ]        STREAM LISTENING 527   /dev/printer
unix 2    [ ]          STREAM CONNECTED 533
unix 2    [ ]          STREAM CONNECTED 534   /dev/log
unix 2    [ ]          STREAM CONNECTED 553
unix 2    [ ]          STREAM CONNECTED 554   /dev/log
unix 2    [ ]          STREAM CONNECTED 812
unix 2    [ ]          STREAM CONNECTED 813   /dev/log
unix 2    [ ]          STREAM CONNECTED 816   /dev/log
unix 2    [ ]          STREAM CONNECTED 826
unix 1  [ ACC ]        STREAM LISTENING 841   /var/run/gpmctl
```

When you have your network connectivity working, you can use the traceroute command to determine how you would get from your address to another address on the network. You can see how many hops it takes and what addresses it hits along the way.

```
# traceroute www.yahoo.com
traceroute to www9.yahoo.com (204.71.200.74), 30 hops max, 40 byte packets
 1 core1-fe8-1-0.mv.best.net (206.184.139.129)  3.406 ms   0.685 ms   0.510 ms
 2 so-0-l.br1.NUO.globalcenter.net (206.251.0.89)  2.253 ms   2.163 ms   2.124 ms
 3 fe5-1.cr1.NUO.globalcenter.net (206.251.1.33)  28.193 ms  2.663 ms   2.759 ms
 4 pos0-0.wr1.NUO.globalcenter.net (206.251.0.122) 2.541 ms 2.404 ms 2.318 ms
 5 pos1-0C12.wr1.SNV.globalcenter.net (206.251.0.74) 3.808 ms 3.880 ms 2.908 ms
 6 pos5-0.cr1.SNV.globalcenter.net (206.251.0.105) 3.684 ms 3.544 ms 5.642 ms
 7 www9.yahoo.com (204.71.200.74) 3.604 ms 3.321 ms 3.268 ms
```

## Linux Firewalls

Because Linux can handle multiple network interface cards (NICs), it can also work as a firewall. Linux does come with its own built-in firewall: `ipfw`, `ipfwadm`, and `xfw`.

![](img/8ad518fddafc7f5e73715a2604b61d50_390_0.png)

### Listing 11-5: Viewing routing information in /proc/net

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

With the Linux firewall, you can filter traffic, set up a proxy, or use IP masquerading. Masquerading is hiding invalid IP addresses behind a valid one. This hides your network addressing from the rest of the world.

Because the firewall capabilities must be compiled in the kernel, you have to turn on the firewall option just like you would to tell Slackware Linux to act more like a router than a host. The interface for the firewall administration is the *ipfwadm* command.

For accounting, pass the -A option. You can specify input, output, or both on what type of rule sets should be counted. The default is both, and provided you have the hard space, you’ll probably want to keep both if you’re not the only user on your Slackware system.

```
# ipfwadm -A command parameters [firewall options] (accounting)
```

For input or output rules, you’ll need to specify -I or -O respectively. These rules are defined to accept, deny, or reject. Reject is letting the user know that the packet was not allowed; deny does not tell the user that the packet was not allowed in.

```
# ipfwadm -I command parameters [firewall options] (input)
# ipfwadm -O command parameters [firewall options] (output)
```

Two more steps you can take with the firewall include forwarding IP addresses (a routing function, actually) and masquerading those addresses.

```
# ipfwadm -F command parameters [firewall options] (forwarding)
```

This means the firewall decides where the packet goes. Basically the firewall becomes a traffic cop with the -M option.

```
# ipfwadm -M [ -i | -s ] [firewall options] (masquerading)
```

This all hides your internal network addresses (especially if you’re using illegal addresses as in RFC 1918) from the outside. This enables many invalid IP addresses to use one valid IP address for Internet connectivity.

Firewall files are stored in */proc/net*. They are *ip_output*, *ip_forward*, and *ip_masquerade*. These files maintain the rule bases for IP forwarding, IP masquerading, and IP output.

## Dial-Up Connections

Linux has two means of networking: modems and NIC, or Network Interface Card. Because more people are connecting to an Internet Service Provider (ISP) or corporate networks through modems, you need to understand how Slackware Linux
