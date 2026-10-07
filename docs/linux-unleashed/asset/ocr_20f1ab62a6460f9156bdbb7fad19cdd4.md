This excerpt has three active TCP connections, as identified by the state ESTABL., with one that has data being sent (as shown in the Send-Q column). An asterisk means that no end point is yet associated with that address.

# # Network Interface Statistics

The behavior of the network interface (such as the network interface card) can be shown with the netstat -i option. This quickly shows administrators whether there are major problems with the network connection.

The netstat -i command displays the name of the interface, the maximum number of characters a packet can contain (MTU), the number of input packets received error free (RX-OK), number of received packets with errors (RX-ERR), number of received packets dropped (RX-DRP), and the number of packets that could not be received (RX-OVR). This is followed by the same statistics for sent packets. The following is a sample output from a netstat -i command:

```
merlin> netstat -i
 Kernel Interface table
  Iface  MTU Met   RX-OK  RX-ERR RX-DRP RX-OVR  TX-OK TX-ERR TX-DRP TX-OVR
 ⇲Flags
  lo     2000  0     0      0      0      0       12    0     0      0
 ⇲BLRU
 eth0   1500  0     218    0      0      0       144   0     0      0
 ⇲BRU
```

# # Routing Table Information

Routing tables are continually updated to reflect connections to other machines. To obtain information about the routing tables (if there are any on your system), the netstat -r option is used.

Columns show the destination machine, the address of the gateway to be used, a flag to show whether the route is active (U) and whether it leads to a gateway (G) or a machine (H for host), a reference counter (Refs) that specifies how many active connections may use that route simultaneously, the number of packets that have been sent over the route (Use), and the interface name.

```
merlin> netstat -r
 Kernel routing table
 Destination  Gateway          Genmask    Flags Metric Ref Use  ⇲Iface
 localnet     *                255.255.0.0 U     0     0    262 eth0
 loopback     *                255.0.0.0   U     0     0    12 lo
 default      *                0.0.0.0     U     0     0    0 eth0
```