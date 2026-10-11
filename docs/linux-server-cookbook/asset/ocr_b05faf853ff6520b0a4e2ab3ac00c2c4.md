*Figure 7.8: Output example for the command ip route*

In the example shown in figure 7.8, the default gateway is 192.168.122.1. It would be used as a hop for all communications whose destination is not 192.168.22.0/24. In case the communication is to an IP in the local network, the gateway is not involved, and the communication is direct. Figure 7.9 shows an example of IPv6:

```
```
root@lab:~# ip --color -6 route
2001:41d0:1:ee26::1 dev eth0 proto kernel metric 256 pref medium
2001:41d0:1:eef::ff:ff:ff:ff dev eth0 metric 1024 pref medium
fe80::/64 dev eth0 proto kernel metric 256 pref medium
default via 2001:41d0:1:eef::ff:ff:ff:ff dev eth0 metric 1024 pref medium
```
```

*Figure 7.9: Output example for the command ip route with IPv6*

The command ip route allows a useful extra argument called get and the IP to obtain the information on how to access it. Figure 7.10 shows two examples, the first one about an IP outside of the network and the second one about an IP in the local network:

```
```
root@ubuntu:~# ip --color route get 8.8.8.8
8.8.8.8 via 192.168.122.1 dev enp1s0 src 192.168.122.101 uid 0
  cache
root@ubuntu:~# ip --color route get 192.168.122.241
192.168.122.241 dev enp1s0 src 192.168.122.101 uid 0
  cache
```
```

*Figure 7.10: Output example for the command ip route get*

As described in Chapter 6, Monitoring System Resources, there are several tools to check the traffic hops from the system to a destination IP, such as traceroute, tracempath, or mtr. The protocol Internet Control Message Protocol (ICMP) is located in Layer 3; this protocol is used by the commands mentioned previously and by the popular command ping. This command is useful to check connectivity to local and remote IPs.

# ## Transport layer (Layer 4)

This layer depends on protocols for the transmission of data. The transport protocols can be stateful, for example, Transmission Control Protocol (TCP), or stateless such as User Datagram Protocol (UDP). The stateful connection ensures that the data is sent correctly and waits for the transmission to be completed. An example of a stateful connection is an HTTP request. A stateless