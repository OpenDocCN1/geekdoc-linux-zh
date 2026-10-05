# 384 TCP/IP and Linux Protocol Implementation

```
133                               if (ciph->daddr == idaddr)
134                               updated = 1;
135                               }
136                            fib_res_put(res);
137                        }
138                    } else {
139                            ciph->daddr = ip->saddr;
140                               updated = 1;
141                    if (updated) {
142                               cksum = &icmp->checksum;
143                               /* Using tcpudp pivot tweaked. Why not? */
144                               check = cksum_tcpudp_magic(ciph->saddr, ciph->daddr, 0, 0, *(cksum)
145                        }
146                            *cksum = cksum_tcpudp_magic(\isaddr, idaddr, 0, 0, "check");
147
148                        break;
149                }
150                default:
151                    break;
152                }
153            return NET_RX_SUCCESS;
154
155    truncated:
156        /* should return NET_RX_BAD; */
157        return -EINVAL;
158    }
```

# ## 6.8 Tunnels

# ### 6.8.1 IP in IP Tunnels

**6.251** IP in IP tunnel—opening remarks: linux/net/ipv4/ipip.c.

```
29    / tunnel.c: an IP tunnel driver
30
31    The purpose of this driver is to provide an IP tunnel through
32    which you can tunnel network traffic transparently across subnets.
33
34    This was written by looking Nick Holloway's dummy driver
35    Thanks for the great code!
36
37        -Sam Latinga (alouken@cs.ucdav.edu) 02/01/95
38
39    Minor tweaks:
40    Cleaned up the code and added some pre-1.3.0 tweaks.
41    dev->hard_header/hard_header_len changed to use no headers.
42    Comments/breaking tweaked.
43    Made the tunnels use dev->name tunnel: when error reporting.
```