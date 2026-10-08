# iptables Syntax

# BALANCE NAT TABLE TARGET EXTENSION

The BALANCE target enables a round-robin method of sending connections to more than one target host. The BALANCE target uses a range of addresses for this purpose and thus provides a rudimentary load-balancing.

The general syntax for BALANCE is as follows:

```
iptables -t nat -A PREROUTING -p tcp -j BALANCE \
--to-destination <ip address>--ip address
```

The CLUSTERIP target also provides some of these same options.



The mangle table targets and extensions apply to the OUTPUT and PREROUTING chains. Remember, the filter table is implied by default. To use the mangle table features, you must specify the mangle table with the -t mangle directive.

# mangle TABLE TARGET EXTENSION

Table 6.24 lists the target extensions available to the mangle table.

| -t mangle Option | Description |
|---|---|
| -j MARK --set-mark <value> | Sets the value of the Netfilter mark value for this packet |
| -j TOS --set-tos <value> | Sets the value in the IP header |

Table 6.24 mangle Target Extensions

There are two mangle table target extensions: MARK and TOS. MARK contains the functionality to set the unsigned long mark value for the packet maintained by the iptables mangle table.

An example of usage follows:

```
iptables -t mangle -A PREROUTING --in-interface eth0 -p tcp \
-s <src address> --sport 1024:65535 \
-d <some destination address> --dport 23 \
-j MARK --set-mark 0x000100070
```

TOS contains the functionality to set the TOS bits in the IP header.

An example of usage follows:

```
iptables -t mangle -A OUTPUT ... -j TOS --set-tos <tos>
```

The possible tos values are the same available in the filter table's TOS extension module.