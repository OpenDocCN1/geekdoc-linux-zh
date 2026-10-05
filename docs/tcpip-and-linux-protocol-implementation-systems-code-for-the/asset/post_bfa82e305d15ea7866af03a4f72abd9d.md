
# Infrastructure Protocols 257

were widely implemented, although they do represent a nasty security hole in the capability for an ISP to do traceback.
The router alert is becoming an interesting exception to this, since it is typically used only occasionally in the stream of packets that rely on its effect.
IPv6 makes a different design decision to separate out-by-hop options from end-to-end options and give a handle to routers to find the next-header easily. We'll look at this later in this chapter.

**Figure 6.64** Internet Protocol–options–build IP option header: linux/net/ipv4/ip_options.c.

```c
/*
 * Write options to IP header, record destination address to
 * source route option, address of outgoing interface
 * (we should already know it, that this function is allowed be
 * called only after routing decision) and timestamp,
 * if we originate this datagram.
 * daddr is real destination address, next hop is recorded in IP header.
 * saddr is address of outgoing interface.
 */

void ip_options_build(struct skb_buff *skb, struct ip_options *opt,
			u32 daddr, struct rtable *rt, int is_frag)
{
		unsigned char iph = skb->nh->raw;

		memcpy((IP(skb)->opt), opt, sizeof(struct ip_options));
		memcpy(iph+sizeof(struct ipphdr), opt->_data, opt->optlen);
		opt = &(IP(skb)->opt);
		topt->is_data = 0;

	if (opt->rr) {
		memcpy(iph+opt->rr+srr[opt->srr-1]-4, &daddr, 4);
		if (is_frag) {
			rt_get_source(iph+opt->rr+iph[opt->rr+2], 5, rt);
			topt->needs_daddr;
			rt_get_source(iph+opt->ts+iph[opt->ts-2], 9, rt);
			if (opt->ts==nextime) {
				struct time tv;
				u32 datetime;
				do_gettimeofday(&tv);
				midtime = htonl((tv.tv_sec % 86400) + 1000 + tv.tv_usec / 1000);
				memcpy(iph+opt->ts+iph[opt->ts-2], &midtime, 4);
			}
		}
		return;
	}
	if (opt->rr) {
		memset(iph+opt->rr, IPOT_NOP, iph[opt->rr+1]);
		topt->rr = 0;
		topt->rr_needs_daddr = 0;
```

# 258 TCP/IP and Linux Protocol Implementation

```c
67   {
68     if (opt->ts) {
69         memset(iph+opt->ts, IPOPT_NOP, iph[opt->ts+1]);
70         opt->ts = 0;
71         opt->needsaddr = opt->needtime = 0;
72     }
73   }
```

Figure 6.65 IP options-echo: linux/net/ipv4/ip_options.c.

```c
75   /*
76    * Provided (soft, skb) points to receive options,
77    * build in doct compiled option set appropriate for answering.
78    * i.e. invert SRR option, copy others,
79    * and grab room in RR/TS options.
80    *
81    * NOTE: dopt cannot point to skb.
82    */
83 
84   int ip_options_echo(struct ip_options *dopt, struct skb_buff *skb) 
85   {
86       struct ip_options *sopt;
87       unsigned char *sptr, *dptr;
88       int offsetset;
89       int optlen;
90       u32 daddr;
91 
92       memset(dopt, 0, sizeof(struct ip_options));
93 
94       dopt->is_data = 1;
95 
96       sopt = &IPCB(skb)->opt;
97 
98       if (sopt->optlen == 0) {
99           dopt->optlen = 0;
100          return 0;
101     }
102 
103      sptr = skb->nh->raw;
104      dptr = dopt->__data;
105 
106      if (skb->dst) {
107          daddr = ((struct rtable*)skb->dst)->rt_spec_dst;
108      else
109          daddr = skb->nh->iph->daddr;
```

Figure 6.66 IP options-echo: linux/net/ipv4/ip_options.c.

```c
if (sopt->rr) {
    optlen = sptr[sopt->rr+1];
    offsetset = sptr[sopt->rr+2];
```

# Infrastructure Protocols 259

```c
114  dopt->rr = dopt->optlen + sizeof(struct iphdr);
115  memcpy(dptr, sptr+sopt->rr, optlen);
116  if (sopt->rr_needs_daddr && offset <= optlen)
117      if (offset + 3 < optlen)
118          return -EINVAL;
119          dptr[2] = offset + 4;
120          dopt->rr_needs_daddr = 1;
121      }
122  dptr += optlen;
123  dopt->optlen += optlen;
124  }
125  if (sopt->ts) {
126      optlen = sptr[sopt->ts+1];
127      offset = sptr[sopt->ts+2];
128      dopt->ts = dopt->optlen + sizeof(struct iphdr);
129      memcpy(dptr, sptr+sopt->ts, optlen);
```

Figure 6.67 IP options-echo: linux/net/ipv4/ip_options.c.

```c
130  if (offset <= optlen) {
131      if (sopt->ts_needs_daddr) {
132          if (offset + 3 < optlen)
133              return -EINVAL;
134          dopt->ts_needs_daddr = 1;
135              offset = 4;
136      }
137      if (sopt->ts_needs_time) {
138          if (offset + 3 < optlen)
139              return -EINVAL;
140              if ((dptr[3]&0xF) != IPOT_TS_SPEC) {
141              dopt->ts_needs_time = 1;
142              offset += 4;
143          } else {
144              dopt->ts_needs_time = 0;
145          }
146      }
147      if (offset <= optlen) {
148          __u32 addr;
149          memcpy(&addr, sptr+sopt->offset-1, 4);
150          if (addr_type(addr) != RT_LOCAL) {
151              dopt->ts_needs_time = 1;
152              offset += 8;
153          }
154      }
155  }
156  }
157  dptr[2] = offset;
158  }
159  dptr += optlen;
160  dopt->optlen += optlen;
161  }
```

# 260 TCP/IP and Linux Protocol Implementation

### 6.68 IP-echo: linux/net/ipv4/ip_options.c. (Wait, the text says echo/ip_options.c)

```c
if (sopt->rr) {
    unsigned char * start = sptr+sopt->rr;
    u32 faddr;

    optlen = start[1];
    offset = start[2];
    doffset = 0;
    if (sopt->rr_needs_daddr) {
        offset = optlen + 1;
        offset = -4;
        if (sopt > 3) {
            memcpy(&faddr, &start[offset-1], 4);
            for (offset=-4, doffset=4; offset > 3; offset=-4, doffset+=4) {
                memcpy(&dopt[doffset], &start[offset-1], 4);
            }
            // RFC 1812 requires to fix illegal source routes.
            if (memcmp(skb->nh->ip->saddr, &start[offset+3], 4) == 0)
                doffset = -4;
        }
    }
    if (sopt > 3) {
        memcpy(&start[doffset-1], &addr, 4);
        dopt->faddr = faddr;
        dptr[0] = start[0];
        dptr[1] = doffset+3;
        dptr[2] = 4;
        dptr += doffset+3;
        dopt->sr = -dopt->optlen + sizeof(struct iphdr);
        dopt->optlen += doffset+3;
        dopt->is_strictroute = sopt->is_strictroute;
    }
    while (dopt->optlen < 3) {
        *dptr++ = IPOT_END;
        dopt->optlen++;
    }
    return 0;
```

### 6.69 IP-options-zero-out options in frags: linux/net/ipv4/ip.options.c.

```c
/*
Options "fragmenting", just fill options not
allowed in fragments with NOOPs.
 Simple and stupid (0), but the most efficient way.
*/
```

```c
void ip_options_fragment(struct skb_buff *skb) {
    unsigned char * optptr = skb->nh->raw;
    struct ip_options *opt = &(IP(skb)->opt);
    int l1 = opt->optlen;
```

# Infrastructure Protocols 261

```c
212 int optlen;
213 while (l > 0) {
214     switch (*optptr) {
215         case IPOT_END:
216             return;
217         case IPOT_NOOP:
218             l--;
219             optptr++;
220             continue;
221     }
222     optlen = optptr[1];
223     if (optlen<2 || optlen>1) {
224             pp_ptr = optptr;
225             goto error;
226     }
```

# Infrastructure Protocols 257

were widely implemented, although they do represent a nasty security hole in the capability for an ISP to do traceback.
The router alert is becoming an interesting exception to this, since it is typically used only occasionally in the stream of packets that rely on its effect.
IPv6 makes a different design decision to separate out-by-hop options from end-to-end options and give a handle to routers to find the next-header easily. We'll look at this later in this chapter.

**Figure 6.64** Internet Protocol–options–build IP option header: linux/net/ipv4/ip_options.c.

```c
/*
 * Write options to IP header, record destination address to
 * source route option, address of outgoing interface
 * (we should already know it, that this function is allowed be
 * called only after routing decision) and timestamp,
 * if we originate this datagram.
 * daddr is real destination address, next hop is recorded in IP header.
 * saddr is address of outgoing interface.
 */

void ip_options_build(struct skb_buff *skb, struct ip_options *opt,
			u32 daddr, struct rtable *rt, int is_frag)
{
		unsigned char iph = skb->nh->raw;

		memcpy((IP(skb)->opt), opt, sizeof(struct ip_options));
		memcpy(iph+sizeof(struct ipphdr), opt->_data, opt->optlen);
		opt = &(IP(skb)->opt);
		topt->is_data = 0;

	if (opt->rr) {
		memcpy(iph+opt->rr+srr[opt->srr-1]-4, &daddr, 4);
		if (is_frag) {
			rt_get_source(iph+opt->rr+iph[opt->rr+2], 5, rt);
			topt->needs_daddr;
			rt_get_source(iph+opt->ts+iph[opt->ts-2], 9, rt);
			if (opt->ts==nextime) {
				struct time tv;
				u32 datetime;
				do_gettimeofday(&tv);
				midtime = htonl((tv.tv_sec % 86400) + 1000 + tv.tv_usec / 1000);
				memcpy(iph+opt->ts+iph[opt->ts-2], &midtime, 4);
			}
		}
		return;
	}
	if (opt->rr) {
		memset(iph+opt->rr, IPOT_NOP, iph[opt->rr+1]);
		topt->rr = 0;
		topt->rr_needs_daddr = 0;
```

# 258 TCP/IP and Linux Protocol Implementation

```c
67   {
68     if (opt->ts) {
69         memset(iph+opt->ts, IPOPT_NOP, iph[opt->ts+1]);
70         opt->ts = 0;
71         opt->needsaddr = opt->needtime = 0;
72     }
73   }
```

Figure 6.65 IP options-echo: linux/net/ipv4/ip_options.c.

```c
75   /*
76    * Provided (soft, skb) points to receive options,
77    * build in doct compiled option set appropriate for answering.
78    * i.e. invert SRR option, copy others,
79    * and grab room in RR/TS options.
80    *
81    * NOTE: dopt cannot point to skb.
82    */
83 
84   int ip_options_echo(struct ip_options *dopt, struct skb_buff *skb) 
85   {
86       struct ip_options *sopt;
87       unsigned char *sptr, *dptr;
88       int offsetset;
89       int optlen;
90       u32 daddr;
91 
92       memset(dopt, 0, sizeof(struct ip_options));
93 
94       dopt->is_data = 1;
95 
96       sopt = &IPCB(skb)->opt;
97 
98       if (sopt->optlen == 0) {
99           dopt->optlen = 0;
100          return 0;
101     }
102 
103      sptr = skb->nh->raw;
104      dptr = dopt->__data;
105 
106      if (skb->dst) {
107          daddr = ((struct rtable*)skb->dst)->rt_spec_dst;
108      else
109          daddr = skb->nh->iph->daddr;
```

Figure 6.66 IP options-echo: linux/net/ipv4/ip_options.c.

```c
if (sopt->rr) {
    optlen = sptr[sopt->rr+1];
    offsetset = sptr[sopt->rr+2];
```

# Infrastructure Protocols 259

```c
114  dopt->rr = dopt->optlen + sizeof(struct iphdr);
115  memcpy(dptr, sptr+sopt->rr, optlen);
116  if (sopt->rr_needs_daddr && offset <= optlen)
117      if (offset + 3 < optlen)
118          return -EINVAL;
119          dptr[2] = offset + 4;
120          dopt->rr_needs_daddr = 1;
121      }
122  dptr += optlen;
123  dopt->optlen += optlen;
124  }
125  if (sopt->ts) {
126      optlen = sptr[sopt->ts+1];
127      offset = sptr[sopt->ts+2];
128      dopt->ts = dopt->optlen + sizeof(struct iphdr);
129      memcpy(dptr, sptr+sopt->ts, optlen);
```

Figure 6.67 IP options-echo: linux/net/ipv4/ip_options.c.

```c
130  if (offset <= optlen) {
131      if (sopt->ts_needs_daddr) {
132          if (offset + 3 < optlen)
133              return -EINVAL;
134          dopt->ts_needs_daddr = 1;
135              offset = 4;
136      }
137      if (sopt->ts_needs_time) {
138          if (offset + 3 < optlen)
139              return -EINVAL;
140              if ((dptr[3]&0xF) != IPOT_TS_SPEC) {
141              dopt->ts_needs_time = 1;
142              offset += 4;
143          } else {
144              dopt->ts_needs_time = 0;
145          }
146      }
147      if (offset <= optlen) {
148          __u32 addr;
149          memcpy(&addr, sptr+sopt->offset-1, 4);
150          if (addr_type(addr) != RT_LOCAL) {
151              dopt->ts_needs_time = 1;
152              offset += 8;
153          }
154      }
155  }
156  }
157  dptr[2] = offset;
158  }
159  dptr += optlen;
160  dopt->optlen += optlen;
161  }
```

# 260 TCP/IP and Linux Protocol Implementation

### 6.68 IP-echo: linux/net/ipv4/ip_options.c.

```c
if (sopt->rr) {
    unsigned char * start = sptr+sopt->rr;
    u32 faddr;

    optlen = start[1];
    offset = start[2];
    doffset = 0;
    if (sopt->rr_needs_daddr) {
        offset = optlen + 1;
        offset = -4;
        if (sopt > 3) {
            memcpy(&faddr, &start[offset-1], 4);
            for (offset=-4, doffset=4; offset > 3; offset=-4, doffset+=4) {
                memcpy(&dopt[doffset], &start[offset-1], 4);
            }
            // RFC 1812 requires to fix illegal source routes.
            if (memcmp(skb->nh->ip->saddr, &start[offset+3], 4) == 0)
                doffset = -4;
        }
    }
    if (sopt > 3) {
        memcpy(&start[doffset-1], &addr, 4);
        dopt->faddr = faddr;
        dptr[0] = start[0];
        dptr[1] = doffset+3;
        dptr[2] = 4;
        dptr += doffset+3;
        dopt->sr = -dopt->optlen + sizeof(struct iphdr);
        dopt->optlen += doffset+3;
        dopt->is_strictroute = sopt->is_strictroute;
    }
    while (dopt->optlen < 3) {
        *dptr++ = IPOT_END;
        dopt->optlen++;
    }
    return 0;
```

### 6.69 IP-options-zero-out options in frags: linux/net/ipv4/ip.options.c.

```c
/*
Options "fragmenting", just fill options not
allowed in fragments with NOOPs.
 Simple and stupid (0), but the most efficient way.
*/
```

```c
void ip_options_fragment(struct sk_buff *skb) {
    unsigned char * optptr = skb->nh->raw;
    struct ip_options *opt = &(IP(skb)->opt);
    int l1 = opt->optlen;
```

# Infrastructure Protocols 261

```c
212 int optlen;
213 while (l > 0) {
214     switch (*optptr) {
215         case IPOT_END:
216             return;
217         case IPOT_NOOP:
218             l--;
219             optptr++;
220             continue;
221     }
222     optlen = optptr[1];
223     if (optlen<2 || optlen>1) {
224             pp_ptr = optptr;
225             goto error;
226     }
```

# Infrastructure Protocols 257

were widely implemented, although they do represent a nasty security hole in the capability for an ISP to do traceback.
The router alert is becoming an interesting exception to this, since it is typically used only occasionally in the stream of packets that rely on its effect.
IPv6 makes a different design decision to separate out-by-hop options from end-to-end options and give a handle to routers to find the next-header easily. We'll look at this later in this chapter.

**Figure 6.64** Internet Protocol–options–build IP option header: linux/net/ipv4/ip_options.c.

```c
/*
 * Write options to IP header, record destination address to
 * source route option, address of outgoing interface
 * (we should already know it, that this function is allowed be
 * called only after routing decision) and timestamp,
 * if we originate this datagram.
 * daddr is real destination address, next hop is recorded in IP header.
 * saddr is address of outgoing interface.
 */

void ip_options_build(struct skb_buff *skb, struct ip_options *opt,
			u32 daddr, struct rtable *rt, int is_frag)
{
		unsigned char iph = skb->nh->raw;

		memcpy((IP(skb)->opt), opt, sizeof(struct ip_options));
		memcpy(iph+sizeof(struct ipphdr), opt->_data, opt->optlen);
		opt = &(IP(skb)->opt);
		topt->is_data = 0;

	if (opt->rr) {
		memcpy(iph+opt->rr+srr[opt->srr-1]-4, &daddr, 4);
		if (is_frag) {
			rt_get_source(iph+opt->rr+iph[opt->rr+2], 5, rt);
			topt->needs_daddr;
			rt_get_source(iph+opt->ts+iph[opt->ts-2], 9, rt);
			if (opt->ts==nextime) {
				struct time tv;
				u32 datetime;
				do_gettimeofday(&tv);
				midtime = htonl((tv.tv_sec % 86400) + 1000 + tv.tv_usec / 1000);
				memcpy(iph+opt->ts+iph[opt->ts-2], &midtime, 4);
			}
		}
		return;
	}
	if (opt->rr) {
		memset(iph+opt->rr, IPOT_NOP, iph[opt->rr+1]);
		topt->rr = 0;
		topt->rr_needs_daddr = 0;
```

# 258 TCP/IP and Linux Protocol Implementation

```c
67   {
68     if (opt->ts) {
69         memset(iph+opt->ts, IPOPT_NOP, iph[opt->ts+1]);
70         opt->ts = 0;
71         opt->needsaddr = opt->needtime = 0;
72     }
73   }
```

Figure 6.65 IP options-echo: linux/net/ipv4/ip_options.c.

```c
75   /*
76    * Provided (soft, skb) points to receive options,
77    * build in doct compiled option set appropriate for answering.
78    * i.e. invert SRR option, copy others,
79    * and grab room in RR/TS options.
80    *
81    * NOTE: dopt cannot point to skb.
82    */
83 
84   int ip_options_echo(struct ip_options *dopt, struct skb_buff *skb) 
85   {
86       struct ip_options *sopt;
87       unsigned char *sptr, *dptr;
88       int offsetset;
89       int optlen;
90       u32 daddr;
91 
92       memset(dopt, 0, sizeof(struct ip_options));
93 
94       dopt->is_data = 1;
95 
96       sopt = &IPCB(skb)->opt;
97 
98       if (sopt->optlen == 0) {
99           dopt->optlen = 0;
100          return 0;
101     }
102 
103      sptr = skb->nh->raw;
104      dptr = dopt->__data;
105 
106      if (skb->dst) {
107          daddr = ((struct rtable*)skb->dst)->rt_spec_dst;
108      else
109          daddr = skb->nh->iph->daddr;
```

Figure 6.66 IP options-echo: linux/net/ipv4/ip_options.c.

```c
if (sopt->rr) {
    optlen = sptr[sopt->rr+1];
    offsetset = sptr[sopt->rr+2];
```

# Infrastructure Protocols 259

```c
114  dopt->rr = dopt->optlen + sizeof(struct iphdr);
115  memcpy(dptr, sptr+sopt->rr, optlen);
116  if (sopt->rr_needs_daddr && offset <= optlen)
117      if (offset + 3 < optlen)
118          return -EINVAL;
119          dptr[2] = offset + 4;
120          dopt->rr_needs_daddr = 1;
121      }
122  dptr += optlen;
123  dopt->optlen += optlen;
124  }
125  if (sopt->ts) {
126      optlen = sptr[sopt->ts+1];
127      offset = sptr[sopt->ts+2];
128      dopt->ts = dopt->optlen + sizeof(struct iphdr);
129      memcpy(dptr, sptr+sopt->ts, optlen);
```

Figure 6.67 IP options-echo: linux/net/ipv4/ip_options.c.

```c
130  if (offset <= optlen) {
131      if (sopt->ts_needs_daddr) {
132          if (offset + 3 < optlen)
133              return -EINVAL;
134          dopt->ts_needs_daddr = 1;
135              offset = 4;
136      }
137      if (sopt->ts_needs_time) {
138          if (offset + 3 < optlen)
139              return -EINVAL;
140              if ((dptr[3]&0xF) != IPOT_TS_SPEC) {
141              dopt->ts_needs_time = 1;
142              offset += 4;
143          } else {
144              dopt->ts_needs_time = 0;
145          }
146      }
147      if (offset <= optlen) {
148          __u32 addr;
149          memcpy(&addr, sptr+sopt->offset-1, 4);
150          if (addr_type(addr) != RT_LOCAL) {
151              dopt->ts_needs_time = 1;
152              offset += 8;
153          }
154      }
155  }
156  }
157  dptr[2] = offset;
158  }
159  dptr += optlen;
160  dopt->optlen += optlen;
161  }
```

# 260 TCP/IP and Linux Protocol Implementation

### 6.68 IP-echo: linux/net/ipv4/ip_options.c.

```c
if (sopt->rr) {
    unsigned char * start = sptr+sopt->rr;
    u32 faddr;

    optlen = start[1];
    offset = start[2];
    doffset = 0;
    if (sopt->rr_needs_daddr) {
        offset = optlen + 1;
        offset = -4;
        if (sopt > 3) {
            memcpy(&faddr, &start[offset-1], 4);
            for (offset=-4, doffset=4; offset > 3; offset=-4, doffset+=4) {
                memcpy(&dopt[doffset], &start[offset-1], 4);
            }
            // RFC 1812 requires to fix illegal source routes.
            if (memcmp(skb->nh->ip->saddr, &start[offset+3], 4) == 0)
                doffset = -4;
        }
    }
    if (sopt > 3) {
        memcpy(&start[doffset-1], &addr, 4);
        dopt->faddr = faddr;
        dptr[0] = start[0];
        dptr[1] = doffset+3;
        dptr[2] = 4;
        dptr += doffset+3;
        dopt->sr = -dopt->optlen + sizeof(struct iphdr);
        dopt->optlen += doffset+3;
        dopt->is_strictroute = sopt->is_strictroute;
    }
    while (dopt->optlen < 3) {
        *dptr++ = IPOT_END;
        dopt->optlen++;
    }
    return 0;
```

### 6.69 IP-options-zero-out options in frags: linux/net/ipv4/ip.options.c.

```c
/*
Options "fragmenting", just fill options not
allowed in fragments with NOOPs.
 Simple and stupid (0), but the most efficient way.
*/
```

```c
void ip_options_fragment(struct skb_buff *skb) {
    unsigned char * optptr = skb->nh->raw;
    struct ip_options *opt = &(IP(skb)->opt);
    int l1 = opt->optlen;
```

# Infrastructure Protocols 261

```c
212 int optlen;
213 while (l > 0) {
214     switch (*optptr) {
215         case IPOT_END:
216             return;
217         case IPOT_NOOP:
218             l--;
219             optptr++;
220             continue;
221     }
222     optlen = optptr[1];
223     if (optlen<2 || optlen>1) {
224             pp_ptr = optptr;
225             goto error;
226     }
```
