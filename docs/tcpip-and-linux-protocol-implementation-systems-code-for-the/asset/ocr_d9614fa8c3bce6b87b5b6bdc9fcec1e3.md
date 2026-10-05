# TCP/IP and Linux Protocol Implementation

```
206 freebind : 1;
207 __u8 pmutudisc;
208 int mc_index; /* Multicast device index */
209 __u32 mc_addr;
210 struct ipc_socklist *mc_list; /* Group array */
211 };
```

Figure 5.142 Socket IPv6 state: linux/include/net/sock.h

```
140 struct ipv6_pinfo {
141 struct in6_addr saddr;
142 struct in6_addr rcv_saddr;
143 struct in6_addr daddr;
144 struct in6_addr *daddr_cache;
145
146 flow_label;
147 __u32 frag_size;
148 __u32 hop_limit;
149 int mcast_hops;
150 int mcast_oif;
151
152 /* pkpton flags flags */
153 union {
154 struct {
155 __u8 arcrt:2;
156 rxinfo:1;
157 rxhlim:1;
158 hopopts:1;
159 detctops:1;
160 authhdr:1;
161 rxflow:1;
162 } bits;
163 __u8 all;
164 } rxopt;
165
166 /* sockopt flags */
167 __u8 mc_loop:1;
168 recverr:1;
169 sndflow:1;
170 pmutudisc:1;
171
172 struct ipv6_socklist *ipv6_mc_list;
173 struct ipv6_fl_socklist *ipv6_fl_list;
174 __u32 dst_cookie;
175
176 struct ipv6_txoptions *opt;
177 struct sk_buff *pkptoptions;
178 };
```