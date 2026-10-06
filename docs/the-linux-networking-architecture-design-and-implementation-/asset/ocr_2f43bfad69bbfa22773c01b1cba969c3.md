# 21.2 Configuring NAT 45

![](bbox=[0.125, 0.065, 0.905, 0.435])

FIGURE 21–2
Netfilter hooks used by the NAT module.

functionality was fully integrated in the iptables tool. iptables can be used to specify rules that control the behavior of the NAT module. As was described in Section 19.2.1., a rule consists of a set of criteria to select session flows (matching rule) and a second part specifying how a session flow should be transformed (binding type or matching type). The IP source and destination addresses, the transport protocol, the port numbers, and the protocol-specific flags.

Criteria identical to packet-filter rules are available to select session flows: the second part of a NAT rule defines how a session flow should be transformed. To this end, there are additional branch destinations, which are valid in the NAT table. We use -j SNAT to translate the source address (source NAT) and -j DNAT to translate the destination address (destination NAT). In addition, we have to use --source and --to-destination to specify a range of IP addresses and port numbers, for the address-translation process.

The selection criteria of the source NAT rule are applied to the original packet-information in the event that the destination address has already been changed by the destination NAT at that point. There are additional branch destinations (e.g., -j MASQUERADE in the Linux 2.2 style) for special cases.

In the example discussed in Section 21.1.6, where source NAT is used to map the internal addresses from the private address range 192.168.1.0–192.168.1.255 to the global address 199.10.42.1, the corresponding iptables invocation would have the following form:

```
iptables -t nat -A POSTROING -s 192.168.1.0/24 \
-j SNAT --to-source 199.10.42.1
```