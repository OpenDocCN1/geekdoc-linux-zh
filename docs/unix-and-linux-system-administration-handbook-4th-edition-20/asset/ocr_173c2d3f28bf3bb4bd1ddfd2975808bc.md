# IPFilter for UNIX systems

inbound traffic is permitted to the 10.0.0.0/24 network on TCP ports 80 and 443 and on UDP port 53.

```
block out quick all
pass in quick proto tcp from any to 10.0.0.0/24 port = 80 keep state
pass in quick proto tcp from any to 10.0.0.0/24 port = 443 keep state
pass in quick proto udp from any to 10.0.0.0/24 port = 53 keep state
block in all
```

The state key deserve special attention. IPFilter keeps track of connections by noting the first packet of new sessions. For example, a new packet arrives addressed to port 80 on 10.0.0.10, IPFilter makes an entry in the state table and allows the packet through. It also allows the reply from the web server though the first rule explicitly blocks all traffic.

keep state is also useful for devices that offer no services but must initiate connections. The however ruleset permits all conversations that are initiated by 192.168.10.10. It blocks all inbound packets except those related to connections that have been initiated.

```
block in quick
pass out quick from 192.168.10.10/32 to any keep state
```

The state keywords work for UDP and ICMP packets, too but since these protocols are stateless, the mechanics are slightly more ad hoc:IPFilter permits responses to a UDP or an ICMP packet for 60 seconds after the inbound packet is seen by the filter. For example, if a UDP packet from 10.0.0.10, port 32000, is addressed to 192.168.10.10, port 53, a UDP reply will be permitted until 60 seconds have passed. Similarly, an ICMP echo reply (ping response) is permitted after an echo request has been entered in the state table.

Network address translation (NAT) is another feature offered by IPFilter. NAT lets a large network with RFC1918 private IP addresses connects to the Internet through a small set of Internet-routable IP addresses. The NAT device maps private network to one or more public addresses, sends requests across the Internet, and intercepts the responses and rewrites them in terms of the IP addresses.

IPFilter uses the map keyword (in place of pass and block) to provide NAT services. In the following rule, the 10.0.0.0/24 network is mapped to the current address on the e1000g interface.

```
map e1000g 10.0.0.0/24 -> 0/32
```

The filter must be reloaded if the address of e1000g changes, as might happen if e1000g leases a dynamic IP address through DHCP. For this reason, IPFilter's NAT features are best used at sites that have a static IP address on the Internetfacing interface.

See page 462 for more information about private addresses and NAT.