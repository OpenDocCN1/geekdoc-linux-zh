

# 基础设施协议 257

这些被广泛实现，尽管它们确实在 ISP 进行回溯的能力方面存在严重的安全漏洞。
路由器告警（router alert）正成为这一有趣的例外，因为它通常在依赖其影响的数据包流中偶尔使用。
IPv6 采取了不同的设计，将逐跳选项（out-by-hop options）与端到端选项分离，并为路由器提供了易于找到下一个头的头部。我们将在本章后面的部分讨论这一点。

**图 6.64** 互联网协议选项-构建 IP 选项头部：linux/net/ipv4/ip_options.c。

```c
/*
 * 将选项写入 IP 头部，将目的地址记录到
 * 源路由选项、输出接口的地址
 * （我们应该已经知道了，该函数允许在路由决策
 * 之后被调用）以及时间戳，
 * 如果数据报文是由我们产生的。
 * daddr 是真实的目的地址，下一跳记录在 IP 头部中。
 * saddr 是输出接口的地址。
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

# 258 TCP/IP 与 Linux 协议实现

```c
67   {
68     if (opt->ts) {
69         memset(iph+opt->ts, IPOPT_NOP, iph[opt->ts+1]);
70         opt->ts = 0;
71         opt->needsaddr = opt->needtime = 0;
72     }
73   }
```

图 6.65 IP 选项-回显：linux/net/ipv4/ip_options.c。

```c
75   /*
76    * 提供的 (soft, skb) 指向接收选项，
77    * 在 doct 中编译的合适的选项集以进行回答。
78    * 即反转 SRR 选项，复制其他选项，
79    * 并在 RR/TS 选项中留出空间。
80    *
81    * 注意：dopt 不能指向 skb。
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

图 6.66 IP 选项-回显：linux/net/ipv4/ip_options.c。

```c
if (sopt->rr) {
    optlen = sptr[sopt->rr+1];
    offsetset = sptr[sopt->rr+2];
```

# 基础设施协议 259

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

图 6.67 IP 选项-回显：linux/net/ipv4/ip_options.c。

```c
130  if (offset <= optlen) {
131      if (sopt->ts_needs_daddr) {
132          if (offset + 3 < optlen)
133              return -EINVAL;
134          dopt->ts_needs_daddr = 1;
135          offset = 4;
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

# 260 TCP/IP 与 Linux 协议实现

### 6.68 IP-回显：linux/net/ipv4/ip_options.c。

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
            // RFC 1812 要求修复错误的源路由
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

### 6.69 IP 选项-分片中的选项清零：linux/net/ipv4/ip.options.c。

```c
/*
“分片”选项，仅用 NOOP 填充在分片中不允许允许的选项。
简单而愚蠢 (0)，但是最高效的方法。
*/
```

```c
void ip_options_fragment(struct skb_buff *skb) {
    unsigned char * optptr = skb->nh->raw;
    struct ip_options *opt = &(IP(skb)->opt);
    int l1 = opt->optlen;
```

# 基础设施协议 261

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

*(注：由于文本中存在大量重复的代码段落和描述，已根据“不要重复输出原文”的原则进行了去重处理和翻译)*

