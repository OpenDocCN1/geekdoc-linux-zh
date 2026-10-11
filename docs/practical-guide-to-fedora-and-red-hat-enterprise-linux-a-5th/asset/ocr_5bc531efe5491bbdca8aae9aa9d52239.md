accepted by this rule. Packets that are not accepted pass to the next rule in the FORWARD chain.

The second command puts the second rule in the FORWARD chain of the Filter table:

```
# iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT
```

To match this rule, a packet must be

+   1.  Received on**eth1** (coming in from the LAN): `-i eth1`.
+   2.  Going to be sent out on**eth0** (going out to the Internet): `-o eth0`.

The kernel accepts packets that meet these two criteria, which means that all packets that originate locally and are going to the Internet are accepted. Accepted packets pass to the next appropriate chain/table. Packets that are not accepted pass to the next rule in the FORWARD chain.

The third command puts the third rule in the FORWARD chain of the Filter table:

```
# iptables -A FORWARD -j LOG
```

Because this rule has no match criteria, it acts on all packets it processes. This rule’s action is to log packets—that is, it logs packets from the Internet that attempt to create a new connection.

Packets that get to the end of the FORWARD chain of the Filter table are done with the rules set up by**iptables** and are handled by the local TCP stack. Packets from the Internet that attempt to create a new connection on the router system are accepted or returned, depending on whether the service they are trying to connect to is available on the router system.

The fourth command puts the first rule in the POSTROUTING chain of the NAT table. Only packets that are establishing a new connection are passed to the NAT table. Once a connection has been set up for SNAT or MASQUERADE, the headers on all subsequent ESTABLISHED and RELATED packets are altered the same way as the first packet. Packets that are sent in response to these packets automatically have their headers adjusted so that they return to the originating local system.

```
# iptables -t NAT -A POSTROUTING -o eth0 -j MASQUERADE
```

To match this rule, a packet must be

+   1.  Establishing a new connection (otherwise it would not have come to the NAT table).
+   2.  Going to be sent out on**eth0** (going out to the Internet): `-o eth0`.

The kernel MASQUERADEs all packets that meet these criteria. In other words, all locally originating packets that are establishing new connections have their source address changed to the address that is associated with**eth0** (10.255.255.255 in the example).