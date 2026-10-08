
If you are designing a firewall that is meant to protect your local network from any attempts to penetrate it from an outside network, you may want to restrict packets coming in. Simply denying access by all packets is unfeasible because users connected to outside servers—say, on the Internet—must receive information from them. You can, instead, deny access by a particular kind of packet used to initiate a connection. The idea is that an attacker must initiate a connection from the outside. The headers of these kinds of packets have their SYN bit set on and their FIN and ACK bits empty. The state module's NEW state matches on any such SYN packet. By specifying a DROP target for such packets, you deny access by any packet that is part of an attempt to make a connection with your system. Anyone trying to connect to your system from the outside is unable to do so. Users on your local system, who have initiated connections with outside hosts can still communicate with them. The following example will drop any packets trying to create a new connection on the `eth0` interface, though they will be accepted on any other interface:

```
iptables -A INPUT -m state --state NEW -i eth0 -j DROP
```

You can use the ! operator on the `eth0` device combined with an ACCEPT target to compose a rule that will accept any new packets except those on the **eth0** device. If the **eth0** device is the only one that connects to the Internet, this still effectively blocks outside access. At the same time, input operation for other devices such as our localhost are free to make new connections. This kind of conditional INPUT rule is used to allow access overall with exceptions. It usually assumes that a later rule such as a chain policy will drop remaining packets.

```
iptables -A INPUT -m state --state NEW ! -i eth0 -j ACCEPT
```

The next example will accept any packets that are part of an established connection or related to such a connection on the `eth0` interface:

```
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
```

> **TIP** You can use the `iptables` tool to display the current state table.

## Specialized Connection Tracking: ftp, irc, Amanda, tftp

To track certain kinds of packets, Iptables uses specialized connection tracking modules. These are optional modules that you have to load manually. To track passive FTP connections, you would have to load the `ip_conntrack_ftp` module. To add NAT table support, you would also load the `ip_nat_ftp` module. For IRC connections, you use `ip_conntrack_irc` and `ip_nat_irc`. There are corresponding modules for Amanda (the backup server) and TFTP (Trivial FTP).

To have these modules loaded automatically by the Red Hat Fedora iptables service script, you have to list them in the `IPTABLES_MODULE` parameter in the `/etc/sysconfig/iptables-config` file. For example, the following assignment adds support for both FTP and Amanda:

```
IPTABLES_MODULES="ip_conntrack, ip_conntrack_ftp, ip_nat_ftp, ip_conntrack_amanda, ip_nat_amanda"
```

If you were writing your own iptables script, instead of using the service iptables script, you would have to add modprobe commands to load the modules.

```
modprobe ip_conntrack ip_conntrack_ftp ip_nat_ftp
modprobe ip_conntrack_amanda ip_nat_amanda
```

## Network Address Translation (NAT)

Network address translation (NAT) is the process whereby a system will change the destination or source of packets as they pass through the system. A packet will traverse several linked systems on a network before it reaches its final destination. Normally, they will simply pass the packet on. However, if one of these systems performs a NAT on a packet, it can change the source or destination. A packet sent to a particular destination could have its destination address changed. To make this work, the system also needs to remember such changes so that the source and destination for any reply packets are altered back to the original addresses of the packet being replied to.

NAT is often used to provide access to systems that may be connected to the Internet through only one IP address. Such is the case with networking features such as IP masquerading, support for multiple servers, and transparent proxying. With IP masquerading, NAT operations will change the destination and source of a packet moving through a firewall/gateway linking the Internet to computers on a local network. The gateway has a single IP address that the other local computers can use through NAT operations. If you have multiple servers but only one IP address, you can use NAT operations to send packets to the alternate servers. You can also use NAT operations to have your IP address reference a particular server application such as a Web server (transparent proxy). NAT tables are not implemented for iptables.

### Adding NAT Rules

Packet selection rules for NAT operations are added to the NAT table managed by the iptables command. To add rules to the NAT table, you have to specify the NAT table with the -t option. Thus, to add a rule to the NAT table, you would have to specify the NAT table with the -t nat option as shown here:

```
iptables -t nat
```

With the -L option, you can list the rules you have added to the NAT table:

```
iptables -t nat -L -n
```

Adding the -n option will list IP addresses and ports in numeric form. This will speed up the listing, as iptables will not attempt to do a DNS lookup to determine the hostname for the IP address.

### Nat Targets and Chains

In addition, there are two types of NAT operations: source NAT, specified as SNAT target, and destination NAT, specified as DNAT target. SNAT target is used for rules that alter source addresses, and DNAT target, for those that alter destination addresses.

Three chains in the NAT table are used by the kernel for NAT operations. These are **PREROUTING**, **POSTROUTING**, and **OUTPUT**. PREROUTING is used for destination NAT (DNAT) rules. These are packets that are arriving. POSTROUTING is used for source NAT (SNAT) rules. These are for packets leaving. OUTPUT is used for destination NAT rules for locally generated packets.

As with packet filtering, you can specify source (**-s**) and destination (**-d**) addresses, as well as the input (**-i**) and output (**-o**) devices. The -j option will specify a target such as MASQUERADE. You would implement IP masquerading by adding a MASQUERADE rule to the POSTROUTING chain:

```
# iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

To change the source address of a packet leaving your system, you would use the POSTROUTING rule with the SNAT target. For the SNAT target, you use the **--to-source** option to specify the source address:

```
# iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source 192.168.0.4
```

To change the destination address of packets arriving on your system, you would use the PREROUTING rule with the DNAT target and the **--to-destination** option:

```
# iptables -t nat -A PREROUTING -i eth0 \
-j DNAT --to-destination 192.168.0.3
```

Specifying a port lets you change destinations for packets arriving on a particular port. In effect, this lets you implement port forwarding. In the next example, every packet arriving on port 80 (the Web service port) is redirected to 10.0.0.3, which in this case would be a system running a Web server.

```
# iptables -t nat -A PREROUTING -i eth0 -dport 80 \
-j DNAT --to-destination 10.0.0.3
```

With the TOS and MARK targets, you can mangle the packet to control its routing or priority. A TOS target sets the type of service for a packet, which can set the priority using criteria such as normal-service, minimize-cost, or maximize-throughput, among others.

The targets valid only for the NAT table are shown here:

| Target | Description |
| :--- | :--- |
| SNAT | Modify source address, use --to-source option to specify new source address. |
| DNAT | Modify destination address, use --to-destination option to specify new destination address. |
| REDIRECT | Redirect a packet. |
| MASQUERADE | IP masquerading. |
| MIRROR | Reverse source and destination and send back to sender. |
| MARK | Modify the Mark field to control message routing. |
