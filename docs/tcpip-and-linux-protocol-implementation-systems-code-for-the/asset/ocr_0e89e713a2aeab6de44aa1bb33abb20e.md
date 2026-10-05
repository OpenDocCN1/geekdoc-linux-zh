# 558 TCP/IP and Linux Protocol Implementation

```
148 struct fib_result res;
149 struct net_device *dev = NULL;
150
151 memset(&akey, 0, sizeof(key));
152 key.dst = addr;
153 #ifdef CONFIG_IP_MULTIPLE_TABLES
154 res.r = NULL;
155 #endif
156
157 if (local_table || local_table->tb_lookup(local_table, &akey, &res) {
158     return NULL;
159 }
160 if (res.type == RTN_LOCAL) {
161     goto out;
162     dev = FIB_RES_DEV(res);
163 if (dev) {
164         atomic_inc(&dev->refcnt);
165     }
166 out:
167     fib_res_put(&res);
168     return dev;
169 }
```

Figure 8.13 FIB front end–by address type: linux/net/ipv4/fib_frontend.c

```
171 unsigned in_inet_addr(u32 addr)
172 {
173     struct rt_key key;
174     struct fib_result res;
175     unsigned ret = RTN_BROADCAST;
176
177     if (ZERONET(addr) || BADCLASS(addr))
178         return RTN_BROADCAST;
179     if (MULTICAST(addr))
180         return RTN_MULTICAST;
181
182     memset(&akey, 0, sizeof(key));
183     key.dst = addr;
184     #ifdef CONFIG_IP_MULTIPLE_TABLES
185         res.r = NULL;
186     #endif
187
188     if (local_table) {
189         ret = RTN_UNICAST;
190         if (local_table->tb_lookup(local_table, &akey, &res) == 0) {
191             ret = res.type;
192             fib_res_put(&res);
193         }
194     }
195     return ret;
196 }
```