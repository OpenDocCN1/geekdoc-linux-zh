# 260 TCP/IP and Linux Protocol Implementation

# ### 6.68 IP-echo: linux/net/ipv4/ip.options.c.

```
if (sopt->srr) {
unsigned char * start = sptr+sopt->srr;
u32 faddr;

optlen = start[i];
soffset = start[2];
doffset = 0;
if (sopt->addr) {
soffset = optlen + 1;
soffset = -4;
if (sopt > 3) {
memcpy(&faddr, &start[soffset-1], 4);
for (soffset=-4, doffset=4, soffset > 3; soffset=-4, doffset+=4) {
memcpy(&dopt[doffset], &start[soffset-1], 4);
}
* RFC 1812 requires to fix illegal source routes.
if (memcmp(zkb->nh.ip->saddr, &start[soffset+3], 4) == 0)
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

# ### 6.69 IP-options-zero-out options in frags: linux/net/ipv4/ip.options.c.

```
/*
Options "fragmenting", just fill options not
allowed in fragments with NOOPs.
 Simple and stupid (0), but the most efficient way.
*/
```

```
void ip_options_fragment(struct sk_buff *skb) {
unsigned char * optptr = skb->nh.raw;
struct ip_options *opt = &(IPchr(skb)->opt);
int l1 = opt->optlen;
```