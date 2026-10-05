# Figure 6.75 IP-validate inbound packet header options: linux:/net/ipv4/
options.c.

```
382            case IPOPT_TS_PRESPEC:
383            if (optptr[2]+7 > optptr[1]) {
384                    pp_ptr = optptr + 2;
385                    goto error;
386                }
387            opt->ts = optptr - iph;
388            {
389                u32 addr;
390                memcpy(&addr, &optptr[optptr[2]-1, 4);
391                if (inst_add_type(addr) == RTN_UNICAST)
392                    break;
393                }
394                if (skb)
395                    timptr = ((u32*)optptr[optptr[2]+3];
396}
397            opt->ts_needtime = 1;
398            optptr[2] += 8;
399            break;
400            default:
401                if (skb && !capable(CAP_NET_RAW)) {
402                    pp_ptr = optptr + 3;
403                    goto error;
404                }
405                break;
406            }
407            if (timptr) {
408                struct timeval tv;
409                u32 midtime;
410                do_gettimeofday(&tv);
411                midtime = htonl((tv.tv_sec % 86400) * 1000 + tv.tv_usec
412                / 1000);
413                memcpy(timptr, &midtime, sizeof(u32));
414                opt->is_changed = 1;
415            } else {
416                unsigned overflow = optptr[3]>>4;
417                if (overflow == 15) {
418                    pp_ptr = optptr + 3;
419                    goto error;
420                }
421                opt->ts = optptr - iph;
422                if (skb) {
423                    optptr[3] = (optptr[3]&0xF)|((overflow+1)<<4);
424                    opt->is_changed = 1;
425                }
426            }
427            break;
```