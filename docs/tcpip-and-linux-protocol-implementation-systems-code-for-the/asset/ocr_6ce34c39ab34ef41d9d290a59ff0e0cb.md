# TCP/IP and Linux Protocol Implementation

```
Figure 6.384 SIT: linux/net/ipv6/sit.c
```c
static struct ip_tunnel *ipv6_tunnel_lookup(u32 remote, u32 local)
{
    unsigned h0 = HASH(remote);
    unsigned hi = HASH(local);
    struct ip_tunnel *t;

    for (t = tunnels_r[h0]; t; t = t->next(t)) {
        if (local == t->parms.iphaddr.saddr &&
            remote == t->parms.iphaddr.saddr && (t->dev->flags&IFF_UP))
            return t;
    }

    for (t = tunnels_r[hi]; t; t = t->next(t)) {
        if (remote = t->parms.iphaddr.saddr && (t->dev->flags&IFF_UP))
            return t;
    }

    for (t = tunnels_l[hi]; t; t = t->next(t)) {
        if (local == t->parms.iphaddr.saddr && (t->dev->flags&IFF_UP))
            return t;
    }

    if ((t = tunnels_vc[0]) != NULL && (t->dev->flags&IFF_UP))
        return t;

    return NULL;
}
```
```

#  6.9.12 Effect on Transport of IPv6 of Note

In general, IPv6 has as little impact on transport and above as possible. The TCP and UDP pseudheaders for checksums have to be modified since they include parts of the IP header (including addresses). The modules linux/net/ipv6/tcp_ipv6.c and linux/net/ipv6/udp.c incorporate the relevant changes. These are relatively minor.

#  6.10 Summary

In this chapter, we looked at the implementation of the Internet infrastructure. The network is built out of links that carry IP packets. IP packets have to be framed for transmission and reception, so we looked at the Ethernet Local Area Network as an example of this, and covered a specific driver. IP addresses need to be translated into link layer addresses, so we looked at the Address Resolution Protocol. IP packets cause problems, and these must be reported from time to time, so we looked at the ICMP protocol. Penultimately, there are some things that require additional levels of encapsulation, so we looked at tunnels. Finally, IP is running out of space, so a replacement, IPv6, has been designed and implemented, so we looked at the Linux implementation of that.

In the next chapter, we look at end-to-end protocols such as TCP, UDP, and RTP, which run over this infrastructure.