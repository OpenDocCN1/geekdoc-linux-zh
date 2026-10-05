# 464 TCP/IP and Linux Protocol Implementation

```
217      if (val < 0 || val > 2)
218          goto e_inval;
219          np->rxopt.bits.scrcrt = val;
220          retv = 0;
221          break;
222
223  case IPv6_HOOPTS:
224              np->rxopt.bits.hopopts = valbool;
225              retv = 0;
226              break;
227
228  case IPv6_AUTHHDR:
229              np->rxopt.bits.authhdr = valbool;
230              retv = 0;
231              break;
232
233  case IPv6_DSTOPTS:
234              np->rxopt.bits.dstopts = valbool;
235              retv = 0;
236              break;
237
238  case IPv6_FLOWINFO:
239              np->rxopt.bits.rxflow = valbool;
240              retv = 0;
241              break;
```

Packet options:

**Figure 6.374** IPv6-socket glue set socket options: linux/net/ipv6/ipv6_sockglue.c.

```
243  case IPv6_PKTOOPTIONS:
244      {
245
246              struct ipv6_options *opt = NULL;
247              struct msghdr *msg;
248              struct flow *fl1;
249              int junk;
250
251              fl1.fi6_flowlabel = 0;
252              fl1.oif = ak->bound_dev_if;
253
254
255              if (optlen == 0)
256                  goto update;
257
258
259              opt = sock_kmalloc(opt, sizeof(*opt) + optlen, GFP_KERNEL);
260              retv = -ENBUFS;
261              if (opt == NULL)
262                  break;
263
264              memset(opt, 0, sizeof(*opt));
265              opt->tot_len = sizeof(*opt) + optlen;
266              retv = -EFAULT;
267              if (copy_from_user(opt+1, optval, optlen))
```