# valid_lft forever preferred_lft forever

+   - An active interface is UP.
- The link/ether line specifies the hardware (MAC) address of the device.
- The inet line specifies an IPv4 address, network prefix length, and scope.
- The inet6 line specifies an IPv6 address, its network prefix length, and scope. This address is of global scope and is normally used.
- This inet6 indicates that the interface has an IPv6 address of link scope that can only be used for communication on the local Ethernet line.

# Displaying Performance Statistics

The ip command may also be used to show statistics about network performance. Counters for each network interface can be used to identify the presence of network issues. The counters record statistics for the number of received (RX) and transmitted (TX) packets, packet errors, and packets that dropped.

```
[user@host ~]$ ip -s link show ens3
2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state qlen 1000
link/ether 52:04:00:00:00:0a br:ff:ff:ff:ff:ff
RX: packets errors dropped overrun mcast
269850 2931 0 0 0
TX: packets errors dropped carrier colisns
300556 3250 0 0 0
```

# CHECKING CONNECTIVITY BETWEEN HOSTS

The ping command is used to test connectivity. The command continues to run until Ctrl+C is pressed unless options are given to limit the number of packets sent.

```
[user@host ~]$ ping -c 3 192.0.2.254
PING 192.0.2.254 (56) 64 bytes of data.
64 bytes from 192.0.2.254: icmp_seq=1 ttl=64 time=43.33 ms
64 bytes from 192.0.2.254: icmp_seq=2 ttl=64 time=3.48 ms
64 bytes from 192.0.2.254: icmp_seq=3 ttl=64 time=6.83 ms
-
192.0.2.254 ping statistics
3 packets transmitted, 3 received, 0% packet loss, time 203ms
rtt min/avg/max/mdev = 3.485/4.886/6.837/1.424 ms
```

The ping command is the ipv6 version of ping in Red Hat Enterprise. It operates over IPv6 and takes IPv6 addresses, but otherwise work like ping.

```
[user@host ~]$ ping 6 2001:db8:0:1::1 56 data bytes
PING 2001:db8:0:1::1(2001:db8:0:1::1) 56 bytes of data
64 bytes from 2001:db8:0:1::1: icmp_seq=1 ttl=64 time=18.4 ms
64 bytes from 2001:db8:0:1::1: icmp_seq=2 ttl=64 time=0.178 ms
64 bytes from 2001:db8:0:1::1: icmp_seq=3 ttl=64 time=0.100 ms
^C
-\2001:db8:0:1::1 ping statistics
3 packets transmitted, 3 received, 0% packet loss, time 201ms
```