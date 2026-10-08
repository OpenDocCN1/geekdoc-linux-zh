With the deny-by-default policy and the firewall rules explicitly accepting packets based in part by matching on destination address, neither of these directed broadcast messages will be accepted by the firewall. These rules become more critical in larger setups in which the LAN uses real-world addresses.

With the use of variable-length network prefixes, a site's network and host fields may or not fall on a byte boundary. For the sake of simplicity, the SUBNET_BASE is your network address, such as 192.168.1.0. The SUBNET_BROCAST is your network's broadcast address, as in 192.168.1.255.

As just with directed broadcast messages, limited broadcasts, confined to your local network segment, are likewise not accepted with the deny-by-default policy and the firewall rules explicitly accepting packets based in part by matching on destination address. Again, the following rule becomes more critical in larger setups in which the LAN uses real-world addresses:

```
# Refuse limited broadcasts
IPT -INPUT -i $ETHERNET -d $BROCAST_DEST -j DROP
```

It should be noted that an exception must be made in later chapters for DHCP clients. Broadcast source and destination addresses are used between the DHCP client and server ports initially.

Multicast addresses are legal only as destination addresses. The next rule spoofed multicast network packets:

```
# Refuse Class D multicast addresses
# illegal as a source address
IPT -A INPUT -i $ETHERNET -s $CLASS_D_MULTICAST -j DROP
```

Legitimate multicast packets are always UDP packets. As such, multicast messages are point-to-point, just as any other UDP message. The difference between unicast and multicast packets is the class of destination address used (and the protocol flag carried in the Ethernet header). The next rule denies multicast packets carrying a non-UDP protocol:

```
IPT - INPUT -i $ETHERNET -p udp -d $CLASS_D_MULTICAST -j DROP
```

Multicast functionality is a configurable option when you compile the kernel, and your network interface card can be initialized to recognize multicast addresses. The functionality is enabled in the default kernel from many newer distributions of Linux. You might want to enable these addresses if you subscribe to a multicast conferencing service that provide audio and video broadcasts. (Multicast is also sometimes used on the local network for resource discovery, such as DHCP or routing.)

You won't generally see destination addresses unless you've registered yourself as a recipient. Multicast packets are sent to multiple, specific, targets by prior arrangement. If you send multicast packets out from machines on ISP's local subnet, however, the default policy drops multicast packets, even if you have registered as a recipient. You have to define a rule to accept the multicast address. The next rule allows incoming multicast packets for the sake of completeness:

```
IPT -A INPUT -i $ETHERNET -p udp -d $CLASS_D_MULTICAST -j ACCEPT
```