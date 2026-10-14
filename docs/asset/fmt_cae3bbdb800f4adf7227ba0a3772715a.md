
132    if (flags & 8)

133        ip_cmsg_recv_opts(msg, skb);

134    if ((flags>>4) == 0)

135        return;

136

137    if (flags & 16)

138        ip_cmsg_rec_retops(msg, skb);

139 }

```

图 6.8 IP 套接字胶层–发送 CMSG：linux/net/ipv4/ip_sockglue.c。

```c
142    int ip_cmg_send(struct msghdr *msg, struct ip_cookie *ipc)
143    {
144        int err;
145        struct cmghdr *cmg;
146
147        for (cmg = CMG_FIRSTHDR(msg); cmg; cmg = CMG_NXHDR(msg, cmg)) {
148            if (cmg->cmg_len < sizeof(struct cmghdr)) ||
149                (unsigned long)((char*)ipc - (char*)msg->msg_control)
150                + cmg->cmg_len) > msg->msg_control) {
151                return -EINVAL;
152            }
153            if (cmg->cmg_level == SOL_IP) {
154                continue;
155                switch (cmg->cmg_type) {
156                case IP_OPTS:
157                    err = cmg->cmg_len - CMG_ALIGN(sizeof(struct cmghdr));
158                    err = ip_options_get(&opt, CMG_DATA(cmg), err < 40 ? 40 : 0);
159                    if (err)
160                        return err;
161                    break;
162                case IP_PKTINFO:
163                    {
164                        struct ip_pktinfo *pktinfo;
165                        if (cmg->cmg_len < LEN(struct ip_pktinfo))
166                            return -EINVAL;
167                        pktinfo = (struct ip_pktinfo*)CMG_DATA(cmg);
168                        ipc->ipi_index = pktinfo->ipi_index;
169                        ipc->addr = pktinfo->ipi_spec_dst.s_addr;
170                        break;
171                    default:
172                        return -EINVAL;
173                }
174            }
175        }
176        return 0;
177    }
```

# 基础设施协议 273

图 6.87 IP 套接字胶层-用户层路由器处理器：linux/net/ipv4/ip_sockglue.c。

```c
// 路由器选项捕获的数据包的特殊输入。
// 它们通过协议字段进行选择，并且仅在有人需要时！
// 这是用户层的问题，取决于它将对它们做什么。
// 我不知道它将如何对它们进行伪装或 NAT 处理，
// 接收者应该足够转发请求以到达目的地。

static void ip_ra_control(struct sock *sk, unsigned char ra, void (*destructor)(struct sock))
{
	struct ip_ra_chain *new_ra, *rap;
	rwlock_t ip_ra_lock = RW_LOCKED;
	if (sk->type == SOCK_RAW || sk->num == IPPROTO_RAW)
		return -EINVAL;
	new_ra = kmalloc(sizeof(new_ra), GFP_KERNEL);
	write_lock(&ip_ra_lock);
	for (rap = &ip_ra_chain; *rap != NULL; ra++) {
		if (ra->sk == sk) {
			if (destructor) {
				unlock_bh(&ip_ra_lock);
				if (new_ra)
					kfree(new_ra);
				return -EADDRUSE;
			}
			rap = ra->next;
			unlock_bh(&ip_ra_lock);
		if (destructor) {
				destructor(sk);
				sock_put(sk);
				kfree(sk);
				return 0;
		}
	}
	if (new_ra == NULL) {
		unlock_bh(&ip_ra_lock);
		return -ENOBUFS;
	}
	new_ra->sk = sk;
	new_ra->destructor = destructor;
	new_ra->next = ra;
	*rap = new_ra;
	sock_hold(sk);
	unlock_bh(&ip_ra_lock);
	return 0;
}
```

图 6.89 IP 套接字胶层–ICMP 错误到套接字错误的映射：linux/net/ipv4/ip_sockglue.c。

```c
void ip_icmp_error(struct *sk, struct sk_buff *skb, int err,
u16 port, u32 info, unsigned *payload)
{
	struct_externr_skb *serr;
	if (!sk->info.af_inet.recverr)
		return;
	skb = skb_clone(skb, GFP_ATOMIC);
	if (!skb)
		return;
	serr = SKB_EXT_ERR(skb);
	serr->ee.errno = err;
	serr->ee.origin = SO_EE_ORIGIN_ICMP;
	serr->ee_ee_type = skb->h->icmph->type;
	serr->ee_code = skb->h->icmph->code;
	serr->ee.ee_pad = 0;
	serr->ee.ee_info = info;
	serr->ee.ee_data = 0;
	serr->daddr_from = (unsigned *)&((struct *) (skb->h->icmph+1)) - skb->nh.raw;
	serr->port = port;
	skb->b.raw = payload;
	skb_pull(skb, payload - skb->data);
	if (sock_queue_err_skb(sk, skb))
		kfree_skb(skb);
}
```

# 图 6.90 IP 套接字胶层–本地错误问题：linux/net/ipv4/ip_sockglue.c。

```c
void ip_local_error(struct *sk, int err, u32 daddr, u16 port, u32 info)
{
	struct_externr_skb *serr;
	struct iphdr *iphdr;
	struct sk_buff *skb;
}
```

# 基础设施协议 275

```c
271 if (!sk->protinfo.af_inet.recverr)
272
273 return;
274
```
