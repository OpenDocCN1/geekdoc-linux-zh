ppp0 interface are masqueraded as coming from this host. Remember that forward rules are also necessary in these cases.

# # mangle Table Listing Formats

The basic format of the mangle table list command to list all rules on the mangle table chains is as follows:

```
```
iptables -t mangle -vn -L PREROUTING
iptables -t mangle -vn -L OUTPUT
```
```

or

```
```
iptables -t mangle -vn -L
```
```

Notice that the preceding list commands show only the rules in the mangle table chains.

What follows are two sample mangle table rules, a MARK rule on the PREROUTING chain and a TOS rule on the OUTPUT chain. In the interest of brevity, only the -v output is presented:

```
```
> iptables -t mangle -v -L
```
```

|   | Chain                  |  pkts |  bytes | target | prot | opt  | in | out | source |
|---|------------------------|-------|--------|--------|------|------|----|-----|--------|
| 1 | PREROUTING (policy DROP 0 packets, 0 bytes) | | | | | | | | \
| 2 | | | | | | | | | \
| 3 | | 0 | 0 | MARK | tcp | -- | eth0 | any | laptop.private.lan | \
| | anywhere | | | | | | spts:1024:65535 dpt:ssh MARK set 0x10070 | | |

|   | Chain                  |  pkts |  bytes | target | prot | opt  | in | out | source |
|---|------------------------|-------|--------|--------|------|------|----|-----|--------|
| 4 | OUTPUT (policy DROP 0 packets, 0 bytes) | | | | | | | | \
| 5 | | | | | | | | | \
| 6 | | 0 | 0 | TOS | tcp | -- | any | eth1 | bastion.firewall.lan | \
| | anywhere | | | | | | spts:1024:65535 dpt:ssh TOS set Minimize-Delay | | |

Line 1 identifies the listing as being for the PREROUTING chain, the point where MANGLE is applied. The PREROUTING chain's default policy is DROP.

Line 2 contains these column headings:

+   *   pkts is the number of packets that have matched the rule.
+   *   bytes is the number of bytes contained in the packets matching the rule.
+   *   target refers to the target disposition of a packet matching the rule MARK or TOS.
+   *   prot is an abbreviation for protocol, which can be all, tcp, udp, or icmp, as well as a value from /etc/protocols.