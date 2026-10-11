Command **ip** can be used to show the Layer 2 information, the IP address, and the network mask. Adding the argument *address* (or *a*) shows the assigned addresses for the interface, as *figure 7.6* illustrates:

```
```
root@ubuntu:~# ip --color=auto address
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
        valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
        valid_lft forever preferred_lft forever
2: enp1s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 52:54:00:ce:80:b8 brd ff:ff:ff:ff:ff:ff
    inet 192.168.122.101/24 metric 100 brd 192.168.122.255 scope global dynamic enp1s0
        valid_lft 3414sec preferred_lft 3414sec
    inet6 fe80::5054:ff:ce:8bb8/64 scope link
        valid_lft forever preferred_lft forever
3: enp50: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default qlen 1000
    link/ether 52:54:00:07:3a:f8 brd ff:ff:ff:ff:ff:ff
```
```

![](bbox=[0.31, 0.35, 0.7, 0.38])

The interface *lo* has always assigned and configured the IP 127.0.0.1 with the network mask 255.0.0.0 (/8). The preceding *figure 7.6*, shows an interface named *enp1s0* configured with the IP 192.168.122.101 with the netmask 255.255.255.0 (/24), and the *broadcast IP* is 192.168.122.255.

The interface named *enp1s0* has an assigned IPv6 local address (starting with *fe80*) with a subnet mask /64. *Figure 7.7* shows an example of an interface with an IPv6 address configured:

```
```
root@lab:~# ip --color -6 address show dev eth0
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 st1de UP qlen 1000
    inet6 2001:41d0:1:ee26::1/128 scope global
        valid_lft forever preferred_lft forever
    inet6 fe80::225:90ff:fe22:424a/64 scope link
        valid_lft forever preferred_lft forever
```
```

![](bbox=[0.25, 0.66, 0.78, 0.69])

# Network layer (Layer 3)

Layer 3 requires to have information on how to access networks that are not the local ones. This includes a default gateway to access outside of the network, and specific gateways to access to other networks if needed. The command **ip** with the argument *route* lists the current table of destinations and gateways. *Figure 7.8* shows an example:

```
```
root@ubuntu:~# ip --color route
default via 192.168.122.1 dev enp1s0 proto dhcp src 192.168.122.101 metric 100
192.168.122.0/24 dev enp1s0 proto kernel scope link src 192.168.122.101 metric 100
```
```