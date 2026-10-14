
overcome this by adding either the -T or -I option to the traceroute command.

## ip

The ip program is a multipurpose network configuration tool that makes use of the full range of networking features available in modern Linux kernels. It replaces the earlier and now deprecated ifconfig program. With ip, we can examine a system's network interfaces and routing table.

```
[me@linuxbox ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN
   group default
   link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
   inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
   inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP
   group default qlen 1000
   link/ether ac:22:0b:52:cf:84 brd ff:ff:ff:ff:ff:ff
   inet 192.168.1.14/24 brd 192.168.1.255 scope global eth0
       valid_lft forever preferred_lft forever
   inet6 fe80::ae22:bff:fe52:cf84/64 scope link
       valid_lft forever preferred_lft forever
```

In the preceding example, we see that our test system has two network interfaces. The first, called lo, is the loopback interface, a virtual interface that the system uses to “talk to itself,” and the second, called eth0, is the Ethernet interface.

When performing casual network diagnostics, the important things to look for are the presence of the word UP in the first line for each interface, indicating that the network interface is enabled, and the presence of a valid IP address in the inet field on the third line. For systems using Dynamic Host Configuration Protocol (DHCP), a valid IP address in this field will verify that the DHCP is working.

## netstat

The netstat program is used to examine various network settings and statistics. Through the use of its many options, we can look at a variety of features in our network setup. Using the -ie option, we can examine the network interfaces in our system.

```
[me@linuxbox ~]$ netstat -ie
eth0      Link encap:Ethernet  HWaddr 00:1d:09:9b:99:67
          inet addr:192.168.1.2  Bcast:192.168.1.255  Mask:255.255.255.0
          inet6 addr: fe80::21d:9ff:fe9b:9967/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:238488  errors:0  dropped:0  overruns:0  frame:0
          TX packets:403217  errors:0  dropped:0  overruns:0  carrier:0
          collisions:0  txqueuelen:100 
          RX bytes:153098921 (146.0 MB)  TX bytes:261035246 (248.9 MB)
          Memory:fdfc0000-fdfe0000

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:2208  errors:0  dropped:0  overruns:0  frame:0
          TX packets:2208  errors:0  dropped:0  overruns:0  carrier:0
          collisions:0  txqueuelen:0 
          RX bytes:111490 (108.8 KB)  TX bytes:111490 (108.8 KB)
```

Using the -r option will display the kernel's network routing table. This shows how the network is configured to send packets from network to network:

```
[me@linuxbox ~]$ netstat -r
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
192.168.1.0     *               255.255.255.0   U       0   0       0   eth0
default         192.168.1.1     0.0.0.0         UG      0   0       0   eth0
```

In this simple example, we see a typical routing table for a client machine on a local area network (LAN) behind a firewall/router. The first line of the listing shows the destination 192.168.1.0. IP addresses that end in zero refer to networks rather than individual hosts, so this destination means any host on the LAN. The next field, Gateway, is the name or IP address of the gateway (router) used to go from the current host to the destination network. An asterisk in this field indicates that no gateway is needed.

The last line contains the destination default. This means any traffic destined for a network that is not otherwise listed in the table. In our example, we see that the gateway is defined as a router with the address of 192.168.1.1, which presumably knows what to do with the destination traffic.

Like ip, the netstat program has many options, and we have looked only at a couple. Check out the ip and netstat man pages for a complete list.

## Transporting Files over a Network

What good is a network unless we can move files across it? There are many programs that move data over networks. We will cover two of them now and several more in later sections.

## ftp

One of the true “classic” programs, ftp gets its name from the protocol it uses, the File Transfer Protocol. FTP was once the most widely used method of downloading files over the Internet. Most, if not all, web browsers support it, and you often see URIs starting with the protocol ftp://.

Before there were web browsers, there was the ftp program. ftp is used to communicate with FTP servers, machines that contain files that can be uploaded and downloaded over a network.

FTP (in its original form) is not secure because it sends account names and passwords in cleartext. This means they are not encrypted, and anyone sniffing the network can see them. Because of this, almost all FTP done over the Internet is done by anonymous FTP servers. An anonymous server allows anyone to log in using the login name “anonymous” and a meaningless password.
