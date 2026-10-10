# Resetting (Zeroing) Counters

It is useful to be able to reset the counters. This can be done with the -Z (zero counters) option. For example:

```
# ipchains -v -L input
Chain input (refcnt = 1): (policy ACCEPT)
pkts bytes target     prot opt tos      tos
10 840 ACCEPT    icmp ------ 0xFF 0x00
ifname mark source      destination ports
lo       anywhere anywhere any

# ipchains -Z input
# ipchains -v -L input
Chain input (refcnt = 1): (policy ACCEPT)
pkts bytes target     prot opt tos      tos
0    0 ACCEPT    icmp ------ 0xFF 0x00
ifname mark source      destination ports
lo       anywhere anywhere any
#
```

The problem with this approach is that sometimes you need to know the counter values immediately before they are reset. In the previous example, some packets could pass through between the -L and -Z commands. For this reason, you can use the -L and -Z together, to reset the counters while reading them. Unfortunately, if you do this you can't operate on a single chain; you have to list and zero all the chains at once.

```
# ipchains -L -v -Z
Chain input (policy ACCEPT):
pkts bytes target     prot opt tos      tos
10 840 ACCEPT    icmp ------ 0xFF 0x00
ifname mark source      destination ports
lo       anywhere anywhere any

Chain forward (refcnt = 1): (policy ACCEPT)
Chain output (refcnt = 1): (policy ACCEPT)
Chain test (refcnt = 0):
0 0 DENY     icmp ------ 0xFF 0x00  ppp0
0 localNet/24          anywhere     any
# ipchains -L -v
Chain input (policy ACCEPT):
pkts bytes target     prot opt tos      tos
10 840 ACCEPT    icmp ------ 0xFF 0x00
ifname mark source      destination ports
lo       anywhere anywhere any

Chain forward (refcnt = 1): (policy ACCEPT)
Chain output (refcnt = 1): (policy ACCEPT)
```