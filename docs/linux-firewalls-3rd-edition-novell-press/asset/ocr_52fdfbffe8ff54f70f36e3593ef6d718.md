The preceding rules are redundant if you have activated the rp_filter kernel facility. Its good practice to define the rules explicitly.

Likewise, the firewall rules drop packets that don’t contain a local source address. Regardless, it’s good practice to explicitly define a rule to implement RFC 2827, “Network Ingress Filtering: Defeating Denial of Service Attacks Which Employ IP Source Address Spoofing”:

```
IPT -A FORWARD -o $DMZ_INTERFACE \
    -s ! $LAN_ADDRESSES -j DROP
```

```
IPT -A FORWARD -i $LAN_INTERFACE \
    -s ! $LAN_ADDRESSES -j DROP
```

```
IPT -A OUTPUT -o $DMZ_INTERFACE -s ! $DMZ_IPADDR -j DROP
IPT -A OUTPUT -o $LAN_INTERFACE -s ! $LAN_IPADDR -j DROP
```

We’ll skip the rules from Chapter 4 that checked for private network source addresses. The gateway firewall is performing that function.

The next sets of rules are primarily for completeness. Both of the firewall’s default policies are to drop everything. As such, broadcast addresses are dropped by default and must be explicitly enabled when they are wanted:

```
# Refuse malformed broadcast packets
IPT -A FORWARD -i $LAN_INTERFACE -o $DMZ_INTERFACE \
    -d $BROADCAST_SRC -j DROP
```

```
IPT -A FORWARD -i $LAN_INTERFACE -o $DMZ_INTERFACE \
    -d $BROADCAST_SRC -j DROP
```

```
# Don’t forward directed broadcasts
IPT -A FORWARD -i $LAN_INTERFACE -o $DMZ_INTERFACE \
    -d $DMZ_NETWORK -j DROP
IPT -A FORWARD -i $LAN_INTERFACE -o $DMZ_INTERFACE \
    -d $DMZ_BROADCAST -j DROP
```

```
# Don’t forward limited broadcasts in either direction
IPT -A FORWARD -d $BROADCAST_DEST -j DROP
```

Multicast is always sent over UDP. Whether or not you add rules to accept incoming multicast, the following rules block illegal multicast packets:

```
IPT -A INPUT -p ! udp -d $CLASS_D_MULTICAST -j DROP
IPT -A FORWARD -p ! udp -d $CLASS_D_MULTICAST -j DROP
```