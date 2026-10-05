# Infrastructure Protocols 433

118

```
119
buf[0]= 0x33;
120
buf[1]= 0x33;
```

```
121
122
    memcpry(buf + 2, >>addr->s6_addr32[3], sizeof(__u32));
123
}
```

# 6.9.2 IPv6 API

Figure 6.329 IPv6 API–address family: linux/include/linux/in6.h.

```
26  /*
27   * IPv6 address structure
28   */
29
30  struct in6_addr
31  {
32      union
33      {
34          __u8   u6_addr[16];
35          __u32  u6_addr16[8];
36          __u32  u6_addr32[4];
37      }\}
38      #define s6_addr      in6.u.u6_addr8
39      #define s6_addr16    in6.u.u6_addr16
40      #define s6_addr32    in6.u.u6_addr32
41  };
```

```
43  struct sockaddr_in6 {
44      unsigned short int s6_family; /* AF_INET6 */
45      __u16 s6_port;               /* Transport layer port * /
46      __u32 s6_flowinfo;           /* IPv6 flow information * /
47      struct in6_addr s6_addr;   /* IPv6 address * /
48      __u8  s6_scope_id;         /* scope id (new in RFC 2553) */
49  };
```

Figure 6.330 IPv6 API–multicast programmer interface: linux/include/linux/in6.h.

```
51  struct ipv6_mreq {
52      /* multicast address of group * /
53      struct in6_addr ipv6mr_multiaddr;
54
55      /* local ipv6 address of interface * /
56      int ipv6mr_ifindex;
57  };
```