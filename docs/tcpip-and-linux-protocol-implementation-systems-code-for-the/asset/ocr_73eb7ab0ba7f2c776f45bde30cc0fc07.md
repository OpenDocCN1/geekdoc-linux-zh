```
struct ipv6hdr {
    if defined(__LITTLE_ENDIAN_BITFIELD)
        __u8 priority:4,
        __u8 version:4;
    elif defined(__BIG_ENDIAN_BITFIELD)
        __u8 version:4,
        __u8 priority:4;
    else
#error "Please fix <asm/byteorder.h"
    __u8 flow_lbl[3];
    __u16 payload_len;
    __u8 nexthdr;
    __u8 hop_limit;
    struct in6_addr saddr;
    struct in6_addr daddr;
};
```

# IPv6 interface header definitions for the INET address family:

Figure 6.321 Next header types: linux/include/net/ipv6.h.

```
#define SIN6_LEN_RPC 2133 24
/*
 * NextHeader field of IPv6 header
 */
#define NEXTHDR_HOP 0      /* Hop-by-hop option header. */
#define NEXTHDR_TCP 6      /* TCP segment. */
#define NEXTHDR_UDP 17     /* UDP message. */
#define NEXTHDR_IPV6 41    /* IPv6 in IPv6 */
#define NEXTHDR_ROUTING 43  /* Routing header. */
#define NEXTHDR_FRAGMENT 44 /* Fragmentation/reassembly header. */
#define NEXTHDR_EST 50     /* Encapsulating security payload. */
#define NEXTHDR_AUTH 51   /* Authentication header. */
#define NEXTHDR_ICMP 58   /* ICMP for IPv6. */
#define NEXTHDR_NONE 59   /* No next header */
#define NEXTHDR_DEST 60   /* Destination options header. */
#define NEXTHDR_MAX 255
```