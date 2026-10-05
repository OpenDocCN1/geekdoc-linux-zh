# TCP/IP and Linux Protocol Implementation

```
245 #endif
246 {
247     ret = FIB_RES_NH(res).nh_scope >= RT_SCOPE_HOST;
248     fib_res_put(&res);
249     return ret;
250 }
251 fib_res_put(&res);
252 if (no_addr) {
253     goto last_resort;
254 } if (rpf) {
255     goto e_inval;
256     key.oif = dev->ifindex;
257 }
258     ret = 0;
259     if (fib_lookup(&key, &res) == 0) {
260         if (res.type == RTN_UNICAST) {
261             *spec_dat = FIB_RES_PREFSERC(res);
262             ret = FIB_RES_NH(res).nh_scope >= RT_SCOPE_HOST;
263         }
264     }
265     fib_res_put(&res);
266 }
267 return ret;
```

```
268 last_resort:
269 if (rpf) {
270     goto e_inval;
271     *spec_dat = inet_select_addr(dev, 0, RT_SCOPE_UNIVERSE);
272     *itag = 0;
273 return 0;
274 }
```

```
275 e_inval:
276     fib_res_put(&res);
277 e_inval:
278     return -EINVAL;
279 }
```

Figure 8.16 FIB front end--ioctl handler: linux/net/ipv4/fib_frontend.c.

```
283 /*
284  * Handle IP routing ioctl calls. These are used to manipulate the routing
285  */
287 int ip_rt_ioctl(unsigned int cmd, void *arg)
288 {
289     int err;
290     struct kern_rta rta;
291     struct rtntry r;
292     struct {
293         struct nlmsghdr nlh;
294         struct rtmsg rtm;
295     }
296     req;
```